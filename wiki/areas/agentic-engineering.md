---
type: area
tags: [agentic-engineering, meta]
created: 2026-05-23
updated: 2026-05-25
status: developing
sources: 9
---

# Agentic engineering

The practice of developing software with the assistance of coding agents — AI agents that can both write *and* execute code in a loop until a stated goal is met. This is the standing domain the whole wiki is built around.

## Synthesis

Per [[simon-willison]], **agentic engineering** is "the practice of developing software with the assistance of coding agents," and an **agent** is "software that runs tools in a loop to achieve a goal." For coding agents specifically, the tool that matters most is one that can execute code — code execution is what turns LLM output from a suggestion into something that can be iterated toward demonstrable correctness. The canonical examples ingested so far are Claude Code, OpenAI Codex, and Gemini CLI. The mechanics — how the harness wraps an LLM with a system prompt, tools, token caching, and reasoning mode — are detailed in [[agent-architecture]].

[[andrej-karpathy]] (the second primary voice in the wiki) provides the canonical *floor-vs-ceiling* framing: **vibe coding raises the floor** (anyone can describe what they want and get software); **agentic engineering raises the ceiling** (the professional discipline of coordinating fallible agents while preserving correctness, security, taste, and maintainability). He places the discipline inside a paradigm shift he calls [[software-3-0]] — humans now program LLMs through context, tools, examples, and instructions, with the LLM as the interpreter. The dated **December 2025 inflection point** is his marker for when agent reliability became good enough that the unit of programming flipped from typing code to delegating "macro actions." See [[willison-vs-karpathy]] for how the two authors' frames divide and overlap.

The shift this enables is economic before it is technical. Coding agents collapse the cost of producing code to nearly zero, which invalidates a large set of long-standing engineering intuitions built around code being expensive — both macro habits (planning, estimating, scoping features against their development cost) and micro habits (refactor / test / document / build-a-debug-interface tradeoffs). See [[economics-of-code]] for the detailed picture. *Cheap* code and *good* code are not the same: Willison defines "good code" along nine dimensions (it works; we know it works; it solves the right problem; handles errors; is simple and minimal; is tested; is documented; affords future change without over-engineering; meets the relevant "ilities"), and meeting that bar remains the human's responsibility.

The prescription is to spend the cheap-code surplus on *raising* quality — not normalizing slop. Two named uses: eliminate the class of technical debt that is "simple but time-consuming" (bad APIs, poor naming, oversized files) using async agents in worktrees; and run **exploratory prototypes** in parallel to make better technology choices before committing. See [[refactoring-with-agents]].

The human's job therefore moves up the stack. With typing no longer the bottleneck, the work becomes: deciding *what* code to write, equipping the agent with the right tools, specifying problems at the right level of detail, and verifying and iterating until the result is robust. Several emerging habits visible in the sources support this:

- **"Fire off a prompt anyway"** — when instinct says a side experiment isn't worth the time, run an async agent on it; the worst case is a few wasted tokens.
- **[[hoarding-working-examples|Hoard working examples]]** — keep a personal collection of runnable code that proves you know how to do specific things, and use it as an input to future agent prompts (via `curl`, local filesystem search, or `git clone` to `/tmp`). The key payoff: you only ever need to figure out a trick once.
- **[[compound-engineering|Compound engineering]]** (Shipper & Klaassen / Every) — end every agent-assisted project with a retrospective whose output is updated instructions for future agent runs. Hoarding accumulates *artifacts*; compound engineering accumulates *instructions*. Both turn one-time effort into permanent leverage.
- **[[agent-code-review|Own the review]]** — async refactor work does not mean async human responsibility. A good agentic PR comes with confidence the code works, small reviewable scope, higher-level context, and a PR description you actually read. Filing unreviewed agent code on collaborators is the first named anti-pattern.
- **[[git-with-agents|Use Git ambitiously]]** — coding agents are fluent in Git's full surface (basic *and* advanced). The human's job shifts from remembering recipes to staying aware of what's possible. The "review changes made today" prompt cheaply seeds a fresh session; "sort out this git mess for me" handles formerly painful merge/cherry-pick states; `git bisect` upgrades from occasional-use to routine because agents handle the test-condition boilerplate.
- **[[subagents|Dispatch subagents to preserve context]]** — context windows are a hard constraint (good results typically below ~200K tokens even when limits are ~1M). Subagents are the architectural response: dispatch a fresh copy of the agent with its own context for exploration (Claude Code's `Explore`), parallel file edits (often on cheaper models like Haiku), or specialist roles (code reviewer, test runner, debugger). Cautionary: don't over-fragment — the value is context preservation, not maximalist orchestration.
- **[[verifiability|Ask whether you're on the model's rails]]** — Karpathy's analytic frame: traditional software automates what you can *specify*; LLMs automate what you can *verify*. Verifiable, heavily-trained tasks (coding, math, games) are where models fly; outside those circuits they fail in "bizarrely basic ways" (the jagged-intelligence corollary). Scope projects accordingly.
- **[[agent-native-infrastructure|Build for the agent, not just the human]]** — most software is still designed for humans clicking screens. Karpathy's frame: the world has to be rewritten with **sensors** (turn world-state into digital info) and **actuators** (let agents change things), exposed through markdown docs, CLIs, APIs, MCP servers, structured logs, copy-pasteable instructions. The MenuGen deployment story is the running benchmark for how mature the infrastructure layer is.

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
- [[2026-05-23-ai-should-help-us-produce-better-code]]
- [[2026-05-23-anti-patterns-things-to-avoid]]
- [[2026-05-23-how-coding-agents-work]]
- [[2026-05-23-using-git-with-coding-agents]]
- [[2026-05-23-subagents]]
- [[2026-04-30-sequoia-ascent-karpathy]]
