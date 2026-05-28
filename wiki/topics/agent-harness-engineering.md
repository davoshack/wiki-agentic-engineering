---
type: topic
tags: [agentic-engineering, harness, custom-harness, specialization, extensible-software]
created: 2026-05-28
updated: 2026-05-28
status: developing
sources: 1
---

# Agent harness engineering

Treating the **harness** — the software that wraps the LLM with a system prompt, tools, conversation management, and the outer loop — as a *first-class engineering discipline*, not a fixed substrate you rent from a vendor. The thesis: if [[agent-architecture]] explains *what a harness is*, this topic is about *building and customizing your own*.

## Synthesis

[[andy-dev-dan]]'s framing in [[2026-05-28-andy-dev-dan-five-pillars]] is the sharpest single-claim statement of harness primacy in the wiki: ***"Whoever controls the agent harness controls your results."*** He treats out-of-the-box harnesses — Claude Code, OpenAI Codex, OpenCode — as **the floor, not the ceiling.** They're *"a great start, a terrible place to finish."* The implication: meaningful gains at the upper end of agentic engineering come from owning and customizing the substrate.

This claim sits between two existing frames:

- [[agent-architecture]] (from [[2026-05-23-how-coding-agents-work|Willison]]) treats the harness as a *thing-to-understand-and-use* — what tokens cost, how token caching works, how the system prompt and tool-call protocol fit together. The reader is expected to be a *user* of that architecture.
- [[compound-engineering]] treats the harness as a *thing-to-iteratively-improve* across runs — each project's retrospective writes lessons back into the system prompt, the `CLAUDE.md`-style instruction files, the tool harness itself.

Harness engineering is a step further: the harness is a *thing-to-design-and-build* as a daily practice. Andy claims to *"build one new custom agent harness every single day"* on top of a composable third-party substrate (he uses the "PI agent harness" by "Mario"; the wiki has no primary source on PI yet). The key affordance he names is **composability** — assembling a unique harness by stacking skills, agents, commands, sandboxes, model fallbacks, model routers, etc.

### What custom-harness ownership lets you do

From Andy's enumeration:

- **Sandbox tools** by default — every prompt and tool call runs in a constrained environment.
- **Sub-agent delegation** wired to your own patterns (vs. only the vendor's defaults; cf. [[subagents]]).
- **Damage control** — guardrails and rollback mechanisms specific to your codebase / domain.
- **Model fallbacks and routing** — different models for different stages or roles (e.g., cheap models for parallel exploration, frontier models for planning — same logic as [[subagents]]' parallel-subagent flavor but generalized).
- **Multi-agent orchestration** at custom granularity — Andy demos a 3-tier "UIA J team" (orchestrator → team leads → workers) with a chat-room interface. This is conceptually the *solo-engineer* analog of [[multi-agent-coordination|Kumar & Ramagopal's Worker / Leader architecture]] at organization scale.
- **Agent communication networks** — multiple model-specific agents (e.g., an Opus 4.7 agent + a Gemini 3.5 flash agent) on a shared message bus the main agent can call into.

### Specialization as the moat

Andy's claim: ***"Specialization is the moat. This will always be true."*** Custom harnesses let you build *domain-specific* variants — a DevOps harness, a testing harness, a billing harness — that out-perform general-purpose vendor harnesses for the specific work they target. The corollary: *if you don't own your harness, you cannot specialize.* You're stuck with whatever your vendor exposes.

This is a meaningful claim worth holding alongside the [[verifiability|jagged-intelligence]] frame: where Karpathy says capability spikes are *training-shaped* (labs decide what verifiable RL to invest in), Andy says they're also *harness-shaped* — a specialized harness routes the model into its narrow strengths and keeps it out of its weaknesses.

### Extensibility as a prerequisite

Andy treats **extensible / pluggable / composable software** as a prerequisite for harness engineering — both for the harness itself (which should be swappable on the fly) and for the codebases the agent operates on. *"Open to extension, closed to modification"* (the Open-Closed Principle) gets explicit invocation. Reason: models, prompts, tools change constantly; brittle software with cascading `if` statements makes agents slow and error-prone navigating it.

The two scopes:
- **Engineering scope** (your own harness, your dev tools) — pluggability is what lets you swap models, system prompts, tool definitions on demand.
- **Production scope** (your shipped products) — agents operating on or with your production code benefit from the same shape; this connects to [[agent-native-infrastructure]] on the world-side.

### Where this sits relative to the rest of the wiki

- **Above [[agent-architecture]].** That page is the *mechanics*. This page is the *discipline of customizing them*.
- **Adjacent to [[compound-engineering]].** Compound engineering accumulates *instructions* into the harness over time; harness engineering also reshapes the *tools and structure* of the harness, not just its content.
- **Parallel to [[multi-agent-coordination]] at smaller scale.** Andy's multi-team orchestrations are solo-engineer-scale; Kumar & Ramagopal's Worker / Leader systems are organization-scale. Same family of patterns, different blast radius.
- **Feeds [[software-factory]].** A specialized harness is a component of a software factory; the factory wraps it with planning, validation, deployment.
- **Models matter less.** Andy's closing meta-claim — *"Models matter less and less. What matters is the systems you place around your agents"* — is most directly an argument for the centrality of harness engineering. It's the strongest single-voice substrate-maximalist claim currently in the wiki.

## Open questions

- How portable is a custom harness across model families? If you build a harness on PI, what happens when you want to swap Opus for Codex underneath?
- What's the right granularity of "specialization"? A DevOps harness is plausible; is a per-microservice harness over-fragmentation?
- The single-source-and-author basis (Andy + PI) means this page rests on one practitioner's setup. The wiki currently has no primary source on the PI harness itself; ingesting one would let the page move from 1 source to 2 and characterize the substrate Andy depends on.
- Andy's "build a new harness every day" claim is striking. Is the discipline genuinely *new harnesses* or *incremental modifications to a base*? The distinction matters: the former implies high duplication; the latter is just an aggressive form of [[compound-engineering]] applied to the harness layer.
- Where does the boundary between *harness engineering* and *agent-harness-as-product* sit? Andy hints at production-deployable agents but doesn't draw it sharply.
- For a single engineer's harness, what's the right balance between specialized variants (one per domain) and a single composable base with profiles? Andy's "one new harness per day" implies the former; software-engineering instincts about DRY suggest the latter.

## Sources

- [[2026-05-28-andy-dev-dan-five-pillars]]
