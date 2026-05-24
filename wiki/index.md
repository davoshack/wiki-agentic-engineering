---
type: index
updated: 2026-05-23
---

# Index

The catalog of every page in this wiki. The LLM updates this on every ingest. To answer a
question, read this first to find relevant pages, then drill into them.

## Overview

- [[overview]] — the evolving big-picture synthesis of what the wiki knows so far.

## Areas

- [[agentic-engineering]] — the practice of developing software with the help of coding agents; the standing domain the wiki is built around.

## Topics

- [[coding-agents]] — what an agent is (tools in a loop), why code execution is the defining capability, sync vs. async flavors, and how this differs from vibe coding.
- [[agent-architecture]] — how a coding agent is actually built: LLM + system prompt + tools in a loop. Tokens, context windows, token caching, the tool-call protocol, reasoning mode.
- [[economics-of-code]] — the cost of producing code has collapsed; the cost of producing *good* code (9-dimension checklist) has not; old engineering intuitions are due for an overhaul; spend the surplus on quality. Now also covers the token-cost layer.
- [[hoarding-working-examples]] — keep a personal collection of runnable code that proves what you know how to do, and recombine those examples in agent prompts.
- [[refactoring-with-agents]] — use async coding agents to eliminate the "simple but time-consuming" class of technical debt; worktree workflow, PR evaluation, zero-tolerance for code smells.
- [[git-with-agents]] — Git is a key tool for agent workflows; agents are fluent in basic and advanced Git, which lets the human be more ambitious. Includes prompt vocabulary, the "sort out this git mess" pattern, bisect, and history rewriting as editorial work.
- [[subagents]] — dispatching a fresh copy of the agent with a new context window. Three flavors: exploratory (Claude Code's `Explore`), parallel (often on cheaper models like Haiku), specialist (code reviewer, test runner, debugger).
- [[compound-engineering]] — end each project with a retrospective whose output is updated agent instructions (system prompt, harness, repo-level instruction files); quality compounds across runs. (Term from Shipper & Klaassen at Every.)
- [[agent-code-review]] — the human owns the first review pass on agent-generated code; characteristics of a good agentic PR; evidence-of-work-done signals.

## People

- [[simon-willison]] — author of *Agentic Engineering Patterns*; practitioner-oriented, definitionally disciplined, frames many patterns as extensions of pre-LLM craft.

## Syntheses

*Cross-cutting analyses, comparisons, and query answers worth keeping. None yet.*

## Sources

- [[2026-05-23-what-is-agentic-engineering]] — Simon Willison, *Agentic Engineering Patterns* Ch. 1. Defines agentic engineering, agent, and coding agent; positions against vibe coding.
- [[2026-05-23-writing-code-is-cheap-now]] — Simon Willison, *Agentic Engineering Patterns* Ch. 2. The cost of code has dropped; the cost of *good* code hasn't; lists 9 dimensions of good code.
- [[2026-05-23-hoard-things-you-know-how-to-do]] — Simon Willison, *Agentic Engineering Patterns* Ch. 3. Hoard working examples; recombine them in agent prompts (worked OCR-PDF example).
- [[2026-05-23-ai-should-help-us-produce-better-code]] — Simon Willison, *Agentic Engineering Patterns* Ch. 4. Spend the cheap-code surplus on quality: async refactoring, exploratory prototyping, compound engineering.
- [[2026-05-23-anti-patterns-things-to-avoid]] — Simon Willison, *Agentic Engineering Patterns* Ch. 5. First anti-pattern: filing PRs with unreviewed agent code. Checklist for a good agentic PR.
- [[2026-05-23-how-coding-agents-work]] — Simon Willison, *Agentic Engineering Patterns* Ch. 6. Technical deep-dive on the harness + LLM + tools loop, tokens, token caching, system prompts, reasoning.
- [[2026-05-23-using-git-with-coding-agents]] — Simon Willison, *Agentic Engineering Patterns* Ch. 7. Git is a key tool; core and advanced Git prompts; the "sort out this git mess" universal prompt; history rewriting as editorial work.
- [[2026-05-23-subagents]] — Simon Willison, *Agentic Engineering Patterns* Ch. 8. Subagents preserve root context; three flavors (exploratory, parallel, specialist); Claude Code's `Explore` walked through with a real transcript.
