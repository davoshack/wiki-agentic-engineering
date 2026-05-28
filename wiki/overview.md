---
type: synthesis
tags: [meta, agentic-engineering]
created: 2026-05-22
updated: 2026-05-28
status: developing
sources: 14
---

# Overview

The big-picture synthesis of this wiki — what it knows about [[agentic-engineering]] and the practices, paradigms, economics, mechanics, and habits that surround it, drawn together across every source ingested so far.

The LLM keeps this page current. When a new source meaningfully shifts the picture, this page is revised along with the affected area and topic pages.

## Current picture

The wiki now rests on four voices. Three sit on the practitioner-side spine: eleven chapters of [[simon-willison]]'s *Agentic Engineering Patterns* guide, [[andrej-karpathy]]'s [[2026-04-30-sequoia-ascent-karpathy|Sequoia Ascent 2026 fireside chat]], and [[andy-dev-dan]]'s [[2026-05-28-andy-dev-dan-five-pillars|five-pillars video]] (channel host of *agenticengineer.com* and seller of *Tactical Agent Coding*; treat his sharper claims as practitioner conjecture per the caveat on his source page). The fourth is the wiki's first enterprise / team-scale source: [[kumar-ramagopal|Kumar & Ramagopal]]'s [[2026-05-26-agentic-engineering-swarms|LangChain-blog write-up of a Cisco multi-agent coordination pilot]]. Willison gives **practices and operational discipline**; Karpathy gives **paradigms and analytic frames** (see [[willison-vs-karpathy]]); Andy gives a **substrate-maximalist prescription** for the individual senior engineer (own the harness, build the factory, gate AFK agents on real arbitrage); Kumar & Ramagopal give the **control plane** that wraps everything at organizational scale — and a meaningfully different definition of *"agentic engineering"* (see [[practitioner-discipline-vs-control-plane]]). Together the four make a self-consistent argument across the layers below.

### 1. What the field is — paradigm and definition

The paradigm-level frame is Karpathy's [[software-3-0]]: humans now program LLMs through **prompts, context, tools, examples, memory, and instructions**, with the LLM as the **interpreter** and the **context window as the program**. The earlier paradigms (1.0 explicit code, 2.0 learned weights) still run underneath; 3.0 is layered on top. A consequence: some software *should disappear* into direct model transformations (Karpathy's MenuGen example — multimodal model renders dish images onto the menu image; no app needed).

[[agentic-engineering]] is the practice of developing software inside this paradigm with the help of [[coding-agents|coding agents]] — software that runs tools in a loop toward a goal, with code execution as the defining tool. The canonical examples are Claude Code, OpenAI Codex, Gemini CLI; the **asynchronous** flavor (Gemini Jules, Codex web, Claude Code on the web) is a deliberate sub-category.

The vocabulary is now stable. Karpathy provides the canonical **vibe coding vs. agentic engineering** framing: vibe coding **raises the floor** (anyone can describe software into existence — fine for prototypes and personal tools); agentic engineering **raises the ceiling** (the professional discipline of coordinating fallible agents while preserving correctness, security, taste, and maintainability). Willison's narrow-definition discipline arrives at the same place.

### 2. How it actually works — mechanics

Under the hood, a coding agent is **a harness wrapping an LLM, extended with a system prompt and a set of callable tools, run in a loop.** That's most of the architecture; a simple version is a few dozen lines on top of an LLM API. [[agent-architecture]] details the pieces: tokens (providers charge per token; context windows top out around 1M but quality often degrades past 200K), chat templated prompts are a thin wrapper around stateless completion (so the harness replays the whole conversation each turn), **token caching** is the central cost optimization (and the reason coding agents deliberately avoid mutating earlier conversation), **system prompts** are often hundreds of lines and are the surface compound engineering writes to, and **reasoning/thinking mode** spends extra tokens to think before answering.

The right mental model for what you're working with is **ghosts, not animals** (Karpathy): LLMs are statistical simulations of human artifacts, not biological intelligences. Avoid anthropomorphic expectations; default posture is empirical familiarity.

The **context-window constraint** is what motivates [[subagents]] — a subagent is a fresh copy of the agent with a new context window, dispatched as a tool call. Three flavors: exploratory (Claude Code's `Explore` runs every new task), parallel (often on cheaper/faster models like Claude Haiku), specialist (code reviewer, test runner, debugger).

### 3. Why it matters economically — and where AI moves fastest

Coding agents collapse the per-task cost of producing code to near zero, which invalidates many engineering intuitions built around code being expensive. But *good code* — defined by a 9-point checklist (works, tested, documented, simple, handles errors, etc.) — is still expensive, and meeting that bar remains the human's responsibility. See [[economics-of-code]]. Three cost-and-return layers now matter: **engineering time** (the headline story); **tokens** (the layer that token caching and subagents are designed to keep low); and [[tokeconomics|tokeconomics]] (Andy's *return-side* lens — a 3-level funnel from token-maxing → useful tokens → captured arbitrage, with **always-on / AFK agents** as the *output* of climbing the funnel rather than a default).

[[verifiability]] is the analytic frame that explains *why* coding agents in particular work so well: **traditional software automates what you can specify; LLMs automate what you can verify.** Code is verifiable — tests pass or fail, programs run or crash — so RL training has tight feedback loops and coding capability progresses fast. The **jagged intelligence** corollary explains the unevenness: capability ≈ verifiability × training attention × data coverage × economic value. Models simultaneously refactor 100K-line codebases and tell you to walk to a 50m-away car wash. The practical question for any project: *are you on the model's rails?*

### 4. What to spend the surplus on — quality, plus what *not* to do

Two concrete productive uses: eliminate the class of technical debt that is "simple but time-consuming" using async agents in worktrees and PRs ([[refactoring-with-agents]]), and run cheap parallel **exploratory prototypes** to make better technology choices. The mechanism for making the gains stick is [[compound-engineering]] — end each project with a retrospective whose output is **edits to the system prompt and tool harness** for future agent runs (term from Shipper & Klaassen at Every; Karpathy's compact recipe — define context / tools / feedback loop / guardrails / let agents work / preserve human understanding — describes the target). [[andy-dev-dan|Andy]] supplies the workflow-level expression of the same motion: the **[[software-factory|software factory]]** wraps planning, spec, build, test, and review into a single-prompt pipeline. Compound engineering compounds *instructions*; the factory compounds *whole workflows*. They stack. The aspirational endpoint Andy names is **ZTE — Zero Touch Engineering** (prompt → production), gated of course by [[agent-code-review]] until the spec-and-guardrails layer is mature enough.

Andy's substrate-maximalist sharpening: ***"Models matter less and less. What matters is the systems you place around your agents."*** The substrate has three layers worth distinguishing: the **harness** ([[agent-harness-engineering]] — out-of-box vendors are the floor, custom composable harnesses are the ceiling; *"specialization is the moat"*); the **factory** ([[software-factory]] — built on top of the harness); and the **agentic access surface** ([[agent-native-infrastructure]] — the world the agent reaches into, with every missing API/CLI/MCP paid as a *token tax* per [[tokeconomics]]).

The first named **anti-pattern**: filing PRs containing agent-generated code you haven't reviewed yourself. Async refactoring does not mean async human responsibility; [[agent-code-review]] is the governance layer.

### 5. The world side — agent-native infrastructure

[[agent-native-infrastructure]] (Karpathy): most software is still built for humans clicking screens. The world has to be rewritten with **sensors** (turn world-state into digital info) and **actuators** (let agents change things), exposed through markdown docs, CLIs, APIs, MCP servers, structured logs, copy-pasteable instructions, safe permissioning, headless setup flows. MenuGen deployment is the running benchmark — *"I should be able to say 'build MenuGen' and have the agent deploy the whole thing without manual clicking."* Andy adds the economic case via the **token tax** ([[tokeconomics]]): every missing surface is a recurring cost paid in tokens, so the upfront investment to expose an API pays back as cheaper agent runs forever.

For founders, the wedge that emerges: **valuable, verifiable, undertrained** domains. The most obvious verifiable domains (coding, math) are saturated by labs; many economically important domains have latent verifiable structure that hasn't been exploited.

### 6. The team / organization side — the control plane

[[multi-agent-coordination]] ([[kumar-ramagopal|Kumar & Ramagopal]], Cisco, on LangChain): once an organization runs many agents in parallel across many teams, the unit of automation is no longer *the developer + a coding agent in a session* but a **swarm of role-differentiated agents** with a **Leader Agent** providing shared prompts, a common tool gateway, long-term memory ([LangMem](https://langchain-ai.github.io/langmem/)), global observability ([LangSmith](https://www.langchain.com/langsmith)), and orchestration over LangGraph. Worker Agents talk **agent-to-agent via A2A**; non-A2A agents are wrapped in **MCP adapters**. The Worker Agent loop is *intent → plan + notify → execute + checkpoint → validate + persist.* Coding agents like Codex and Claude run *inside* Worker Agents as reasoning and code-generation engines — the practitioner-discipline literature still applies; it just gets industrialised inside the control plane.

The Cisco pilot reports a **93% reduction in time-to-root-cause** across 20+ debug workflows (200+ engineering hours saved across 512 sessions / 70 users / one month) and a **65% reduction in execution time** across 15+ development workflows. The headline finding: *"PR review process itself became the bottleneck introduced by human-in-the-loop"* — once coordination overhead is compressed, the trust gate from [[agent-code-review]] becomes the rate limiter. Numbers are from a single enterprise with internal-baseline methodology and should be read with caveats; they are nonetheless the most concrete delivery-cycle numbers in the wiki.

The Kumar & Ramagopal source also uses *"agentic engineering"* in a sense substantively different from the Willison/Karpathy practitioner discipline — multi-agent control plane vs. human-using-coding-agent practice — and the wiki carries both definitions side by side. [[practitioner-discipline-vs-control-plane]] is the cross-cutting comparison.

### Cross-cutting habits

Four complementary habits sit underneath everything:

- **[[hoarding-working-examples|Hoard working examples]]** — keep a personal collection of runnable code that proves what you know how to do; point agents at it via `curl`, filesystem search, or `git clone`. Parallel subagents on cheap models accelerate hoard growth. Karpathy's `microGPT` and the LLM Wiki Pattern are canonical distilled artifacts in this family.
- **[[git-with-agents|Use Git ambitiously]]** — agents are fluent in basic *and* advanced Git, which removes the recall cost. `git bisect` becomes routine because agents handle the test-condition boilerplate. "Review changes made today" is a cheap session-seeding move.
- **[[compound-engineering|Compound across sessions]]** — retrospectives produce harness edits that persist. Hoarding accumulates *artifacts*; compound engineering accumulates *instructions*. Both turn one-time effort into permanent leverage.
- **[[agentic-testing|Wire the verifier in]]** — `First run the tests` to seed a session and put the agent in a testing mindset; `Use red/green TDD` to build new code test-first; manual testing (`python -c`, `curl`, Playwright/Rodney) for what the suite misses; route every manual finding back into the suite via red/green so verification compounds. Tests are the canonical reward signal (the [[verifiability|verifiability]] frame at workflow level), and the four-word prompt pattern shows how much pre-trained engineering discipline a compact phrase can activate.

### State of the picture

Four voices deep now. The practitioner-side blind spot around team-scale coordination, enterprise framing, and concrete delivery-cycle numbers — flagged in [[willison-vs-karpathy]] and prior lint passes — has been partially filled by [[kumar-ramagopal|Kumar & Ramagopal]]. Andy adds a fourth practitioner vantage (individual senior engineer, channel-host with course business) and several new vocabulary anchors (software factory / ADWs / ZTE, tokeconomics, token tax, agent-harness-engineering as a discipline). The remaining gaps: still no adversarial / skeptical perspective; no security-first or compliance-first framing; no academic / empirical-quality studies; vendor comparison still thin; no source from a second enterprise to triangulate the Cisco numbers; no primary source on the PI agent harness Andy depends on; the willison-vs-karpathy synthesis is now a two-of-four comparison and may want a multi-author refresh once the picture settles.

The most load-bearing un-ingested external references are still: Shipper & Klaassen's [Every post on Compound Engineering](https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents); the linked [OpenAI Codex system prompt](https://github.com/openai/codex/blob/rust-v0.114.0/codex-rs/core/templates/model_instructions/gpt-5.2-codex_instructions_template.md); vendor subagent docs. Newly load-bearing: a non-Cisco enterprise multi-agent pilot for triangulation; A2A protocol specification(s); a skeptical / adversarial framing of swarm-of-agents claims.

## Open questions

- **How do verification and review work at agent speed?** Parallel agents change the shape of code review; [[agent-code-review]] is a start; the Cisco pilot's *"PR review process itself became the bottleneck"* observation in [[2026-05-26-agentic-engineering-swarms]] sharpens the question. Open: which checks must remain human-only and which can move to a reviewer agent; whether *evidence-of-work-done* artifacts from [[agentic-testing]] meaningfully shorten human review time; whether a two-tier (agent-reviewer → human spot-check) gate is the right design. See [[practitioner-discipline-vs-control-plane]].
- **Which old micro-tradeoffs flipped, and which didn't?** "Simple but time-consuming" debt class clearly flipped to yes; which decisions are still "no"?
- **What does updating the agent harness look like day-to-day?** [[compound-engineering]] names the practice and we now know the substrate (system prompt + tools + repo-level files). Open: how the system prompt is pruned, what a good "compound step" looks like.
- **How do you tell when you're on the model's rails before committing engineering effort?** [[verifiability]] describes the diagnosis but not the operational recipe.
- **What does a meaningfully agent-native product look like at the application layer** (vs. infrastructure)? [[agent-native-infrastructure]] characterizes infra; the application-layer equivalent is open.
- **Vendor portability of patterns and subagents.** Vendor docs exist; characterizations of differences don't.
- **When does reasoning mode pay off vs. cost too much?** ([[agent-architecture]])
- **Safe envelope for shared-branch history rewriting** ([[git-with-agents]]).
- **What other anti-patterns belong in [[agent-code-review]]?** Willison's chapter currently lists only one.
- **Counter-perspectives.** Skeptics, empirical quality studies, security framings — still missing. Enterprise framing partly filled by [[2026-05-26-agentic-engineering-swarms]]; a second enterprise source for triangulation is now load-bearing.
- **Vocabulary trajectory.** *"Agentic engineering"* is now in active use with two non-identical meanings ([[practitioner-discipline-vs-control-plane]]). Does the field settle on one, or do both stabilize? Worth watching the next sources.
- **Safe envelope at swarm scale.** [[multi-agent-coordination]] systems have a different failure surface from single-coding-agent sessions (cascade failures, unauthorized actions, inter-agent prompt injection). The post mentions deterministic execution and authorized actions but doesn't go deep.
