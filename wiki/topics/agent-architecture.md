---
type: topic
tags: [agentic-engineering, agent-architecture, llm-fundamentals, tokens, system-prompts, harness, reasoning, ghosts-vs-animals, mental-model]
created: 2026-05-23
updated: 2026-05-26
status: developing
sources: 3
---

# Agent architecture

How a coding agent is actually built under the hood. A **harness** that wraps an LLM, extending it with a system prompt and a set of callable tools, and runs the whole thing in a loop. This page goes deeper than [[coding-agents]] — that page defines what an agent *is*; this page describes how the pieces fit together.

## Synthesis

[[simon-willison]]'s framing in [[2026-05-23-how-coding-agents-work]]: *"A coding agent is a piece of software that acts as a harness for an LLM, extending that LLM with additional capabilities that are powered by invisible prompts and implemented as callable tools."* The whole architecture reduces to **LLM + system prompt + tools in a loop** — and a simple version is a few dozen lines on top of an LLM API. (A *good* version is much more work, but the mechanics are surprisingly straightforward.)

### LLMs as completion engines

An LLM is a model that completes a sequence. Given "the cat sat on the ", it suggests "mat." Scaled up with enough training, the same mechanism completes "a python function to download a file from a URL is `def download_file(url):` " into real-looking code.

LLMs don't operate on words but on **tokens** — integer IDs. "the cat sat on the " becomes `[3086, 9059, 10139, 402, 290, 220]`. Two practical consequences:
- Providers charge **per token** (input *and* output).
- Models have **hard limits on how many tokens they can consider at once** — the context window. ([[subagents]] is the architectural response to that constraint.)

The [OpenAI tokenizer](https://platform.openai.com/tokenizer) is useful to develop intuition.

**Multimodal / vision LLMs (vLLMs)** extend the same mechanism to images. A common misconception is that images go through a separate OCR/analysis pipeline — they don't. Images are tokenized and processed the same way as text.

### Chat templated prompts and statelessness

Early LLMs were used purely as completion engines. The user-friendlier model today is the **chat templated prompt**: a thin formatting convention that looks like:

```
user: write a python function to download a file from a URL
assistant:
```

The "natural completion" is the assistant's answer. But the LLM itself is **stateless** — every call starts from a blank slate. To simulate an ongoing conversation, the harness **replays the entire history** every turn:

```
user: write a python function to download a file from a URL
assistant: def download_url(url):
    return urllib.request.urlopen(url).read()
user: use the requests library instead
assistant:
```

Because input tokens grow with every turn and providers charge per token, naive replay would make long conversations prohibitively expensive.

### Token caching as the central optimization

The mitigation is **cached input tokens**: most providers charge a lower rate for token prefixes they've recently processed, because the infrastructure can reuse the expensive computation. The design consequence is significant: **coding agents are deliberately built to avoid modifying earlier conversation content** so that the cache stays warm as the conversation grows. Mutating the history is expensive even when it would simplify the logic.

### The tool-call protocol

A **tool** is a function the harness makes available to the LLM. At the prompt level it looks like this:

```
system: If you need the weather, end your turn with <tool>get_weather(city)</tool>
user: what's the weather in San Francisco?
assistant: <tool>get_weather("San Francisco")</tool>
```

The harness parses the tool call out of the response (often with a regex), executes the underlying function, and re-injects the result:

```
user: <tool-result>61°, Partly cloudy</tool-result>
assistant:
```

The LLM continues from there. Most coding agents define **a dozen or more tools**. The most powerful are the code-execution tools: a `Bash()` tool for terminal commands, a `Python()` tool for Python — and these are what make agents *coding* agents in the sense defined in [[coding-agents]].

**The browser-automation tool surface.** Once code execution is in hand, the next frontier is making the *running* application verifiable. [[2026-05-26-agentic-manual-testing]] surveys three tools that turn web UIs into something the agent can interact with the way a user would: [Playwright](https://playwright.dev/) (Microsoft, multi-binding, multi-engine), [agent-browser](https://github.com/vercel-labs/agent-browser) (Vercel; Playwright wrapper designed for agents), and [Rodney](https://github.com/simonw/rodney) (Willison; Chrome DevTools Protocol direct). These are concrete instances of [[agent-native-infrastructure]]: their `--help` text is written *as agent-onboarding documentation* and they pair naturally with the model's own vision capabilities (e.g. `rodney screenshot` → vLLM evaluation of the captured image). See [[agentic-testing]] for the full practice.

### System prompts

Every conversation typically starts with an initial **system message** that's not shown to the user. It explains the available tools, the expected output format, and any behavioral constraints. **System prompts can be hundreds of lines long.** Willison points to the [OpenAI Codex system prompt as of March 2026](https://github.com/openai/codex/blob/rust-v0.114.0/codex-rs/core/templates/model_instructions/gpt-5.2-codex_instructions_template.md) as a clear public example.

The system prompt is the surface that [[compound-engineering]] writes to — retrospective lessons accumulate as edits to the system prompt and tools.

### Reasoning / thinking mode

One of the major 2025 advances: models spend extra tokens generating text that **talks through the problem before answering**. This is similar in effect to a person thinking out loud — more tokens, more time, hopefully a better result. Particularly useful for **debugging**, where the model can mix reasoning passes with tool calls to follow function calls back to a root cause. Many agents expose a **reasoning effort dial** to spend more on harder problems.

### Putting it together

The full loop is: take the user prompt, prepend the system prompt and the conversation history, send to the LLM, parse out any tool calls, execute them, append the results, repeat — until the model emits a final response without a tool call. **LLM + system prompt + tools in a loop.**

### Mental model: ghosts, not animals

[[andrej-karpathy]]'s framing from [[2026-04-30-sequoia-ascent-karpathy]] is worth holding alongside the mechanics. LLMs are **not animals**. They have no biological drives, no embodied survival pressure, no curiosity, play, or intrinsic motivation in the animal sense. They are **statistical simulations of human artifacts**, shaped by pretraining, post-training, RL, product feedback, and economic incentives.

Why this matters in practice: anthropomorphic expectations mislead. *"These systems can be brilliant in one moment and bizarrely dumb in the next. They are not smooth human minds. They are jagged, alien tools."* See [[verifiability|jagged intelligence]] for the analytic frame that explains the unevenness — capability spikes where labs concentrated verifiable RL and data; behavior degrades elsewhere.

The posture the framing recommends: **neither dismissal nor blind trust — empirical familiarity.** Learn where the model works, where it fails, what it was trained for, and how to build guardrails around it. Yelling at the model doesn't help; testing it against your actual workload and updating the harness based on what you learn ([[compound-engineering]]) does.

The mechanics on this page describe *what* the agent is. Ghosts-not-animals is a reminder of *what kind of thing* you're interacting with — neither a human collaborator nor a deterministic computer, but a third category that needs its own intuitions.

## Open questions

- How aggressively does cache invalidation happen in practice across providers? The "don't modify earlier conversation" rule is a strong design constraint — worth understanding the actual cache-hit economics.
- When is reasoning worth its extra token cost? The dial exists; what's the right setting for which kinds of tasks?
- How thick is the harness, really? Tool definitions, prompt construction, history management, cache-aware mutation rules, retry logic — what does a *good* harness include that a naive few-dozen-line one doesn't?
- What does the system-prompt-as-living-document workflow look like in practice (the [[compound-engineering]] interface to this layer)?
- Multimodal/vision inputs are tokenized too — how do *image* token budgets compare to text, and when is sending a screenshot cheaper or more effective than describing the problem in text?

## Sources

- [[2026-05-23-how-coding-agents-work]]
- [[2026-04-30-sequoia-ascent-karpathy]]
- [[2026-05-26-agentic-manual-testing]]
