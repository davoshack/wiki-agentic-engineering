---
type: synthesis
tags: [meta, agentic-engineering, comparison, definitions, multi-agent, enterprise]
created: 2026-05-26
updated: 2026-05-26
status: developing
sources: 11
---

# Practitioner discipline vs. control plane: two senses of "agentic engineering"

The wiki now carries two **non-identical definitions of *agentic engineering*** drawn
from different sources, written for different audiences, and pointed at different
units of organization. They are not opposed — they compose cleanly — but they are
genuinely different. This synthesis names the split, shows how the two senses fit
together, and tracks where the field's vocabulary may go.

## The two senses, side by side

| | Practitioner discipline | Control plane |
| --- | --- | --- |
| **Canonical sources** | [[2026-05-23-what-is-agentic-engineering\|Willison Ch.1]], [[2026-04-30-sequoia-ascent-karpathy\|Karpathy at Sequoia Ascent 2026]] | [[2026-05-26-agentic-engineering-swarms\|Kumar & Ramagopal (LangChain blog, 2026-04-17)]] |
| **Core definition** | *"The practice of developing software with the assistance of [[coding-agents\|coding agents]]"* (Willison). *"The professional discipline of coordinating fallible agents while preserving correctness, security, taste, maintainability"* (Karpathy). | *"A multi-agent coordination model where AI agents act as digital team members — each with defined roles, shared memory, and a common observability layer — to move software through the full delivery pipeline, not just generate code faster."* |
| **Unit of organization** | The human + a coding agent in a session (sync or async). | A **swarm of role-differentiated agents** + a Leader Agent, supervised by humans. |
| **Author vantage** | Solo developer / small team; AI-positive practitioner. | Enterprise (Cisco); cross-team operating model. |
| **Primary concern** | Quality, taste, correctness, verification, maintainability of *what one human + agent produce*. | Coordination, observability, audit, traceability of *what a fleet of agents produce across team boundaries*. |
| **Substrate** | Claude Code / Codex / Gemini CLI; Git; tests; system prompts; CLAUDE.md / AGENTS.md. | LangGraph + LangSmith + LangMem; A2A protocol; MCP gateways. |
| **What "good" looks like** | Willison's [[economics-of-code\|9-point good-code checklist]]; small reviewable PRs; tests pass; evidence of work done. | Plan / execution / validation auditable; **93% debug time reduction**, **65% dev time reduction**, no QE-measured quality loss. |
| **Where the bottleneck is** | Human attention, taste, judgment; review; verification. | Cross-team coordination; downstream testing post-PR-merge; *"PR review process itself became the bottleneck introduced by human-in-the-loop."* |

## They compose, they don't compete

The most important relationship is that the two senses **stack**, not collide.

> *"Codex-class models are often embedded within Worker Agents or as a component in
> the workflow as reasoning or code-generation engines."*
> — [[2026-05-26-agentic-engineering-swarms]]

Within a Worker Agent, the practitioner-discipline sense is still load-bearing:
*something* still has to translate intent into code, run tests, write good PR
descriptions, hoard working examples, use Git ambitiously. That something is a
[[coding-agents|coding agent]], operated under (some flavor of) the
Willison/Karpathy discipline. The control plane around the Worker doesn't replace any
of that; it *industrialises* it — adds checkpointing, audit trails, cross-team routing,
long-term memory, observability.

A useful way to hold them:

- **Practitioner discipline = micro / per-session / per-developer.** What a single
  human and coding agent should do, turn-by-turn, to produce good code.
- **Control plane = macro / per-workflow / per-team.** What the system around those
  sessions should provide so that work moves cleanly across people, teams, and time.

The same person could be doing both at once — running Claude Code with red/green TDD
(practitioner) inside an IDE that's wrapped in an MCP adapter and routed by a Leader
Agent (control plane).

## What each sense gets right that the other under-specifies

### What the practitioner-discipline sense gets right
- The **per-turn** mechanics: prompts, tools, context, verification.
- The **9-point good-code** standard and how the human is still on the hook for it.
- Why the work is the way it is: [[verifiability]], jagged intelligence,
  [[software-3-0]], [[agent-architecture|ghosts-not-animals]].
- The cheap-code surplus and where to spend it.
- The **anti-patterns** at the individual contributor level (unreviewed PRs, etc.).

What the practitioner-discipline sense leaves under-specified: how this scales when
there are *many* humans and *many* agents acting in parallel across an organization;
how cross-team handoff actually works; what the audit and compliance story looks like.
[[willison-vs-karpathy|The Willison/Karpathy synthesis]] explicitly flagged this as
the shared blind spot.

### What the control-plane sense gets right
- The **macro shape** of an enterprise system of agents: roles, coordination, memory,
  observability.
- Concrete **operational requirements** (state mgmt + checkpointing, audit trails,
  authorized actions, interoperability).
- Empirical **delivery-cycle numbers** in production.
- The team-scale **bottleneck observation**: code-gen is fast; what's slow is the
  work *around* it.

What the control-plane sense leaves under-specified: what the Worker Agents actually
do per-turn (it leans on AI coding agents inside Workers and doesn't reopen the
practitioner-discipline questions); whether the architecture ports beyond LangChain or
beyond Cisco; what *safety at swarm scale* looks like; how the Leader Agent is itself
debugged when it routes badly.

## Where the bottleneck sits under each frame

Under the **practitioner-discipline** frame, the bottleneck is the human's review
attention. [[agent-code-review]] is built around making the human's review pass
trustworthy, which is also necessarily a serial, careful, cognitively expensive step.

Under the **control-plane** frame, Kumar & Ramagopal report that *"PR review process
itself became the bottleneck introduced by human-in-the-loop"* once the rest of the
delivery cycle was compressed. The trust gate becomes the rate limiter.

Both are *true at the same time* and they point at the same engineering object. The
question they raise jointly is interesting: **what does a PR-review gate look like
when it has to remain trustworthy and stop being slow?** This is one of the wiki's
better current open questions. Subquestions:

- Which checks must remain human-only (judgment, taste, security gates) and which can
  move to a reviewer agent?
- Do the *evidence-of-work-done* artifacts from [[agentic-testing]] (Showboat
  documents, manual-test notes, "exec" command outputs) shorten the human's review
  time enough to matter?
- Could a **two-tier** gate work — automated reviewer agent does the surface pass,
  human does a much smaller spot-check?

## Vocabulary, briefly

The word *"agentic engineering"* now has two non-identical referents in the field. The
wiki's policy (per the schema's contradiction rule) is to **carry both** in
[[agentic-engineering]] (area) and in the topic pages, and to let context disambiguate.
Quick rules of thumb the wiki uses:

- If the context is *what one human + agent should do*, the **practitioner-discipline**
  sense is operative.
- If the context is *how a team or organization runs many agents*, the **control-plane**
  sense is operative.
- The substrate is a strong cue: Claude Code / Codex / Gemini CLI / Git → practitioner;
  LangGraph / LangSmith / LangMem / A2A / Worker / Leader → control plane.

Whether the field settles on one meaning or keeps both is a question worth watching.
This synthesis page will be revised when a third or fourth source either reinforces
the split or collapses it.

## Sources

- [[2026-05-26-agentic-engineering-swarms]]
- [[2026-05-23-what-is-agentic-engineering]]
- [[2026-05-23-writing-code-is-cheap-now]]
- [[2026-05-23-hoard-things-you-know-how-to-do]]
- [[2026-05-23-ai-should-help-us-produce-better-code]]
- [[2026-05-23-anti-patterns-things-to-avoid]]
- [[2026-05-23-how-coding-agents-work]]
- [[2026-05-23-using-git-with-coding-agents]]
- [[2026-05-23-subagents]]
- [[2026-04-30-sequoia-ascent-karpathy]]
- (Testing trio [[2026-05-26-first-run-the-tests]] / [[2026-05-26-red-green-tdd]] / [[2026-05-26-agentic-manual-testing]] are also referenced where the PR-review and verification arguments use them.)
