---
type: synthesis
tags: [meta, agentic-engineering]
created: 2026-05-22
updated: 2026-05-25
status: developing
sources: 9
---

# Overview

The big-picture synthesis of this wiki — what it knows about [[agentic-engineering]] and the practices, paradigms, economics, mechanics, and habits that surround it, drawn together across every source ingested so far.

The LLM keeps this page current. When a new source meaningfully shifts the picture, this page is revised along with the affected area and topic pages.

## Current picture

The wiki now rests on two primary voices: eight chapters of [[simon-willison]]'s *Agentic Engineering Patterns* guide and [[andrej-karpathy]]'s [[2026-04-30-sequoia-ascent-karpathy|Sequoia Ascent 2026 fireside chat]]. Willison gives us the **practices and operational discipline**; Karpathy gives us the **paradigms and analytic frames** — see [[willison-vs-karpathy]] for the explicit cross-author comparison. Together they make a self-consistent argument across five layers.

### 1. What the field is — paradigm and definition

The paradigm-level frame is Karpathy's [[software-3-0]]: humans now program LLMs through **prompts, context, tools, examples, memory, and instructions**, with the LLM as the **interpreter** and the **context window as the program**. The earlier paradigms (1.0 explicit code, 2.0 learned weights) still run underneath; 3.0 is layered on top. A consequence: some software *should disappear* into direct model transformations (Karpathy's MenuGen example — multimodal model renders dish images onto the menu image; no app needed).

[[agentic-engineering]] is the practice of developing software inside this paradigm with the help of [[coding-agents|coding agents]] — software that runs tools in a loop toward a goal, with code execution as the defining tool. The canonical examples are Claude Code, OpenAI Codex, Gemini CLI; the **asynchronous** flavor (Gemini Jules, Codex web, Claude Code on the web) is a deliberate sub-category.

The vocabulary is now stable. Karpathy provides the canonical **vibe coding vs. agentic engineering** framing: vibe coding **raises the floor** (anyone can describe software into existence — fine for prototypes and personal tools); agentic engineering **raises the ceiling** (the professional discipline of coordinating fallible agents while preserving correctness, security, taste, and maintainability). Willison's narrow-definition discipline arrives at the same place.

### 2. How it actually works — mechanics

Under the hood, a coding agent is **a harness wrapping an LLM, extended with a system prompt and a set of callable tools, run in a loop.** That's most of the architecture; a simple version is a few dozen lines on top of an LLM API. [[agent-architecture]] details the pieces: tokens (providers charge per token; context windows top out around 1M but quality often degrades past 200K), chat templated prompts are a thin wrapper around stateless completion (so the harness replays the whole conversation each turn), **token caching** is the central cost optimization (and the reason coding agents deliberately avoid mutating earlier conversation), **system prompts** are often hundreds of lines and are the surface compound engineering writes to, and **reasoning/thinking mode** spends extra tokens to think before answering.

The right mental model for what you're working with is **ghosts, not animals** (Karpathy): LLMs are statistical simulations of human artifacts, not biological intelligences. Avoid anthropomorphic expectations; default posture is empirical familiarity.

The **context-window constraint** is what motivates [[subagents]] — a subagent is a fresh copy of the agent with a new context window, dispatched as a tool call. Three flavors: exploratory (Claude Code's `Explore` runs every new task), parallel (often on cheaper/faster models like Claude Haiku), specialist (code reviewer, test runner, debugger).

### 3. Why it matters economically — and where AI moves fastest

Coding agents collapse the per-task cost of producing code to near zero, which invalidates many engineering intuitions built around code being expensive. But *good code* — defined by a 9-point checklist (works, tested, documented, simple, handles errors, etc.) — is still expensive, and meeting that bar remains the human's responsibility. See [[economics-of-code]]. Two cost layers actually matter: **engineering time** (the headline story) and **tokens** (the layer that token caching and subagents are designed to keep low).

[[verifiability]] is the analytic frame that explains *why* coding agents in particular work so well: **traditional software automates what you can specify; LLMs automate what you can verify.** Code is verifiable — tests pass or fail, programs run or crash — so RL training has tight feedback loops and coding capability progresses fast. The **jagged intelligence** corollary explains the unevenness: capability ≈ verifiability × training attention × data coverage × economic value. Models simultaneously refactor 100K-line codebases and tell you to walk to a 50m-away car wash. The practical question for any project: *are you on the model's rails?*

### 4. What to spend the surplus on — quality, plus what *not* to do

Two concrete productive uses: eliminate the class of technical debt that is "simple but time-consuming" using async agents in worktrees and PRs ([[refactoring-with-agents]]), and run cheap parallel **exploratory prototypes** to make better technology choices. The mechanism for making the gains stick is [[compound-engineering]] — end each project with a retrospective whose output is **edits to the system prompt and tool harness** for future agent runs (term from Shipper & Klaassen at Every; Karpathy's compact recipe — define context / tools / feedback loop / guardrails / let agents work / preserve human understanding — describes the target).

The first named **anti-pattern**: filing PRs containing agent-generated code you haven't reviewed yourself. Async refactoring does not mean async human responsibility; [[agent-code-review]] is the governance layer.

### 5. The world side — agent-native infrastructure

[[agent-native-infrastructure]] (Karpathy): most software is still built for humans clicking screens. The world has to be rewritten with **sensors** (turn world-state into digital info) and **actuators** (let agents change things), exposed through markdown docs, CLIs, APIs, MCP servers, structured logs, copy-pasteable instructions, safe permissioning, headless setup flows. MenuGen deployment is the running benchmark — *"I should be able to say 'build MenuGen' and have the agent deploy the whole thing without manual clicking."*

For founders, the wedge that emerges: **valuable, verifiable, undertrained** domains. The most obvious verifiable domains (coding, math) are saturated by labs; many economically important domains have latent verifiable structure that hasn't been exploited.

### Cross-cutting habits

Three complementary habits sit underneath everything:

- **[[hoarding-working-examples|Hoard working examples]]** — keep a personal collection of runnable code that proves what you know how to do; point agents at it via `curl`, filesystem search, or `git clone`. Parallel subagents on cheap models accelerate hoard growth. Karpathy's `microGPT` and the LLM Wiki Pattern are canonical distilled artifacts in this family.
- **[[git-with-agents|Use Git ambitiously]]** — agents are fluent in basic *and* advanced Git, which removes the recall cost. `git bisect` becomes routine because agents handle the test-condition boilerplate. "Review changes made today" is a cheap session-seeding move.
- **[[compound-engineering|Compound across sessions]]** — retrospectives produce harness edits that persist. Hoarding accumulates *artifacts*; compound engineering accumulates *instructions*. Both turn one-time effort into permanent leverage.

### State of the picture

Two authors deep, but still single-perspective in the sense that both Willison and Karpathy are AI-positive practitioners writing from solo / small-team vantages. The wiki's blind spots are largely theirs — see "What's still missing" in [[willison-vs-karpathy]]: no adversarial perspective, light on team-scale coordination and evaluation methodology, no real vendor comparison, no enterprise framing.

The most load-bearing un-ingested external references are still: Shipper & Klaassen's [Every post on Compound Engineering](https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents); the linked [OpenAI Codex system prompt](https://github.com/openai/codex/blob/rust-v0.114.0/codex-rs/core/templates/model_instructions/gpt-5.2-codex_instructions_template.md); vendor subagent docs.

## Open questions

- **How do verification and review work at agent speed?** Parallel agents change the shape of code review; [[agent-code-review]] is a start; team-scale answer is still open.
- **Which old micro-tradeoffs flipped, and which didn't?** "Simple but time-consuming" debt class clearly flipped to yes; which decisions are still "no"?
- **What does updating the agent harness look like day-to-day?** [[compound-engineering]] names the practice and we now know the substrate (system prompt + tools + repo-level files). Open: how the system prompt is pruned, what a good "compound step" looks like.
- **How do you tell when you're on the model's rails before committing engineering effort?** [[verifiability]] describes the diagnosis but not the operational recipe.
- **What does a meaningfully agent-native product look like at the application layer** (vs. infrastructure)? [[agent-native-infrastructure]] characterizes infra; the application-layer equivalent is open.
- **Vendor portability of patterns and subagents.** Vendor docs exist; characterizations of differences don't.
- **When does reasoning mode pay off vs. cost too much?** ([[agent-architecture]])
- **Safe envelope for shared-branch history rewriting** ([[git-with-agents]]).
- **What other anti-patterns belong in [[agent-code-review]]?** Willison's chapter currently lists only one.
- **Counter-perspectives.** Skeptics, empirical quality studies, security framings, enterprise contexts — still missing.
