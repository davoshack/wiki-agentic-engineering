---
type: area
tags: [agentic-engineering, meta]
created: 2026-05-23
updated: 2026-05-23
status: developing
sources: 3
---

# Agentic engineering

The practice of developing software with the assistance of coding agents — AI agents that can both write *and* execute code in a loop until a stated goal is met. This is the standing domain the whole wiki is built around.

## Synthesis

Per [[simon-willison]], **agentic engineering** is "the practice of developing software with the assistance of coding agents," and an **agent** is "software that runs tools in a loop to achieve a goal." For coding agents specifically, the tool that matters most is one that can execute code — code execution is what turns LLM output from a suggestion into something that can be iterated toward demonstrable correctness. The canonical examples ingested so far are Claude Code, OpenAI Codex, and Gemini CLI.

The shift this enables is economic before it is technical. Coding agents collapse the cost of producing code to nearly zero, which invalidates a large set of long-standing engineering intuitions built around code being expensive — both macro habits (planning, estimating, scoping features against their development cost) and micro habits (refactor / test / document / build-a-debug-interface tradeoffs). See [[economics-of-code]] for the detailed picture. *Cheap* code and *good* code are not the same: Willison defines "good code" along nine dimensions (it works; we know it works; it solves the right problem; handles errors; is simple and minimal; is tested; is documented; affords future change without over-engineering; meets the relevant "ilities"), and meeting that bar remains the human's responsibility.

The human's job therefore moves up the stack. With typing no longer the bottleneck, the work becomes: deciding *what* code to write, equipping the agent with the right tools, specifying problems at the right level of detail, and verifying and iterating until the result is robust. Two emerging habits already visible in the sources support this:

- **"Fire off a prompt anyway"** — when instinct says a side experiment isn't worth the time, run an async agent on it; the worst case is a few wasted tokens.
- **[[hoarding-working-examples|Hoard working examples]]** — keep a personal collection of runnable code that proves you know how to do specific things, and use it as an input to future agent prompts (via `curl`, local filesystem search, or `git clone` to `/tmp`). The key payoff: you only ever need to figure out a trick once.

A vocabulary distinction worth preserving: agentic engineering is **not** the same as **vibe coding** ([[coding-agents]] elaborates). Vibe coding, in Karpathy's original narrow sense, is unreviewed prototype-quality LLM output; agentic engineering covers the full spectrum up to and including production-grade work.

The field is early. Best practices are being figured out in public, and the *Agentic Engineering Patterns* guide that anchors the wiki is itself explicitly a work in progress.

## Open questions

- What does the "verify and iterate" loop look like in practice when the agent runs in parallel across multiple workstreams? Existing intuitions about code review and testing assume a serial human author.
- Which parts of the "good code" checklist do current coding agents handle well unsupervised, and which still require the human to drive?
- How should the agent's tool harness be updated over time to internalize lessons? (Willison flags this as something agents *can* do but humans must deliberately do for them.)
- What habits, beyond hoarding examples and "prompt anyway," are emerging? Worth watching for further chapters and counter-perspectives.

## Sources

- [[2026-05-23-what-is-agentic-engineering]]
- [[2026-05-23-writing-code-is-cheap-now]]
- [[2026-05-23-hoard-things-you-know-how-to-do]]
