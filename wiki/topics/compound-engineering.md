---
type: topic
tags: [agentic-engineering, workflow, retrospectives, agent-instructions, system-prompts, long-term-memory]
created: 2026-05-23
updated: 2026-05-29
status: developing
sources: 7
---

# Compound engineering

The practice of ending every agent-assisted project with a retrospective that captures what worked and feeds it forward into instructions for future agent runs — so quality compounds over time instead of being re-discovered every session.

## Synthesis

Term originated by Dan Shipper and Kieran Klaassen at [Every](https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents), and adopted by [[simon-willison]] as the concrete workflow expression of an observation he had made earlier: LLMs don't learn from their past mistakes, but **coding agents can — provided the human deliberately updates the instructions and tool harness** based on what each round teaches (see [[coding-agents]]).

The loop is simple:

1. Run a coding project with an agent.
2. At the end, hold a **compound step** — a short retrospective on what worked, what failed, what surprised you.
3. Document those lessons in a form the agent will read on the next run (instructions files, `CLAUDE.md`-style harness notes, tool wrappers, evaluation prompts).
4. Future runs inherit those lessons. Quality improves project over project.

Willison's framing in [[2026-05-23-ai-should-help-us-produce-better-code]] places this inside a broader argument about quality: small improvements compound, and quality work that used to be "too time-consuming to justify" is now cheap. Compound engineering is the mechanism that turns each cheap improvement into a permanent capability.

This topic also connects to [[hoarding-working-examples]] from a different angle: hoarding is about accumulating *artifacts* (working code) for reuse; compound engineering is about accumulating *instructions* (how the agent should behave) for reuse. Both turn one-time effort into persistent leverage; they're complementary.

A third compounding loop sits at the suite level rather than the harness level. [[agentic-testing]] describes the *manual finding → red/green TDD → permanent regression test* motion: anything caught during manual testing is fixed by writing a failing test first, then implementing the fix. Each catch becomes durable verification the next agent run inherits. The same loop shape — *transient signal → durable instruction* — works at four granularities now:

1. **Test suite** (per-feature) — manual finding → red/green → permanent test.
2. **Repo instructions** (per-project) — session lesson → `CLAUDE.md` / `AGENTS.md` edit.
3. **System prompt** (per-user / per-role) — cross-project lessons → harness updates.
4. **Swarm memory** (per-organization) — [[multi-agent-coordination|LangMem]] indexes workflows so prior runs are retrievable by future Worker Agents across teams.

The fourth granularity comes from [[2026-05-26-agentic-engineering-swarms]] and is worth flagging as the **organization-scale analog** of compound engineering: where compound engineering accumulates *instructions* in an individual or team-level harness, LangMem accumulates *workflow indices, plans, and long-term state* shared across a swarm. Same motion, larger blast radius — and a different governance question (who owns and prunes the swarm's memory?). Reuse is the explicit goal: *"prior workflows to be indexed and reused. This significantly reduced onboarding overhead for repeat tasks."*

### "Every mistake becomes a rule" — compound engineering as a mindset

[[cole-medin]] ([[2026-05-29-cole-medin-harness-engineering]]) gives the same loop its sharpest practitioner statement and reframes it from a *practice* into a **mindset**. The pattern he names is the failure-attribution one: *"the agent does something dumb, the engineer blames the model, and the blame gets filed under 'wait for the next version.'"* The compounding mindset **rejects that** — because the failure is usually *legible*: agent broke a convention → add it to `agents.md`; agent ran a destructive command → add a hook that blocks it. **"Every mistake becomes a rule"** — *"an opportunity to improve your harness."*

Cole calls this **system evolution**, and locates it precisely in [[agent-harness-engineering|the AI layer's]] six components (rules, skills, hooks, …). It maps cleanly onto granularities 2–3 above (repo instructions and the system prompt / harness), and is the same *transient signal → durable instruction* shape — but stated as the thing that distinguishes a harness *engineer* from someone merely *using* a coding agent and waiting for the next model. It also answers a question [[agent-harness-engineering]] used to carry: the discipline is **compounded modification of a base**, not a literal new harness each time.

### Compound engineering ⊆ the software factory

A complementary frame from [[andy-dev-dan]] in [[2026-05-28-andy-dev-dan-five-pillars]]: the **[[software-factory]]** wraps planning, spec, build, test, and review into a single-prompt pipeline. Compound engineering is the *substrate-level* loop that improves the harness over time; the factory is the *workflow-level* loop that uses that harness to produce features. They stack — a mature factory is itself a compounded artifact, and each project's compound step can refine either the harness *or* the factory's pipeline steps. Andy's *"build the system that builds the system"* is the workflow-level expression of the same motion compound engineering applies at the instruction level.

### What "the instructions" actually are

The mechanics view from [[agent-architecture]] makes this concrete: the **system prompt** is the surface compound engineering writes to. System prompts in real coding agents are routinely hundreds of lines (Willison links the [Codex system prompt](https://github.com/openai/codex/blob/rust-v0.114.0/codex-rs/core/templates/model_instructions/gpt-5.2-codex_instructions_template.md) as a public example). When a "compound step" produces a lesson worth keeping, it lands either there, in repo-level instruction files (`CLAUDE.md`, `AGENTS.md`) that the harness loads into context, or in the **tool harness** itself — new tools, refined tool descriptions, or changed defaults. The same channel governs how [[subagents|specialist subagents]] are configured (their custom system prompts and tools are exactly this kind of compounded knowledge applied at a per-role granularity).

### The recipe Karpathy compounds toward

[[andrej-karpathy]]'s compact recipe in [[2026-04-30-sequoia-ascent-karpathy]] makes the *target* of compound engineering more explicit:

```
define the context
define the tools
define the feedback loop
define the guardrails
let agents work
preserve human understanding
```

A mature compounded harness is exactly an answer to the first four lines: what context the agent loads, what tools it can use, how it gets feedback ([[verifiability|verifiability and evals]]), and what guardrails prevent unsafe actions. Each compound step refines one or more of these. *"Preserve human understanding"* is the deliberately non-automatable last line — the reason retrospectives are still done by a human, not an agent.

The aspirational endpoint Karpathy gestures at: *"I should be able to say 'build MenuGen' and have the agent deploy the whole thing without manual clicking."* Reaching that point is a function of two compounding loops: the agent's own harness getting better via compound engineering, *and* the surrounding world becoming [[agent-native-infrastructure|agent-native]] so the actuators the harness needs actually exist.

## Open questions

- What does a good "compound step" actually look like in practice? Is it a checklist, free-form notes, structured prompt updates? The Every post would be worth ingesting directly.
- Where do the compounded lessons live — in repo-level instruction files (`CLAUDE.md`, `AGENTS.md`), in user-level dotfiles, in shared team docs, or in updated tool definitions? Probably some of each, but the boundaries matter.
- How do you avoid the instructions file growing into an unmanageable mess? Pruning and refactoring instructions is presumably its own discipline.
- How does compound engineering generalize across projects with different domains? Are some lessons universal (style, review process) and others project-local?

## Sources

- [[2026-05-23-ai-should-help-us-produce-better-code]]
- [[2026-05-23-how-coding-agents-work]]
- [[2026-04-30-sequoia-ascent-karpathy]]
- [[2026-05-26-agentic-manual-testing]]
- [[2026-05-26-agentic-engineering-swarms]]
- [[2026-05-28-andy-dev-dan-five-pillars]]
- [[2026-05-29-cole-medin-harness-engineering]]
