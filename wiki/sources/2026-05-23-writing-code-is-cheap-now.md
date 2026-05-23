---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/code-is-cheap/
source_date: 2026-05-23
tags: [agentic-engineering, economics, habits, good-code]
created: 2026-05-23
updated: 2026-05-23
status: developing
---

# Writing code is cheap now

The second chapter of *Agentic Engineering Patterns*. Argues that coding agents have collapsed the cost of producing code to near-zero, which invalidates a large set of engineering intuitions — both macro (planning, estimating, scoping) and micro (whether to refactor, test, document) — that were built around code being expensive. But *good* code is still expensive, and the chapter enumerates what "good" means.

## Key takeaways

- Thesis: *"The biggest challenge in adopting agentic engineering practices is getting comfortable with the consequences of the fact that writing code is cheap now."*
- Historically, "a few hundred lines of clean, tested code" took most developers a full day or more. Engineering habits at every level were built around that constraint.
- **Macro-level habits built on expensive code**: heavy upfront design, estimating, planning. Product features were evaluated as needing to *earn* their development cost many times over.
- **Micro-level habits built on expensive code**: hundreds of daily tradeoffs — "is this refactor worth an extra hour?", "is this test worth writing?", "can I justify a debug interface?" Coding agents disrupt most of these intuitions.
- **Parallel agents** compound the disruption: one human can now have agents implementing, refactoring, testing, and documenting in multiple places simultaneously, making the old intuitions even less reliable.
- *Cheap code* and *good code* are not the same thing. Delivering new code is now nearly free; delivering **good code** remains significantly more expensive.
- Willison's working definition of **good code** has 9 elements:
  1. The code works (does what it's meant to, without bugs).
  2. We *know* it works (we've confirmed it for ourselves and others).
  3. It solves the right problem.
  4. It handles error cases gracefully and predictably — errors carry enough info for future maintainers.
  5. It's simple and minimal — only what's needed, understandable by humans and machines now and later.
  6. It's protected by tests, both for now and as a regression suite.
  7. It's documented at an appropriate level, and the documentation stays in sync as behavior changes.
  8. The design affords future changes without over-engineering — [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it) still applies, but don't make future change much harder than it needs to be.
  9. The relevant "ilities" — accessibility, testability, reliability, security, maintainability, observability, scalability, usability.
- Coding agents help with most of this, but the developer driving the agents remains responsible for ensuring the output meets the project's particular subset of "good."
- Best practices for agent-era engineering are still being figured out across the industry, including by Willison himself.
- Practical heuristic he offers: *any time your instinct says "don't build that, it's not worth the time," fire off a prompt anyway* in an asynchronous agent session. The downside is just some wasted tokens.

## Connections

- Direct continuation of [[2026-05-23-what-is-agentic-engineering]] — that chapter defined the practice; this one explains the economic shift that makes the practice consequential.
- The cost-collapse thesis and the "good code" decomposition are the substance of [[economics-of-code]].
- The "fire off a prompt anyway" heuristic is itself a habit — connects to [[hoarding-working-examples]] (because the cheap experiment, if it works, becomes a hoardable artifact).
- The point that coding agents *can* learn (raised in chapter 1) plus the point that good code requires verification (this chapter) together motivate building feedback loops into the agent harness.
- Author: [[simon-willison]].

## Raw file

`raw/Writing code is cheap now - Agentic Engineering Patterns.md`
