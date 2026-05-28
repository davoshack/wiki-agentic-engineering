---
type: topic
tags: [agentic-engineering, multi-agent, swarms, control-plane, langgraph, langsmith, langmem, mcp, a2a, observability, enterprise, team-scale]
created: 2026-05-26
updated: 2026-05-28
status: developing
sources: 2
---

# Multi-agent coordination

A **control-plane architecture** in which multiple AI agents — each with a defined
role, shared memory, and a common observability layer — coordinate to move software
through the *full* delivery pipeline. The unit of automation is not an individual
developer with a [[coding-agents|coding agent]] but a **swarm of role-differentiated
agents** mirroring an engineering team. The Worker/Leader pattern, the A2A and MCP
protocols, and the LangGraph/LangSmith/LangMem substrate are the load-bearing pieces.

This topic is also where the wiki carries the **second definition of "agentic
engineering"** — the one used by [[kumar-ramagopal]] in
[[2026-05-26-agentic-engineering-swarms]] — alongside the
[[agentic-engineering|practitioner-discipline definition]] from Willison and Karpathy.
The two are *complementary, not competing* (coding agents are components inside Worker
Agents) but the term itself now has two non-identical referents in the field.
[[practitioner-discipline-vs-control-plane]] is the cross-cutting synthesis.

## Synthesis

### The core thesis

The thesis from [[2026-05-26-agentic-engineering-swarms]]:

> The biggest step change doesn't come from better tools alone. It comes from systems
> that mirror real-world teams.

Kumar & Ramagopal's claim is that the limiting factor in software delivery is *not*
how fast any single engineer (or any single agent) can produce code — it's how
*coordination overhead*, cross-team latency, context handoff, and downstream
verification consume the cycle. The remedy is to model the whole delivery pipeline as
a coordinated set of agent roles, not as a series of code-generation prompts.

The system this maps to is *"not a better coding AI" / "not a better task assistant."*
It is a **control plane** that orchestrates cross-team workflows, maintains long-term
memory across agents, and manages state and traceability across the full SDLC.

### The Worker / Leader pattern

The architecture is a loosely-coupled system of agents with two complementary roles.

**Worker Agents** are *"digital counterparts to individual contributors on an
engineering team."* Each Worker:

- Interprets user intent and translates it into an executable plan via a reasoning
  model.
- Gathers required context from systems of record (source repos, issue trackers,
  internal knowledge bases, logs) via MCP-style tool gateways.
- Executes workflows through tools, [[coding-agents|coding agents]], or sub-agents.
- Validates outcomes.
- Reports plans, actions, and results upward for transparency, accountability, and
  traceability.

Workers are *intentionally loosely coupled* so they scale horizontally, adapt to new
workflows, and can delegate to other Workers in the swarm.

A **Leader Agent** is *"the digital analogue of a project leader."* It provides:

- A shared **prompt and workflow library** that standardizes best practices and lowers
  onboarding friction.
- A common **tool gateway** that exposes approved capabilities to Workers in a
  consistent, secure manner.
- **Long-term memory** for the swarm, enabling learning and continuous improvement.
- **Global observability** into agent activity, decisions, and outcomes.
- **Orchestration** — *"when and how agents act, not just what they produce."*

The design property the authors highlight: *"By separating execution from coordination,
the framework preserves autonomy at the edges while maintaining coherence at scale."*
This is the same shape as well-functioning human engineering organizations.

### The four-stage Worker loop

Each Worker Agent runs a logical four-stage progression *"applicable to most agentic
workflows"*:

1. **Intent Analysis** — the engineer's natural-language intent (from an IDE, CLI,
   GitHub action, or Jira trigger) is sent to a Worker. LangGraph orchestrates intent
   parsing and MCP-tool context retrieval.
2. **Planning + Notification** — the Worker produces a structured multi-step plan and
   notifies engineers via Slack / Teams / Webex. Visibility is built in by default;
   plans are not just submitted to the system, they are surfaced to the team.
3. **Execution + Tracking** — steps are executed one at a time, in collaboration with
   an IDE-resident AI coding agent. State is checkpointed via LangGraph so the workflow
   can recover, retry, or audit.
4. **Validation + Closure** — the Worker confirms the executed plan matches the
   checkpointed state, persists the result in LangMem, and notifies the channel.

This is structurally similar to a senior engineer working a ticket — read intent, plan,
execute with peer review, close — but compressed and made auditable by default.

### Protocols: A2A and MCP

Two protocols carry the system's traffic.

- **A2A (Agent-to-Agent)** is the native communication protocol between Worker Agents
  in the swarm.
- **MCP (Model Context Protocol)** is used as an adapter layer for agents and systems
  that don't speak A2A. The pilot wrapped an IDE-resident AI coding agent in an MCP
  adapter so the rest of the system stays IDE-agnostic.

This pairing is the team-scale instance of the [[agent-native-infrastructure]] thesis:
sensors and actuators standardized enough that arbitrary agents and systems can be
composed without bespoke integrations.

### Why LangChain's stack

[[kumar-ramagopal]] evaluated several frameworks before selecting LangGraph + LangSmith
+ LangMem against five production criteria:

| Requirement | What it solves |
| --- | --- |
| State management + checkpointing across steps, agents, retries | Resumability and recoverability |
| Audit trails (*"who decided what, when, and why"*) | Post-hoc analysis, compliance |
| Interface compatibility with systems of record + MCP gateways | Real integration surface |
| Deterministic execution to enforce authorized actions | Operational risk control |
| Interoperability across protocols / frameworks | Avoids lock-in |

- **LangGraph** — graph of stateful nodes; the substrate for the four-stage worker
  loop and any custom workflows.
- **LangSmith** — observability and evals; the global telemetry the Leader Agent
  exposes.
- **LangMem** — long-term memory; the substrate for *swarm-level* learning and
  workflow-indexing/reuse.

These choices reflect a different optimization target from the practitioner-side
literature: not *"how do I get my coding agent to do a good job?"* but *"how do I
operate a fleet of agents safely and observably?"*

### Pilot results from Cisco

Concrete quant findings (the wiki's first heavily-numerical source):

- **Debugging.** 20+ cross-team triage / root-cause workflows. **93% reduction in
  time-to-root-cause** vs historical baselines. Several investigations completed in
  under five minutes of coordinated agent execution. Independent QE assessment found no
  measurable quality loss. From **512 sessions / 70 users / one month**, the authors
  computed **200+ engineering hours saved**.
- **Development.** 15+ workflows pairing an IDE coding agent with a Worker Agent.
  **65% reduction in execution time** vs historical baselines, with worker overhead
  included.
- **Where the gain actually came from.** *"The primary gains were not limited to
  faster code generation — which AI coding agents already perform well — but from
  compressing downstream workflows for functional testing after PR merge through
  coordinated agent execution."* Code-gen was already fast; the cycle was bottlenecked
  on what happened around it.

The numbers should be read with caveats: a single enterprise, internal-baseline
methodology, "reported conservatively," no external replication yet. They are
nevertheless the most concrete delivery-cycle numbers in the wiki so far.

### The PR-review bottleneck — a team-scale corollary

A striking observation: *"PR review process itself became the bottleneck introduced by
human-in-the-loop."* When the surrounding work compresses, the human gating step is
exposed as the binding constraint.

This is the team-scale corollary of [[agent-code-review]]: the human-owned review is
the *trust gate* that keeps unreviewed agent code off colleagues' plates, *and* the
*rate limiter* once the rest of the system gets fast. Both things at once. The
implication is not that the gate should be removed — Willison's anti-pattern still
stands — but that the gate's design (what it actually checks, what evidence it
demands, who performs it, in what window) is now where further compression has to come
from. Open question for the wiki.

### How this composes with the rest of the field

- **[[coding-agents]] are components, not the whole stack.** *"Codex-class models are
  often embedded within Worker Agents or as a component in the workflow as reasoning
  or code-generation engines."* The Willison/Karpathy subject is a primitive *inside*
  the Worker Agent. The two layers compose: a coding agent does the local
  intent-to-code translation; the Worker plans, gathers context, validates, and
  reports; the Leader orchestrates across Workers and teams.
- **[[subagents]] vs. swarms — same word, different unit.** Willison's parallel
  subagents are fresh copies of the same coding agent dispatched by a parent within a
  *single user-driven session* — context-preservation devices. Kumar & Ramagopal's
  swarm of Worker Agents is **persistent, role-differentiated, multi-session**, and
  coordinated by a Leader Agent across team boundaries. The two are not in conflict;
  they sit at different scales of organization.
- **[[compound-engineering]] and LangMem.** Compound engineering accumulates
  *instructions* in a personal/repo harness across sessions; LangMem accumulates
  *workflow indices and long-term state* shared across a swarm. The motion is the
  same — transient signal becomes durable instruction — at a different organizational
  level.
- **[[agent-native-infrastructure]] gets concrete substrate.** Karpathy's sensors and
  actuators thesis predicted standardized agent ↔ agent and agent ↔ system protocols;
  A2A and MCP are the protocols this source actually operates on. The MCP entry on the
  agent-native surface inventory gets a second source.
- **[[agentic-testing]] and post-PR testing.** *"Compressing downstream workflows for
  functional testing after PR merge"* is the new headline use case for agentic
  testing at team scale: the suite the human used to babysit between merge and deploy
  is now the surface area for the next round of compression.
- **[[verifiability]] still applies but moves up a level.** At single-agent scale the
  verifier is the test suite; at swarm scale additional verifiers (Validation +
  Closure stage, LangSmith evals, the Leader's observability layer) are needed because
  the chain of action is longer.

## Open questions

- **What does the PR-review gate look like once it's the constraint?** Sub-questions
  the wiki should track: which checks remain human-only and which can move to a
  reviewer agent; whether the "evidence of work done" artifacts from [[agentic-testing]]
  (Showboat documents, manual-test notes) shorten the human's review time enough to
  matter; what a two-tier (agent-review → human-spot-check) gate would look like in
  practice.
- **Generalization beyond Cisco.** The pilot numbers are striking but come from a
  single enterprise with its own bootcamp-curated baseline. No replication yet from
  other organizations. What's the open-source / non-enterprise analog?
- **Leader Agent design.** The post characterizes the Leader's responsibilities at a
  high level but doesn't show the actual prompts, the orchestration policy, or how
  Leaders themselves are evaluated. How is *the orchestrator* itself debugged when it
  makes a bad routing decision?
- **A2A protocol maturity.** A2A is named as the native inter-agent protocol but the
  post doesn't compare it to alternatives (or specify which A2A — the field has more
  than one). What's the actual standardization landscape?
- **Failure modes and safety.** Swarm-of-agents systems have a different failure
  surface from single coding-agent sessions (cascade failures, unauthorized actions,
  inter-agent prompt injection). The post mentions deterministic execution and
  authorized actions but doesn't go deep. What does *safe envelope at swarm scale*
  look like?
- **Where does Leader<-->Leader coordination break?** Cross-team orchestration through
  Leader Agents is described as a clean recursion of the within-team pattern. In a
  real organization the bottleneck is usually political (priorities, accountability,
  ownership) not technical. How much of this can a Leader Agent surface or shortcut?
- **Coding-agent-as-component composition.** When a Worker Agent uses a coding agent
  internally, who owns context for the coding agent's session? Does
  [[hoarding-working-examples]] still work the same way when the *human* isn't the
  one prompting?
- **Vocabulary.** The field now has two non-identical uses of *"agentic engineering"*
  in circulation simultaneously. Does this split stabilize, or will the term collapse
  back to one meaning? Watching the next sources for signal.

## Sources

- [[2026-05-26-agentic-engineering-swarms]]
