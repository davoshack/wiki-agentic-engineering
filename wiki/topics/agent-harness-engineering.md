---
type: topic
tags: [agentic-engineering, harness, custom-harness, specialization, extensible-software, ai-layer, harness-engineering]
created: 2026-05-28
updated: 2026-05-29
status: developing
sources: 2
---

# Agent harness engineering

Treating the **harness** — the software that wraps the LLM with a system prompt, tools, conversation management, and the outer loop — as a *first-class engineering discipline*, not a fixed substrate you rent from a vendor. The thesis: if [[agent-architecture]] explains *what a harness is*, this topic is about *building and customizing your own*.

The wiki now has two practitioner voices on this: [[andy-dev-dan]] (harness *primacy* — why it's the moat) and [[cole-medin]] (harness *structure* — the layers and components you actually build, and the mindset that drives it). They agree on the thesis and complement each other on the detail.

## Synthesis

[[andy-dev-dan]]'s framing in [[2026-05-28-andy-dev-dan-five-pillars]] is the sharpest single-claim statement of harness primacy in the wiki: ***"Whoever controls the agent harness controls your results."*** He treats out-of-the-box harnesses — Claude Code, OpenAI Codex, OpenCode — as **the floor, not the ceiling.** They're *"a great start, a terrible place to finish."* The implication: meaningful gains at the upper end of agentic engineering come from owning and customizing the substrate.

[[cole-medin]] (in [[2026-05-29-cole-medin-harness-engineering]]) supplies the **structure** Andy gestures at but never diagrams, and frames the whole discipline as **a direct evolution of [[context-engineering]]** — *"the next big thing for this year, just like context engineering was for last year."*

This claim sits between two existing frames:

- [[agent-architecture]] (from [[2026-05-23-how-coding-agents-work|Willison]]) treats the harness as a *thing-to-understand-and-use* — what tokens cost, how token caching works, how the system prompt and tool-call protocol fit together. The reader is expected to be a *user* of that architecture.
- [[compound-engineering]] treats the harness as a *thing-to-iteratively-improve* across runs — each project's retrospective writes lessons back into the system prompt, the `CLAUDE.md`-style instruction files, the tool harness itself.

Harness engineering is a step further: the harness is a *thing-to-design-and-build* as a daily practice. Andy claims to *"build one new custom agent harness every single day"* on top of a composable third-party substrate (he uses the "PI agent harness" by "Mario"; the wiki has no primary source on PI yet). The key affordance he names is **composability** — assembling a unique harness by stacking skills, agents, commands, sandboxes, model fallbacks, model routers, etc.

### The three-layer model (Cole Medin)

[[cole-medin]]'s diagram is the cleanest structural account in the wiki of *what you're actually building*:

1. **The LLM** — GPT, Claude, etc. The reasoning. By itself, *"not that much"*: an LLM has no way to touch a file system or run commands. (This is the [[agent-architecture]] mechanics, stated as a floor.)
2. **The coding agent you pick** — Claude Code, Codex, Pi, … *"not something you build yourself."* Each is itself a harness a vendor engineered around a model, supplying capabilities (filesystem, command execution) **plus a system prompt** out of the box. *"You're picking the harness when you choose the tool."*
3. **The AI layer** — *"the ultimate wrapper around any coding agent session. This is what you get to actually build."* It defines all of *your* context and processes, sitting on top of whatever vendor harness you chose.

The distinction between layers 2 and 3 is the load-bearing one: layer 2 is **rented and roughly fixed** (the debate over "is Claude Code or Codex the best harness" lives here); layer 3 is **yours to engineer**, and it's where this whole topic operates. Andy's "own the harness" and Cole's "build the AI layer" are the same prescription aimed at the same layer.

### The six components of the AI layer

Cole's enumeration of *how* you inject process and rules — *"no matter how you want to inject your process or your rules, you're going to do it through one of these six things"*:

1. **Global rules** — constraints, conventions, patterns (plus on-demand context like markdown / Confluence docs). The *foundation* of the AI layer.
2. **Skills** — reusable workflows. Cole keeps **separate plan / implement / validate skills and runs each in a separate session** (token efficiency + focus), each emitting a **markdown artifact** as the handoff to the next.
3. **MCP servers** — external capabilities and data.
4. **Codebase search** — LSP or knowledge graphs.
5. **Hooks** — deterministic code that fires around tool calls. Cole's three high-value uses: a **pre-tool-use security hook** (block destructive commands, block reading secrets into context), a **stop-validation hook** (deterministically run tests/lint/typecheck on "done" and force iteration — see [[agentic-testing]]), and **lint-after-every-edit**.
6. **Sub-agents** — fresh-context delegation (see [[subagents]]).

This list is a useful *checklist for the surface area of a custom harness* — it's the concrete inventory of what Andy's "composable substrate" composes.

### Harness engineering vs. context engineering — the "what's actually new" question

Cole is unusually honest that *most* of the harness is just [[context-engineering]] under a new name — context injection, tool/MCP actions, persistence, observability — which is *why* "harness engineering" risks becoming a buzzword. He names **two things that make it a genuine evolution**:

1. **Control** — orchestrating multiple coding-agent sessions and sub-agents (the [[ralph-loop|Ralph loop]]). *"The one thing that really is different is control."*
2. **The system-evolution mindset** (below).

So: **harness engineering ≈ context engineering + control + ownership-mindset.** That decomposition is the most precise the wiki has, and it resolves some of the term's fuzziness.

### System evolution — "every mistake becomes a rule"

Cole's strongest contribution is reframing harness engineering as a **mindset**, not just a skill. The pattern he names: *"the agent does something dumb, the engineer blames the model, and the blame gets filed under 'wait for the next version.'"* The harness-engineering mindset **rejects that default** because the failure is usually **legible**:

> The agent didn't know about a convention, so you add it to `agents.md`. The agent ran a destructive command, so you add a hook that blocks it. **Every mistake becomes a rule** — an opportunity to improve your harness.

He calls this **system evolution**: an initial generation seeded with your principles, then **sensors for feedback** (hooks, review agents, self-correction skills) that **evolve the AI layer over time**, with *"the human steering the system, feeding forward."* This is **[[compound-engineering]] relocated to the harness layer and elevated to a posture** — and it settles the open question this page used to carry (see below): the discipline is *not* literally "a brand-new harness every day" so much as **relentless compounding modification of a base via legible failures.**

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
- **Culminates in orchestration.** Cole's "peak evolution" of harness engineering is **orchestrating many coding-agent sessions** — don't hand a massive PRD to one session (it gets token-overwhelmed and *"falls flat on its face"* however good the AI layer is); split it across focused sessions and automate the hand-offs. The [[ralph-loop|Ralph loop]] is the minimal worked example, and Cole's **Archon** is his open-source builder for it. This is the same shape as [[software-factory]] and the solo-scale analog of [[multi-agent-coordination]].
- **Builds on [[context-engineering]].** Cole frames the AI layer as a *direct evolution* of context engineering — the harness is mostly context engineering, plus control and the ownership mindset.
- **Models matter less.** Andy's closing meta-claim — *"Models matter less and less. What matters is the systems you place around your agents"* — is most directly an argument for the centrality of harness engineering. Cole's *"it does not matter how good the AI layer is… if you send too much into the LLM at once, it is going to fall flat on its face"* is the complementary caution: the substrate is the lever, but it can't rescue a badly-scoped session. Together they are the strongest substrate-maximalist position in the wiki.

## Open questions

- How portable is a custom harness across model families? If you build a harness on PI, what happens when you want to swap Opus for Codex underneath?
- What's the right granularity of "specialization"? A DevOps harness is plausible; is a per-microservice harness over-fragmentation?
- **Two practitioner voices, no primary substrate source.** The page now rests on two practitioners ([[andy-dev-dan]] + [[cole-medin]]), which de-risks the single-voice problem — but both depend on tools the wiki hasn't ingested directly (Andy's **PI harness**, Cole's **Archon**). A primary source on *either* would let the page characterize a concrete harness substrate rather than describe it secondhand.
- ~~Is the discipline genuinely *new harnesses* or *incremental modifications to a base*?~~ **Largely resolved by Cole:** his "every mistake becomes a rule / system evolution" framing puts it firmly on the *compounded-modification-of-a-base* side — an aggressive form of [[compound-engineering]] applied to the harness layer. Andy's "new harness every day" is best read as the same motion described maximally. Residual question: is there ever a case for genuinely *forking* a harness vs. always evolving one base?
- Where does the boundary between *harness engineering* and *agent-harness-as-product* sit? Andy hints at production-deployable agents but doesn't draw it sharply; Cole's Archon *is* a productized harness builder, which sharpens but doesn't settle the question.
- For a single engineer's harness, what's the right balance between specialized variants (one per domain) and a single composable base with profiles? Andy's "one new harness per day" implies the former; Cole's "evolve one AI layer per codebase" and DRY instincts suggest the latter.
- Cole and Andy cut the harness differently (Cole: LLM → coding-agent → AI-layer-of-six-components; Andy: harness / factory / access-surface). Do these reconcile into one model, and which cut is more useful in practice?

## Sources

- [[2026-05-28-andy-dev-dan-five-pillars]]
- [[2026-05-29-cole-medin-harness-engineering]]
