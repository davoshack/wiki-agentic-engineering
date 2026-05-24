---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/how-coding-agents-work/
source_date: 2026-05-23
tags: [agentic-engineering, agent-architecture, llm-fundamentals, tokens, system-prompts, reasoning]
created: 2026-05-23
updated: 2026-05-23
status: developing
---

# How coding agents work

The sixth chapter of *Agentic Engineering Patterns*. A technical walkthrough of how a coding agent is actually built: an LLM wrapped in a **harness** that adds a system prompt and a set of callable tools, run in a loop. Covers LLM mechanics (tokens, statelessness, multimodal), chat templated prompts, token caching, the tool-call format, system prompts, and reasoning/thinking mode. Closing claim: *"LLM + system prompt + tools in a loop"* is most of what it takes — a simple version is a few dozen lines of code, though a good loop is much more work.

## Key takeaways

- A coding agent is **software that acts as a harness for an LLM**, extending it with extra capabilities driven by invisible prompts and implemented as callable tools.
- **LLMs are completion engines.** Given "the cat sat on the ", an LLM suggests the next word. Larger models + more training extend this to "a python function to download a file from a URL is `def download_file(url):` ".
- **LLMs work on tokens, not words.** "the cat sat on the " → `[3086, 9059, 10139, 402, 290, 220]`. Providers charge per token and have hard limits on how many tokens a model can consider at a time. The [OpenAI tokenizer](https://platform.openai.com/tokenizer) lets you experiment with this.
- **Multimodal / vision LLMs (vLLMs)** accept images alongside text. Common misconception flagged: there's no separate OCR/image-analysis step — images are tokenized and processed the same way as text tokens.
- **Chat templated prompts** are a thin wrapper around completion. The prompt looks like `user: ... \n assistant: ` and the LLM's "completion" is the assistant's reply. **LLMs are stateless**: every call starts blank. To simulate a conversation, the harness replays the entire conversation each turn. Cost grows because input tokens grow each turn.
- **Token caching** is the major mitigation. Most providers charge a lower rate for **cached input tokens** — common token prefixes processed recently can be cached at the infrastructure layer. Coding agents are designed around this: *they deliberately avoid modifying earlier conversation content to keep the cache hit rate high.*
- **Tools are functions the harness makes available to the LLM.** At the prompt level it looks like:
  ```
  system: If you need the weather, end your turn with <tool>get_weather(city)</tool>
  user: what's the weather in San Francisco?
  assistant: <tool>get_weather("San Francisco")</tool>
  ```
  The harness extracts the tool call (often with a regex), runs it, and re-injects the result as `<tool-result>61°, Partly cloudy</tool-result>`. The LLM then continues.
- Most coding agents define **a dozen or more tools**. The most powerful are the code-execution tools: a `Bash()` tool for terminal commands, a `Python()` tool for Python.
- **System prompts** are an initial "system" message that tells the model how to behave (including how to call tools). They can be hundreds of lines long. Concrete linked example: [the OpenAI Codex system prompt as of March 2026](https://github.com/openai/codex/blob/rust-v0.114.0/codex-rs/core/templates/model_instructions/gpt-5.2-codex_instructions_template.md).
- **Reasoning / thinking mode** (one of the big 2025 advances): the model spends extra tokens generating text that talks through the problem before answering. Effect is similar to a person thinking out loud — more tokens spent, hopefully better result. Particularly useful for **debugging**, since the model can mix reasoning with tool calls to trace function calls back to root causes. Many agents expose a dial for reasoning effort.
- **The whole architecture is: LLM + system prompt + tools in a loop.** *"Believe it or not, that's most of what it takes to build a coding agent!"* A simple version: a few dozen lines on top of an LLM API. A *good* loop: much more work, but the fundamentals are straightforward.

## Connections

- This is the architectural foundation for everything in [[coding-agents]] and the new dedicated topic [[agent-architecture]]. The agent-loop definition from [[2026-05-23-what-is-agentic-engineering]] now has a concrete mechanism behind it.
- **Token caching** has direct consequences for cost (see [[economics-of-code]]) and for why long-running conversations stay affordable. The "don't modify earlier conversation" design choice is part of why the linear conversation history can grow comfortably.
- **Context limit** becomes the natural setup for [[2026-05-23-subagents]] — subagents are the response to that constraint.
- **System prompts** are the surface that [[compound-engineering]] writes to: harness updates accumulating lessons across runs *are* edits to the system prompt and to the available tools.
- The "harness + tools" framing connects directly to the prompt examples in [[2026-05-23-hoard-things-you-know-how-to-do]] — `curl`, filesystem search, and `git clone` are tools invoked through this exact mechanic.
- Author: [[simon-willison]].

## Raw file

`raw/How coding agents work - Agentic Engineering Patterns.md`
