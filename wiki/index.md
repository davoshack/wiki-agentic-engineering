---
type: index
updated: 2026-05-26
---

# Index

The catalog of every page in this wiki. The LLM updates this on every ingest. To answer a
question, read this first to find relevant pages, then drill into them.

## Overview

- [[overview]] — the evolving big-picture synthesis of what the wiki knows so far.

## Areas

- [[agentic-engineering]] — the practice of developing software with the help of coding agents; the standing domain the wiki is built around.

## Topics

### Foundations

- [[coding-agents]] — what an agent is (tools in a loop), why code execution is the defining capability, sync vs. async flavors, vibe-coding vs. agentic-engineering (Karpathy's canonical floor/ceiling framing).
- [[agent-architecture]] — how a coding agent is actually built: LLM + system prompt + tools in a loop. Tokens, context windows, token caching, the tool-call protocol, reasoning mode, ghosts-not-animals mental model.
- [[software-3-0]] — Karpathy's paradigm progression (1.0 explicit code → 2.0 learned weights → 3.0 LLM-as-interpreter, context-window-as-program). Some apps should disappear into direct model transformations.

### Economics and analytic frames

- [[economics-of-code]] — the cost of producing code has collapsed; the cost of producing *good* code (9-dimension checklist) has not; old engineering intuitions are due for an overhaul; spend the surplus on quality. Token-cost layer and the verifiability-of-coding explanation included.
- [[verifiability]] — Karpathy's analytic frame: LLMs automate what you can verify. Jagged intelligence as a corollary; capability spikes where labs train heavily on verifiable RL.

### Practices

- [[hoarding-working-examples]] — keep a personal collection of runnable code that proves what you know how to do, and recombine those examples in agent prompts. Karpathy's `microGPT` and the LLM Wiki Pattern as canonical distilled artifacts.
- [[refactoring-with-agents]] — use async coding agents to eliminate the "simple but time-consuming" class of technical debt; worktree workflow, PR evaluation, zero-tolerance for code smells.
- [[git-with-agents]] — Git is a key tool for agent workflows; agents are fluent in basic and advanced Git, which lets the human be more ambitious. Prompt vocabulary, the "sort out this git mess" pattern, bisect, and history rewriting as editorial work.
- [[subagents]] — dispatching a fresh copy of the agent with a new context window. Three flavors: exploratory (Claude Code's `Explore`), parallel (often on cheaper models like Haiku), specialist (code reviewer, test runner, debugger).
- [[compound-engineering]] — end each project with a retrospective whose output is updated agent instructions (system prompt, harness, repo-level instruction files); quality compounds across runs. Karpathy's compact recipe (define context / tools / feedback loop / guardrails; let agents work; preserve understanding) is the target shape.
- [[agent-code-review]] — the human owns the first review pass on agent-generated code; characteristics of a good agentic PR; evidence-of-work-done signals.
- [[agentic-testing]] — testing as the verification layer: `First run the tests` to seed sessions, `Use red/green TDD` for new code, manual testing (`python -c`, `curl`, Playwright/Rodney) for what the suite misses; manual findings feed back into the suite via red/green so verification compounds. Short prompts as compressed software-engineering discipline.

### World-side

- [[agent-native-infrastructure]] — when the user is an agent acting for a human, products need sensors and actuators: markdown docs, CLIs, APIs, MCP servers, structured logs, copy-pasteable instructions, safe permissioning, headless setup flows. MenuGen deployment as the running benchmark.

## People

- [[simon-willison]] — author of *Agentic Engineering Patterns*; practitioner-oriented, definitionally disciplined, frames many patterns as extensions of pre-LLM craft.
- [[andrej-karpathy]] — co-founder of OpenAI; Tesla Autopilot; Eureka Labs. Paradigm-namer (Software 1.0/2.0/3.0; vibe coding; agentic engineering; verifiability; jagged intelligence; ghosts not animals). Originator of the LLM Wiki Pattern that inspired this wiki.

## Syntheses

- [[willison-vs-karpathy]] — the wiki's first cross-author synthesis. Willison gives practices and operational discipline; Karpathy gives paradigms and analytic frames. Where they overlap, where they diverge, what's still missing from both.
- [[ghosts-and-the-bitter-lesson]] — anti-anthropomorphism at two stages: Sutton (don't encode your cognition intuitions into the *training*) and Karpathy (don't project your cognition intuitions onto the *resulting system*). The ghost is the artifact of taking Sutton seriously; jagged intelligence is the corollary of "scales with computation." Sutton not yet ingested.

## Sources

- [[2026-04-30-sequoia-ascent-karpathy]] — Andrej Karpathy in conversation with Stephanie Zhan, Sequoia Ascent 2026. Software 3.0, verifiability, jagged intelligence, vibe coding vs. agentic engineering, ghosts not animals, agent-native infrastructure, MenuGen examples.
- [[2026-05-23-what-is-agentic-engineering]] — Simon Willison, *Agentic Engineering Patterns* Ch. 1. Defines agentic engineering, agent, and coding agent; positions against vibe coding.
- [[2026-05-23-writing-code-is-cheap-now]] — Simon Willison, *Agentic Engineering Patterns* Ch. 2. The cost of code has dropped; the cost of *good* code hasn't; lists 9 dimensions of good code.
- [[2026-05-23-hoard-things-you-know-how-to-do]] — Simon Willison, *Agentic Engineering Patterns* Ch. 3. Hoard working examples; recombine them in agent prompts (worked OCR-PDF example).
- [[2026-05-23-ai-should-help-us-produce-better-code]] — Simon Willison, *Agentic Engineering Patterns* Ch. 4. Spend the cheap-code surplus on quality: async refactoring, exploratory prototyping, compound engineering.
- [[2026-05-23-anti-patterns-things-to-avoid]] — Simon Willison, *Agentic Engineering Patterns* Ch. 5. First anti-pattern: filing PRs with unreviewed agent code. Checklist for a good agentic PR.
- [[2026-05-23-how-coding-agents-work]] — Simon Willison, *Agentic Engineering Patterns* Ch. 6. Technical deep-dive on the harness + LLM + tools loop, tokens, token caching, system prompts, reasoning.
- [[2026-05-23-using-git-with-coding-agents]] — Simon Willison, *Agentic Engineering Patterns* Ch. 7. Git is a key tool; core and advanced Git prompts; the "sort out this git mess" universal prompt; history rewriting as editorial work.
- [[2026-05-23-subagents]] — Simon Willison, *Agentic Engineering Patterns* Ch. 8. Subagents preserve root context; three flavors (exploratory, parallel, specialist); Claude Code's `Explore` walked through with a real transcript.
- [[2026-05-26-first-run-the-tests]] — Simon Willison, *Agentic Engineering Patterns*. The four-word session-seeder that forces the agent to discover the test harness and puts it in a testing mindset for the rest of the session.
- [[2026-05-26-red-green-tdd]] — Simon Willison, *Agentic Engineering Patterns*. Test-first development is a "fantastic fit" for agents; the red step (confirming tests fail before implementation) is load-bearing; `Use red/green TDD` is shorthand for the full discipline.
- [[2026-05-26-agentic-manual-testing]] — Simon Willison, *Agentic Engineering Patterns*. Code execution is the defining capability of a coding agent; manual testing patterns (`python -c`, `curl` exploration, Playwright / agent-browser / Rodney for web UIs); Showboat for capturing exec'd commands and outputs as "show your work" artifacts; manual findings feed back into the suite via red/green.
