---
type: topic
tags: [agentic-engineering, economics, habits, good-code]
created: 2026-05-23
updated: 2026-05-23
status: developing
sources: 2
---

# Economics of code

How the cost structure of producing software changes once coding agents make typing code nearly free — and which engineering habits, built around code being expensive, no longer hold.

## Synthesis

### The cost collapse

Code has historically been expensive. [[simon-willison]] points to a baseline: "a few hundred lines of clean, tested code takes most software developers a full day or more." Two layers of engineering practice grew up around that constraint:

- **Macro level** — heavy upfront design, estimation, and planning, all aimed at making expensive coding time efficient. Product features were evaluated against the cost of their development: a feature had to "earn its development costs many times over" to be worthwhile.
- **Micro level** — hundreds of daily tradeoffs predicated on time scarcity: *is this refactor worth an extra hour? is this test worth writing? can I justify a debug interface for this?* Most developers default-no on these all day.

Coding agents drop the cost of producing code to nearly zero. That disrupts *both* layers of intuition. Features that wouldn't have earned their old cost may be worth shipping now. Refactors, tests, docs, and debug tooling that previously failed the micro-tradeoff now often pass it. The intuitions themselves haven't been retrained yet.

**Parallel agents amplify the disruption.** One human can now have several agents implementing, refactoring, testing, and documenting different parts of a system at the same time, which moves the bottleneck further away from typing speed and makes the old serial-author intuitions even less reliable.

### Cheap code ≠ good code

The thesis isn't that good software is now free — it's that *delivering new code* is cheap and *delivering good code* is still significantly more expensive. Willison's working decomposition of **good code** (from [[2026-05-23-writing-code-is-cheap-now]]):

1. **It works** — does what it's meant to do, without bugs.
2. **We *know* it works** — confirmed for ourselves and others, not just assumed.
3. **It solves the right problem.**
4. **It handles errors gracefully and predictably** — errors carry enough information for future maintainers to understand what went wrong; it's not just the happy path.
5. **It's simple and minimal** — only what's needed, understandable by humans and machines now and in the future.
6. **It's protected by tests** — both proving current correctness and acting as a regression suite.
7. **It's documented at an appropriate level** — and the documentation stays in sync as behavior changes.
8. **The design affords future change** — [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it) still applies (don't anticipate hypothetical futures), but don't make future change much harder than it needs to be either.
9. **The relevant "ilities"** — accessibility, testability, reliability, security, maintainability, observability, scalability, usability — to the extent they apply to the class of software being built.

Coding agents can help with most of this, but the human driving them remains responsible for ensuring the output meets the *specific* subset of "good" that matters for the current project.

### New habits, partially formed

Willison is explicit that the new habits to replace the old intuitions are still being worked out across the industry — including by him. One concrete heuristic he offers: **"fire off a prompt anyway"** — any time the old instinct says *don't build that, it's not worth the time*, run it as an async agent session anyway. The downside is a few wasted tokens; the upside is sometimes a working prototype you wouldn't have had. This is the same mechanism that feeds the practice of [[hoarding-working-examples]] — cheap experiments become hoardable artifacts.

## Open questions

- Which old intuitions are *actually* wrong now, and which are still load-bearing? Default-yes on every refactor is presumably not the answer either.
- How do you reorganize estimation and planning when the variable cost of code is near zero but the cost of *good* code (testing, verification, design judgment) hasn't collapsed proportionally?
- What's the right human review and verification process for code an agent produced asynchronously in parallel — particularly when several agents touched related code?
- Which dimensions of "good code" do current agents do well unsupervised, and which still require the human to drive every time?

## Sources

- [[2026-05-23-writing-code-is-cheap-now]]
- [[2026-05-23-what-is-agentic-engineering]]
