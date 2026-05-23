---
type: topic
tags: [agentic-engineering, definitions, coding-agents, vibe-coding, async-agents]
created: 2026-05-23
updated: 2026-05-23
status: developing
sources: 5
---

# Coding agents

Software that wraps an LLM in a tool-execution loop, including a tool that can run code, so it can iterate toward a stated goal until that goal is met. The defining instrument of [[agentic-engineering]].

## Synthesis

### The agent loop

[[simon-willison]] adopts a narrow, operational definition: **"Agents run tools in a loop to achieve a goal."** Concretely, an agent is software that:

1. Calls an LLM with a user prompt *and* a set of tool definitions.
2. Executes whichever tools the LLM requests.
3. Feeds the results back into the LLM.
4. Repeats until the goal is reached.

A **coding agent** is the special case where one of the available tools can execute code. Willison calls code execution *"the defining capability that makes agentic engineering possible"*: without it, an LLM's output is "of limited value"; with it, the agent can iterate toward software that demonstrably works rather than merely plausible-looking. Named examples ingested so far: [Claude Code](https://code.claude.com/), [OpenAI Codex](https://openai.com/codex/), [Gemini CLI](https://geminicli.com/).

A useful corollary: because the agent acts through tools, the *set of tools you expose to it* and *how well they work* directly shape what the agent can accomplish. Willison's prompts in [[2026-05-23-hoard-things-you-know-how-to-do]] illustrate this — he reaches for `curl` rather than a built-in WebFetch when he wants raw HTML, and he gives the agent filesystem paths or `git` access when he wants it to consult prior work. The agent's capability is the loop *plus* its tools.

A related point: LLMs by themselves don't learn from past mistakes, but coding agents *can* — provided the human deliberately updates the instructions and the tool harness based on what each round teaches. The named workflow for doing this is [[compound-engineering]].

### Synchronous vs. asynchronous

Within coding agents, [[simon-willison]] singles out **asynchronous coding agents** as a category worth using deliberately. Named examples: [Gemini Jules](https://jules.google.com/), [OpenAI Codex web](https://developers.openai.com/codex/cloud/), [Claude Code on the web](https://code.claude.com/docs/en/claude-code-on-the-web). The async flavor lets the human fire off work — typically a refactor or an exploratory prototype — without surrendering their laptop's foreground attention to it; results come back as a pull request to evaluate. The synchronous local flavor (Claude Code CLI, etc.) is what you use when you want to be in the loop. The patterns that make heaviest use of the async mode are in [[refactoring-with-agents]] and the exploratory-prototyping section of [[economics-of-code]].

### Coding agents ≠ vibe coding

[Andrej Karpathy coined "vibe coding"](https://twitter.com/karpathy/status/1886192184808149383) in February 2025 — three weeks before the first Claude Code release — to describe prompting LLMs to write code while you "forget that the code even exists." Some commentators have stretched the term to cover *any* LLM-assisted coding. Willison pushes back: the original narrow meaning is more useful, because we need vocabulary that distinguishes **unreviewed, prototype-quality LLM output** from code that the author has brought up to a production-ready standard.

For this wiki: "vibe coding" is the lower-stakes mode (prototypes, throwaways, exploration); agentic engineering covers the whole range up through production work, where the human is responsible for verification, testing, and the rest of [[economics-of-code|what makes code "good"]].

### What the human still does

Because typing code is no longer the constraint, the human's role in the loop is more clearly: choose *what* to build, equip the agent with the right tools, specify the problem at the right level of detail, and verify and iterate on results until the output is robust and credible.

## Open questions

- What's the right level of detail when specifying a problem to a coding agent? Too vague and it drifts; too detailed and you're back to typing the code yourself.
- How should the agent's tool harness be designed and updated over time so the agent accumulates capability across sessions?
- How do you set tool-access boundaries (filesystem, network, code execution) safely, especially when the agent is running asynchronously or in parallel?
- Are there meaningful capability differences between Claude Code, Codex, and Gemini CLI that affect which patterns work, or are the patterns largely portable?

## Sources

- [[2026-05-23-what-is-agentic-engineering]]
- [[2026-05-23-writing-code-is-cheap-now]]
- [[2026-05-23-hoard-things-you-know-how-to-do]]
- [[2026-05-23-ai-should-help-us-produce-better-code]]
- [[2026-05-23-anti-patterns-things-to-avoid]]
