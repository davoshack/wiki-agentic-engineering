---
type: source
source_type: article
source_url: https://www.langchain.com/blog/agentic-engineering-redefining-software-engineering
source_date: 2026-04-17
tags: [agentic-engineering, multi-agent, swarms, enterprise, langgraph, langsmith, langmem, mcp, a2a, control-plane, observability, definitions]
created: 2026-05-26
updated: 2026-05-26
status: developing
---

# Agentic Engineering: How Swarms of AI Agents Are Redefining Software Engineering

A guest post on the LangChain blog (2026-04-17) by [[kumar-ramagopal|Renuka Kumar
(Cisco, Principal SWE / Director) and Prashanth Ramagopal (Cisco, Senior Director of
Engineering)]]. Reports on a Cisco-internal pilot of a **multi-agent coordination
framework** built on LangGraph + LangSmith + LangMem. The first **enterprise /
team-scale** source ingested into the wiki, and the first to use *"agentic
engineering"* in a sense **substantively different** from the Willison/Karpathy
practitioner discipline — see the Connections section for how the wiki handles the
definitional split.

## Key takeaways

- **A different definition of "agentic engineering."** For Kumar & Ramagopal, agentic
  engineering is *"a multi-agent coordination model where AI agents act as digital team
  members — each with defined roles, shared memory, and a common observability layer —
  to move software through the full delivery pipeline, not just generate code faster."*
  The system they describe is explicitly **"not a better coding AI" / "not a better task
  assistant."* It is a **control plane** that orchestrates cross-team workflows,
  maintains long-term memory, and manages state and traceability across the full SDLC.
  Compare with [[2026-05-23-what-is-agentic-engineering|Willison]] ("the practice of
  developing software with the assistance of coding agents") and
  [[2026-04-30-sequoia-ascent-karpathy|Karpathy]] ("the professional discipline of
  coordinating fallible agents while preserving correctness, security, taste,
  maintainability"). The Willison/Karpathy sense is *human + coding agent*; the
  Kumar/Ramagopal sense is *agents + agents, supervised by humans*.
- **AI coding agents are components, not the unit.** *"Codex-class models are often
  embedded within Worker Agents or as a component in the workflow as reasoning or
  code-generation engines."* This is a clean repositioning: the Willison/Karpathy subject
  is a primitive *inside* the system Kumar & Ramagopal describe. The two layers
  compose rather than compete.
- **Worker / Leader architecture.**
  - **Worker Agents** — *"digital counterparts to individual contributors on an
    engineering team."* Autonomous within well-defined boundaries; plan and execute
    tasks (development, testing, debugging, ops). A deployment may use a single worker
    or a *"dynamically coordinated swarm."*
  - **Leader Agent** — *"the digital analogue of a project leader."* Provides a shared
    prompt and workflow library, a common tool gateway, long-term memory for the swarm,
    global observability, and orchestration (*"when and how* agents act, not just
    *what* they produce"*).
  - Design property: *"By separating execution from coordination, the framework
    preserves autonomy at the edges while maintaining coherence at scale."*
- **Worker Agent capabilities** (the four-stage loop):
  1. **Intent Analysis** — interpret user intent via a reasoning model; gather context
     from systems of record (source repos, issue trackers, knowledge bases) via MCP
     tools.
  2. **Planning + Notification** — produce a structured multi-step plan; notify
     engineers via Slack / Teams / Webex.
  3. **Execution + Tracking** — execute one step at a time, in collaboration with the
     IDE-resident AI coding agent; track state via LangGraph checkpointing.
  4. **Validation + Closure** — confirm the executed plan matches the checkpointed
     state; persist results in LangMem; notify engineers.
- **Protocols.** Worker Agents communicate **agent-to-agent via the A2A protocol**.
  Agents that don't speak A2A are wrapped via an **MCP adapter**, which keeps the
  system IDE-agnostic.
- **Framework choices.**
  - **LangGraph** — graph of stateful nodes; controllable agent orchestration;
    checkpointing.
  - **LangSmith** — observability and evals.
  - **LangMem** — long-term memory abstraction; supports swarm-level learning and
    workflow indexing/reuse.
  Selected because they map to **production requirements**: state management &
  checkpointing, audit trails (*"who decided what, when, and why"*), interface
  compatibility with systems of record and MCP gateways, deterministic execution to
  enforce authorized actions, and interoperability with agents built on other
  frameworks.
- **Concrete pilot results.** Across Cisco internal use.
  - **Debugging:** 20+ workflows; **93% reduction in time-to-root-cause** vs historical
    baselines; some cross-team investigations under five minutes; independent QE
    confirmed no quality loss. **200+ engineering hours saved** across **512 sessions /
    70 users / one month**.
  - **Development:** 15+ workflows; **65% reduction in execution time**. *"The primary
    gains were not limited to faster code generation — which AI coding agents already
    perform well — but from compressing downstream workflows for functional testing
    after PR merge through coordinated agent execution."*
  - Baseline curation method: a bootcamp where engineering teams pre-curated use cases
    and the historical (no-agents) execution time, "reported conservatively."
- **A striking bottleneck observation.** *"PR review process itself became the
  bottleneck introduced by human-in-the-loop."* When agent coordination compresses the
  cycle around the PR, the human gating step becomes the new constraint. This is the
  team-scale corollary of Willison's [[agent-code-review]]: the discipline that keeps
  unreviewed agent code off colleagues' plates is *also* the rate limiter once the
  agentic system gets fast.
- **Cross-team scope.** The macro architecture extends across team boundaries — a
  Leader Agent in one team can collaborate with a Leader Agent in another (e.g., a
  product-management Leader routes a requirement to the engineering Leader, who routes
  it to the right Worker swarm).
- **Onboarding gain.** *"The benefit of the agentic engineering framework is the
  noticeable ease of ramp up into the software delivery pipeline with minimal setup
  required by engineers. Once the agents are configured, multiple teams can leverage
  the worker agent to fetch context from tools, both internal and external."* Long-term
  memory + a shared workflow library make reuse cheap.
- **The thesis the authors keep returning to.** *"The biggest step change doesn't come
  from better tools alone. It comes from systems that mirror real-world teams."* The
  unit of automation isn't a developer; it's a coordinated set of roles.

## Connections

- **The definitional split** is the most important relationship. The wiki's prior
  primary definition ([[2026-05-23-what-is-agentic-engineering]], reinforced by
  [[2026-04-30-sequoia-ascent-karpathy]]) describes a *practitioner discipline*; this
  source describes a *multi-agent control plane*. Both are now in active circulation
  in the field. The wiki carries both, side-by-side, in [[agentic-engineering]]
  (area). The cross-cutting comparison is in
  [[practitioner-discipline-vs-control-plane]] (synthesis).
- **New topic page:** [[multi-agent-coordination]] is the home for Worker/Leader,
  swarms, A2A vs MCP, the four-stage worker loop, LangGraph/LangSmith/LangMem, and the
  team-scale framing.
- **Coding agents as components.** The repositioning of Codex/Claude as *reasoning and
  code-generation engines embedded in Worker Agents* updates [[coding-agents]]: the
  Willison/Karpathy subject is a building block, not the whole stack. [[coding-agents]]
  now carries a forward link to [[multi-agent-coordination]].
- **"Swarm" disambiguation against [[subagents]].** Willison's *parallel subagents*
  are fresh copies of the same coding agent dispatched by a parent within a single
  user-driven session. Kumar/Ramagopal's *swarm of Worker Agents* are persistent,
  role-differentiated agents coordinated by a Leader Agent across sessions and teams.
  Same word, different unit of organization — [[subagents]] now flags the difference.
- **LangMem as the team-scale analog of [[compound-engineering]].** Compound
  engineering accumulates *instructions* in a personal/repo harness; LangMem
  accumulates *workflow indices and long-term state* shared across a swarm. Same
  shape (transient signal → durable instruction), different organizational level.
- **A2A and MCP as [[agent-native-infrastructure]] substrate.** The Karpathy
  sensors/actuators thesis predicts standardized agent-to-agent and agent-to-system
  protocols; A2A + MCP are the concrete protocols this source operates on. MCP gets a
  second source backing it.
- **The PR-review-bottleneck observation** updates [[agent-code-review]]: it confirms
  the chapter's framing (human-in-the-loop review is the trust gate) and adds a
  team-scale wrinkle (it's also the rate limiter at scale).
- **The "post-PR testing compression"** observation refines [[agentic-testing]]: when
  code-gen is fast and tests are agent-runnable, the work that used to be the bulk of
  the cycle (downstream verification) becomes the surface area for further compression.
- **Fills the wiki's known enterprise / team-scale gap** flagged in
  [[willison-vs-karpathy]] and prior lint passes. The "blind spots outside both
  circles" zone in the Willison/Karpathy Venn diagram now has at least one source.
- **Authors:** [[kumar-ramagopal]]. Combined author page (single co-authored source;
  Cisco enterprise perspective).

## Raw file

`raw/Agentic Engineering How Swarms of AI Agents Are Redefining Software Engineering.md`
