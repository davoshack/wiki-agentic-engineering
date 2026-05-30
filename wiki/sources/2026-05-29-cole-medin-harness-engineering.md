---
type: source
source_type: transcript
source_url: https://youtu.be/ulNsa0sD8N0
source_date: 2026-05
tags: [agentic-engineering, agent-harness, harness-engineering, context-engineering, ralph-loop, orchestration, hooks, ai-layer]
created: 2026-05-29
updated: 2026-05-29
status: developing
---

# Harness Engineering: What Separates Top Agentic Engineers Right Now

> **About this source.** Cole Medin is a YouTuber in the AI-coding space and the creator of **Archon**, an open-source "harness builder" he promotes at the end of the video as *"the easiest way to get started with agentic engineering."* The video also carries a paid **Google Cloud Agent CLI** sponsor segment (≈7:44–9:26) that is advertising, not core content. The substance — a clean three-layer model of the harness and a two-stage account of harness engineering — is genuinely useful and notably *less* sales-shaped than [[2026-05-28-andy-dev-dan-five-pillars|Andy Dev Dan's pillars]], but the Archon plug and the sponsor read should be calibrated for. The raw PDF is a bilingual auto-transcript (English + Spanish machine translation interleaved); takeaways below are from the English.

A ~15-minute explainer arguing that **harness engineering** — "building the wrapper around the model" — is "the next big thing for this year, just like [[context-engineering|context engineering]] was for last year," and that it is a *direct evolution* of context engineering rather than a wholly new thing. Cole breaks it into two stages: (1) engineering the **AI layer** *within a single coding-agent session*, and (2) the "peak evolution" of **orchestrating many coding-agent sessions** into an automated workflow (the [[ralph-loop|Ralph loop]] as the worked example). The throughline is *ownership*: **"every mistake becomes an opportunity to improve your harness"** — what he calls **system evolution**, with the human as the feed-forward operator.

## Diagram

![[cole-medin-harness-engineering.png]]
*Visual map of Cole's argument: the three-layer stack (LLM → coding agent → AI layer), the six AI-layer components (with Hooks called out), the system-evolution feedback loop, and Stage 2's manual foundational workflow alongside the automated Ralph loop. Source: [[cole-medin-harness-engineering.excalidraw]] — built with the project's `excalidraw-diagram` skill.*

## Key takeaways

### Definition and the three-layer model

- **Harness engineering = building the wrapper around the model.** *"Any agent is the combination of the underlying large language model… and then the wrapper around it that gives it the context and defines your processes."* The video focuses on AI coding assistants but Cole notes the idea extrapolates to any agent.
- A clean three-layer diagram:
  1. **The LLM** (GPT / Claude) — the *reasoning*. By itself "not that much": an LLM has no way to access a file system or run commands.
  2. **The coding agent you pick** (Claude Code, Codex, Pi, …) — *"not something you build yourself."* These tools are themselves harnesses a company engineered around a model; they supply the capabilities (filesystem, command execution) **plus the system prompt** out of the box. *"You're picking the harness when you choose the tool."* Which is best (Claude Code vs Codex …) is live debate.
  3. **The AI layer** — *"the ultimate wrapper around any coding agent session. This is what you get to actually build."* It defines all *your* context and processes.
- **The six components of the AI layer** (built into pretty much every AI coding assistant now): **global rules, skills, MCP servers, codebase search (LSP or knowledge graphs), hooks, and sub-agents.** *"No matter how you want to inject your process or your rules, you're going to do it through one of these six things."*

### Why it's a true evolution of context engineering (not just a rename)

Cole concedes most of the harness *is* just context engineering — context injection, actions through tools/MCPs, persistence, observability — and that this is why "harness engineering" is becoming a buzzword. Two things make it a real evolution:

1. **Control.** *"The one thing that really is different is control"* — Ralph loops, orchestrating different coding-agent sessions and sub-agents. He calls this a true evolution *from* sub-agents.
2. **The "skill issue" reframe / mindset.** Harness engineering is *"not just a skill, it's also sort of a mindset."* The pattern he names (crediting a linked article): *"The agent does something dumb, the engineer blames the model, and the blame gets filed under 'wait for the next version.'"* The harness-engineering mindset **rejects that default.** The failure is usually **legible**: agent didn't know a convention → add it to `agents.md`; agent ran a destructive command → add a hook that blocks it. **"Every mistake becomes a rule"** / *"every mistake becomes an opportunity to improve your harness."*

### System evolution — the feed-forward loop

Cole's term for the above is **system evolution**: *"taking ownership and improving the performance of your coding agent over time with the AI layer that you control."* The shape: an initial generation seeded with your **principles / context**, then **sensors for feedback** — hooks, review agents, self-correction skills — that **evolve your AI layer over time.** *"We want to be the human steering the system, feeding forward,"* rather than being at the mercy of whether the next session happens to avoid the same problem.

### Golden nuggets on the AI-layer components

- **Rules** are the *foundation*: constraints, conventions, patterns the agent should follow — global rules plus on-demand context (markdown / Confluence docs).
- **Skills** are *workflows*. Cole keeps **separate skills for plan, implement, and validate**, and — the strong recommendation — runs each **in a separate coding-agent session** to keep each one **token-efficient and focused**. Each skill **outputs an artifact** (a markdown doc) used as a **handoff** to the next session.
- **Hooks** (which he says are underused) earn three concrete uses:
  - **Pre-tool-use security hook** — runs before any tool call (file write, command); block destructive commands (e.g. deleting directories) and block reading sensitive files into the LLM's context.
  - **Stop-validation hook** — when the agent says it's done, **deterministically** run unit tests, linting, type-checking; if anything fails, **force the agent to iterate** until it passes.
  - **Lint after every file edit** — keeps the codebase clean, which also makes future agent runs more reliable.
- He links a **companion repo** as a concrete reference AI layer, and notes a separate video covering rules/skills/LSP/hooks in more depth.

### The foundational workflow

The basic process the repo demonstrates: **plan** (send the feature to the plan skill, iterate, produce a markdown plan) → hand the markdown to the **implement** skill in a *separate* session → the agent runs a **validation** strategy to check its own work. Still done *manually* at this stage — you carry the markdown between sessions yourself.

### Peak evolution — orchestrating coding-agent sessions

- **Don't hand a massive task / PRD to a single session.** It isn't token-efficient and the LLM gets overwhelmed: *"It does not matter how good the AI layer is… if you send too much into the LLM at once, it is going to fall flat on its face."*
- Instead, give **each session a very focused task** (these can be sub-agents, but in the Ralph loop they're *actual coding-agent sessions* handing artifacts to each other). Example pipeline: explore the user requirement → one agent **writes the plan** → send that plan artifact into **implementation** → **many code-review agents in parallel** (one for security, one for correctness, one for simplicity) → if all pass, **create the PR**; otherwise iterate.
- You can do this **manually** (open Claude Code twice), but the real power of harness engineering is to **automate** it — a system that hooks the sessions together with handoff documents and creates the PRs.

### The Ralph loop and Archon

- The **[[ralph-loop|Ralph loop]]** ([[geoffrey-huntley|Geoffrey Huntley]], credited as "one of the pioneers") is the worked example of an agent harness: a simple **bash or Python script** that takes a large scope (a "massive PRD"), splits it into individual tasks, and **runs coding-agent sessions one at a time in a `while` loop**, building up a log across iterations. The **only exit condition** is a `done.txt` (he says `done.ext`) marker the agent writes once it's confident the implementation and all validation are complete (e.g. "all 8 spec items done"). The point: *"we're automating it so we don't have to babysit our coding agent."*
- **Archon** — Cole's own **open-source harness builder**, pitched as the easiest way to build your own harnesses (like the Ralph loop but customized to your exact process / SDLC).
- Closing claim: *"This really is the future of agentic engineering — building these harnesses to handle larger scopes of work as the models and the underlying tools get more powerful. This is the way."*

## Connections

- **Second voice on [[agent-harness-engineering]].** The page was single-source ([[andy-dev-dan]]) and explicitly flagged as needing a second author; this source moves it from 1 → 2. Cole supplies the missing **structural model** (LLM → coding-agent/tool → AI layer; six AI-layer components) that Andy gestured at but never diagrammed.
- **Resolves a standing open question on that page.** The page asked whether harness engineering is "genuinely *new harnesses* or *incremental modifications to a base* — the latter being an aggressive form of [[compound-engineering]] applied to the harness layer." Cole comes down firmly on the **compound-engineering side**: his "every mistake becomes a rule / system evolution" is exactly compound engineering operating on the harness, made into a *mindset*.
- **Strengthens [[compound-engineering]].** "Every mistake becomes a rule" via hooks/skills/rules is the same *transient signal → durable instruction* loop, named as a mindset and located explicitly in the AI layer.
- **Parallels [[software-factory]].** Cole's automated plan → implement → parallel-review → PR pipeline is structurally Andy's ADW/"dark factory," and the Ralph loop is a concrete, minimal factory. Two independent practitioner voices now describe the same orchestration shape.
- **Sharpens [[subagents]].** Cole distinguishes *sub-agents* (one of the six AI-layer components) from *orchestrating actual coding-agent sessions that hand off to each other*, and calls the latter "a true evolution from sub agents." Adds the separate-session-per-phase, markdown-handoff pattern as a context-preservation play.
- **Feeds [[agentic-testing]].** The **stop-validation hook** (deterministically run tests/lint/typecheck and force iteration) is the verifier wired in *mechanically* — the deterministic complement to `First run the tests`.
- **Feeds [[agent-code-review]].** Parallel review agents (security / correctness / simplicity) gating PR creation is an automated expression of the review layer.
- **Introduces [[context-engineering]] as a named predecessor.** First source to position harness engineering explicitly as the successor to 2025's context engineering.
- **New people:** [[cole-medin]] (author; Archon), [[geoffrey-huntley]] (originator of the Ralph loop, currently a secondhand mention).
- **Echoes [[agent-architecture]].** "An LLM by itself can't touch a filesystem or run commands; the tool supplies that" is the same harness-wraps-the-LLM mechanics Willison details — Cole layers his three-tier diagram on top of it.

## Raw file

`raw/Harness Engineering_ What Separates Top Agentic Engineers Right Now.pdf`
</content>
</invoke>
