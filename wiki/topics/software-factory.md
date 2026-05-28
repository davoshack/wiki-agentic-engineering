---
type: topic
tags: [agentic-engineering, software-factory, ADWs, dark-factory, ZTE, workflow]
created: 2026-05-28
updated: 2026-05-28
status: developing
sources: 1
---

# Software factory

A repeatable system of **agents + code + workflow** that produces software outputs on-spec from a single prompt, rather than from per-feature human-in-the-loop sessions. Andy Dev Dan's term — also called the **dark factory** or **AI Developer Workflows (ADWs)** — and his most ambitious prescription: *"build factories, not features."*

## Synthesis

The thesis from [[2026-05-28-andy-dev-dan-five-pillars]]: you should stop being the engineer who *ships the feature* and become the engineer who *builds the system that ships features.* The unit of engineering work moves up a level — from writing code to designing the pipeline of agents and code that writes the code.

[[andy-dev-dan]]'s framing: ***"You write one prompt and your factory of agents and code work together to produce a massive result, to produce an entire feature, to produce an outcome."*** What's inside the factory:

- **Planning** — *"a plan is a prompt scaled."* Plan / spec prompts are how you teach the factory the formula for how engineering work gets done.
- **Plan review** — by another agent, or by you.
- **Scouting** — exploratory passes that surface the local context (cf. [[subagents]] § Claude Code's `Explore`).
- **Validation** — checks against the spec.
- **Build** — the actual implementation.
- **Test** — bound to [[agentic-testing]]'s `First run the tests` + red/green TDD discipline.
- **Review** — automated review passes (cf. [[agent-code-review]]); human review still required per Willison's anti-pattern.

The aspirational endpoint is **ZTE — Zero Touch Engineering**: prompt directly to production, no manual intervention. Andy explicitly flags this as *"super super advanced; that's where this all goes"* rather than the current target.

### How this relates to existing wiki patterns

The software-factory frame **subsumes and intensifies several existing topics**:

- **[[compound-engineering]]** accumulates *instructions* (system prompt + harness updates) across runs. The software factory goes further: it accumulates *whole pipelines* (planning + spec + build + test + review steps) that fire on a single prompt. Compound engineering is the *substrate-level* loop; the software factory is the *workflow-level* loop. They stack: a mature factory is itself a compounded artifact.
- **[[agent-harness-engineering]]** is a *component* of the factory — your specialized harness is one of the tools in the factory's toolbox.
- **[[multi-agent-coordination]]** (Kumar & Ramagopal at Cisco) describes a structurally similar org-scale system: Leader agents orchestrate Worker agents through a four-stage loop (intent → plan + notify → execute + checkpoint → validate + persist). The factory frame is the solo / small-team analog of the same shape. Where Kumar & Ramagopal sit on LangGraph + LangSmith + LangMem, Andy's solo factory sits on a custom-built composable harness.
- **[[refactoring-with-agents]]** is one *application* of the factory pattern. A refactor on a worktree, evaluated as a PR, is a small factory output. The factory generalizes that pattern to features, deployments, and beyond.
- **[[economics-of-code]]** explains *why* this is now economic: the per-task cost of agent work has collapsed, so investing in a system that produces many such outputs amortizes over many runs. The factory is what the cheap-code surplus is *spent on* at the workflow level.

### Where the framing pushes hardest

Andy frames the software factory as a **new SWE discipline alongside frontend, backend, full-stack, and DevOps** — *"a software engineering skill that takes practice."* The strongest version of his claim: by end of 2026, having a software factory for your production products will be a *requirement*, with the leverage going to engineers who internalized the factory mindset early.

This is a confident prediction. Worth holding alongside:

- *"Top 500 companies, everyone is building a software factory"* — unsourced claim. Some plausibly are (Kumar & Ramagopal's Cisco pilot is one concrete instance); whether *everyone* is is unverified.
- *"Output per unit of time goes parabolic"* — strong rhetoric; the [[economics-of-code|cost-shift]] story supports a step-change, but "parabolic" is closer to motivational language than measured throughput.
- The PR-review-as-bottleneck observation from [[2026-05-26-agentic-engineering-swarms|Kumar & Ramagopal]] is the empirically-grounded version of the same prediction — when the rest of the pipeline compresses, the human review gate becomes the rate limiter. The factory frame doesn't yet have a story for how that bottleneck releases.

### The factory and human responsibility

Andy doesn't dwell on it but the **factory does not dissolve human responsibility**, and the wiki's other voices are sharp on this:

- [[agent-code-review]]: the human owns the first review pass; filing unreviewed agent PRs on collaborators is the named anti-pattern.
- [[2026-05-23-anti-patterns-things-to-avoid|Willison]]: agents write convincing PR descriptions; you review those too.
- [[andrej-karpathy|Karpathy]]: *"preserve human understanding"* is the deliberately non-automatable last line of his recipe.

A factory is what you build *because* the human can no longer be in every loop — but the human still owns the *spec*, the *guardrails*, and the *review of the output*. ZTE (prompt → production) is interesting as a destination only if the spec and guardrails are mature enough to absorb the human's old role.

## Open questions

- What does a "good plan/spec prompt" actually look like in practice? Andy mentions it repeatedly without showing one. This is the obvious operational question.
- How do you *test* a factory itself (vs. just the outputs)? The factory has its own brittle points — bad spec prompts, drift in tool definitions, model swaps — and presumably needs its own test suite. None of the current sources address this.
- For a single engineer's factory vs. an organization's: is the factory pattern fundamentally fractal (same shape at every scale) or do qualitative differences emerge? Kumar & Ramagopal's substrate (LangGraph / LangSmith / LangMem) suggests org-scale needs explicit observability and memory infrastructure that solo factories can do without.
- When does building a factory pay off vs. just shipping the feature? Andy implies always; that's likely wrong for one-off work. What's the breakeven?
- What's the human's role in a near-ZTE factory? Andy says *"build the system that builds the system"* but stops short of describing the day-to-day work after the factory is mature. Plausibly: spec writing, factory maintenance, and review.

## Sources

- [[2026-05-28-andy-dev-dan-five-pillars]]
