---
type: topic
tags: [agentic-engineering, economics, habits, good-code, technical-debt, exploratory-prototyping, tokens, verifiability]
created: 2026-05-23
updated: 2026-05-26
status: developing
sources: 8
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

Coding agents can help with most of this, but the human driving them remains responsible for ensuring the output meets the *specific* subset of "good" that matters for the current project. Dimensions 1, 2, and 6 (*works*, *we know it works*, *protected by tests*) are the operational pressure that motivates [[agentic-testing]] — the practice of seeding sessions with the existing suite, building new code test-first, and supplementing with manual testing.

### New habits, partially formed

Willison is explicit that the new habits to replace the old intuitions are still being worked out across the industry — including by him. One concrete heuristic he offers: **"fire off a prompt anyway"** — any time the old instinct says *don't build that, it's not worth the time*, run it as an async agent session anyway. The downside is a few wasted tokens; the upside is sometimes a working prototype you wouldn't have had. This is the same mechanism that feeds the practice of [[hoarding-working-examples]] — cheap experiments become hoardable artifacts.

### Spending the surplus on quality, not noise

In [[2026-05-23-ai-should-help-us-produce-better-code]], Willison sharpens the prescription: the cheap-code surplus should be spent *raising quality*, not normalizing slop. Two concrete uses he names:

- **Eliminating "simple but time-consuming" technical debt.** A whole class of debt (bad API shapes that need many call-site changes, poor naming, duplicate-but-divergent functionality, oversized files) historically gets punted because it can't compete with urgent work for human time. Agents are ideal for it. *"The cost of these code improvements has dropped so low that we can afford a zero tolerance attitude to minor code smells and inconveniences."* The workflow lives in [[refactoring-with-agents]].
- **Exploratory prototyping for better technology choices.** Much technical debt originates upstream of any code — bad planning, missed options, picking the wrong tool. Coding agents make it cheap to *prove* a tech choice fits by wiring up a simulation and running a load test (Willison's worked example: "Is Redis a good choice for the activity feed on a site which expects thousands of concurrent users?"). Cheap enough to run **multiple experiments in parallel** and pick the winner — and the resulting prototype is then a hoardable artifact (see [[hoarding-working-examples]]).

LLMs also help by surfacing options the human didn't consider, and tend to suggest **[Boring Technology](https://boringtechnology.club/)** because it dominates their training data — which Willison frames as a feature: boring is usually what works.

The bigger payoff is the framing: small quality improvements **compound**. The mechanism for making them stick across agent runs is [[compound-engineering]] — end each project with a retrospective that updates the instructions future agents will read. *"Coding agents mean we can finally have both"* — quality *and* shipping.

### The token-cost layer

The cost story above is about *engineering time*. There is a second cost layer — **tokens** — that becomes visible once you look at the mechanics in [[agent-architecture]]. Providers charge per input *and* output token, and because LLMs are stateless, the full conversation history is replayed on every turn — so naive long sessions get expensive fast. Two design responses are now standard:

- **Token caching.** Providers charge a lower rate for token prefixes they've recently processed. Coding agents are deliberately built to avoid mutating earlier conversation content so the cache stays warm. This is why long sessions remain affordable.
- **Subagents.** Dispatching a fresh copy of the agent with a new context window keeps the parent's tokens free for the work that needs root context. Parallel subagents on cheaper/faster models (like Claude Haiku) trade root-context tokens for cheaper subagent tokens and serial latency for parallel latency. See [[subagents]] for the architectural pattern.

These optimizations matter because the [[economics-of-code|cheap-code surplus]] depends on the *per-task* cost staying low. Without caching and subagents, the cost of code would creep back up at scale.

### Why coding specifically — the verifiability layer

[[andrej-karpathy]] in [[2026-04-30-sequoia-ascent-karpathy]] adds an analytic frame that explains *why* coding agents work so dramatically better than ordinary LLM applications: **coding is verifiable.** Tests pass or fail; programs run or crash; diffs can be inspected; benchmarks can be measured. Verifiable tasks are practiceable in reinforcement learning, which is why frontier labs train coding heavily and capability progresses rapidly.

The implication for the cost story: the cheap-code surplus is partly a *consequence* of coding being on the model's rails. Tasks without an automatic success signal (Karpathy's "tasteful simplification" example — see his `microGPT` story) stay expensive in a different way: even with agents, the work doesn't compound through RL training. See [[verifiability]] for the full frame, including the **jagged intelligence** corollary that explains why models simultaneously refactor 100K-line codebases and tell you to walk to a 50m-away car wash.

The practical reading: when scoping a project, ask not only "is this work cheap with an agent?" but also "is this work verifiable enough that the model is *good* at it?" The two questions trade off when you push toward less-verifiable domains (UI taste, code aesthetics, novel system design).

### The return side — tokeconomics

This page describes the *cost* of agent work — engineering time, then token cost as the next layer. [[andy-dev-dan]] in [[2026-05-28-andy-dev-dan-five-pillars]] supplies a complementary *return* lens: a 3-level funnel that gates the decision to deploy agents always-on (AFK). Token-maxing (L1) → useful tokens (L2) → token arbitrage / revenue capture (L3). Always-on agents are appropriate *only* at L3; before that, an always-running agent is paying token-tax 24/7. See [[tokeconomics]] for the full framing, including the **token tax** as the recurring cost of missing agent-native surfaces (the economic case for [[agent-native-infrastructure]]).

## Open questions

- Which old intuitions are *actually* wrong now, and which are still load-bearing? Default-yes on every refactor is presumably not the answer either.
- How do you reorganize estimation and planning when the variable cost of code is near zero but the cost of *good* code (testing, verification, design judgment) hasn't collapsed proportionally?
- What's the right human review and verification process for code an agent produced asynchronously in parallel — particularly when several agents touched related code?
- Which dimensions of "good code" do current agents do well unsupervised, and which still require the human to drive every time?

## Sources

- [[2026-05-23-writing-code-is-cheap-now]]
- [[2026-05-23-what-is-agentic-engineering]]
- [[2026-05-23-ai-should-help-us-produce-better-code]]
- [[2026-05-23-how-coding-agents-work]]
- [[2026-05-23-subagents]]
- [[2026-04-30-sequoia-ascent-karpathy]]
- [[2026-05-26-first-run-the-tests]]
- [[2026-05-28-andy-dev-dan-five-pillars]]
