---
type: index
updated: 2026-05-30
---

# Index

The catalog of every page in this wiki. The LLM updates this on every ingest. To answer a
question, read this first to find relevant pages, then drill into them.

## Overview

- [[overview]] — the evolving big-picture synthesis of what the wiki knows so far.

## Areas

- [[agentic-engineering]] — the practice of developing software with the help of coding agents; the standing domain the wiki is built around.

## Topics

### Foundations

- [[coding-agents]] — what an agent is (tools in a loop), why code execution is the defining capability, sync vs. async flavors, vibe-coding vs. agentic-engineering (Karpathy's canonical floor/ceiling framing).
- [[agent-architecture]] — how a coding agent is actually built: LLM + system prompt + tools in a loop. Tokens, context windows, token caching, the tool-call protocol, reasoning mode, ghosts-not-animals mental model.
- [[agent-harness-engineering]] — the discipline of building and customizing your own harness. **Two voices:** Andy Dev Dan (harness *primacy* — *"whoever controls the harness controls your results"*, *"specialization is the moat"*) and Cole Medin (harness *structure* — the three-layer model: LLM → coding-agent → **AI layer**; six AI-layer components: rules, skills, MCP, codebase-search, hooks, sub-agents; *"every mistake becomes a rule"* = system evolution).
- [[context-engineering]] — *(stub)* curating what enters the context window; named in the wiki as the predecessor harness engineering evolves from (harness engineering ≈ context engineering + control + ownership-mindset).
- [[software-3-0]] — Karpathy's paradigm progression (1.0 explicit code → 2.0 learned weights → 3.0 LLM-as-interpreter, context-window-as-program). Some apps should disappear into direct model transformations.

### Economics and analytic frames

- [[economics-of-code]] — the cost of producing code has collapsed; the cost of producing *good* code (9-dimension checklist) has not; old engineering intuitions are due for an overhaul; spend the surplus on quality. Token-cost layer and the verifiability-of-coding explanation included.
- [[verifiability]] — Karpathy's analytic frame: LLMs automate what you can verify. Jagged intelligence as a corollary; capability spikes where labs train heavily on verifiable RL.
- [[tokeconomics]] — Andy Dev Dan's *return-side* lens: 3-level funnel from token-maxing → useful tokens → captured arbitrage; the **token tax** as the recurring cost of missing agent-native surfaces; AFK / always-on agents as the *output* of L3 rather than a default.

### Practices

- [[hoarding-working-examples]] — keep a personal collection of runnable code that proves what you know how to do, and recombine those examples in agent prompts. Karpathy's `microGPT` and the LLM Wiki Pattern as canonical distilled artifacts.
- [[refactoring-with-agents]] — use async coding agents to eliminate the "simple but time-consuming" class of technical debt; worktree workflow, PR evaluation, zero-tolerance for code smells.
- [[git-with-agents]] — Git is a key tool for agent workflows; agents are fluent in basic and advanced Git, which lets the human be more ambitious. Prompt vocabulary, the "sort out this git mess" pattern, bisect, and history rewriting as editorial work.
- [[subagents]] — dispatching a fresh copy of the agent with a new context window. Three flavors: exploratory (Claude Code's `Explore`), parallel (often on cheaper models like Haiku), specialist (code reviewer, test runner, debugger).
- [[compound-engineering]] — end each project with a retrospective whose output is updated agent instructions (system prompt, harness, repo-level instruction files); quality compounds across runs. Karpathy's compact recipe (define context / tools / feedback loop / guardrails; let agents work; preserve understanding) is the target shape.
- [[software-factory]] — Andy Dev Dan's ambitious prescription: *"build factories, not features."* Wrap planning, spec, build, test, and review into a single-prompt pipeline (AI Developer Workflows / ADWs / "dark factory"). Stacks on top of [[compound-engineering]]; aspirational endpoint is **ZTE = Zero Touch Engineering** (prompt → production).
- [[agent-code-review]] — the human owns the first review pass on agent-generated code; characteristics of a good agentic PR; evidence-of-work-done signals.
- [[agentic-testing]] — testing as the verification layer: `First run the tests` to seed sessions, `Use red/green TDD` for new code, manual testing (`python -c`, `curl`, Playwright/Rodney) for what the suite misses; manual findings feed back into the suite via red/green so verification compounds. Short prompts as compressed software-engineering discipline. Cole Medin adds the **deterministic** complement: a stop-validation hook that runs tests/lint/typecheck on "done" and forces iteration.
- [[ralph-loop]] — *(stub)* Geoffrey Huntley's minimal orchestration pattern: a `while`-loop script that splits a large PRD into tasks, runs coding-agent sessions one at a time, and exits only on a `done.txt` marker. The smallest runnable [[software-factory]]; brought in via Cole Medin.

### Organization / team scale

- [[multi-agent-coordination]] — Worker / Leader architecture, A2A vs. MCP protocols, the four-stage Worker loop (intent → plan + notify → execute + checkpoint → validate + persist), LangGraph + LangSmith + LangMem as the substrate. The second sense of *"agentic engineering"* — a multi-agent control plane that wraps coding-agent sessions, not replaces them. Cisco pilot: 93% debug-time reduction; *"PR review became the bottleneck."*

### World-side

- [[agent-native-infrastructure]] — when the user is an agent acting for a human, products need sensors and actuators: markdown docs, CLIs, APIs, MCP servers, structured logs, copy-pasteable instructions, safe permissioning, headless setup flows. MenuGen deployment as the running benchmark.

## People

- [[simon-willison]] — author of *Agentic Engineering Patterns*; practitioner-oriented, definitionally disciplined, frames many patterns as extensions of pre-LLM craft.
- [[andrej-karpathy]] — co-founder of OpenAI; Tesla Autopilot; Eureka Labs. Paradigm-namer (Software 1.0/2.0/3.0; vibe coding; agentic engineering; verifiability; jagged intelligence; ghosts not animals). Originator of the LLM Wiki Pattern that inspired this wiki.
- [[kumar-ramagopal]] — Renuka Kumar (Cisco, Principal SWE / Director) and Prashanth Ramagopal (Cisco, Senior Director of Engineering). Combined author page for a single co-authored LangChain-blog post on a Cisco multi-agent coordination pilot. First enterprise / team-scale vantage in the wiki, and the source of the wiki's second sense of *"agentic engineering"*.
- [[andy-dev-dan]] — channel host of *agenticengineer.com*, seller of the *Tactical Agent Coding* course. Third practitioner-vantage voice; individual-senior-engineer scale; substrate-maximalist (*"models matter less and less"*). Read with the marketing caveat on his page.
- [[cole-medin]] — YouTuber and creator of the open-source *Archon* harness builder. Second voice on harness engineering; supplies its structural model (three layers, six AI-layer components) and the "system evolution" mindset. Comparatively measured, but promotes his own tool.
- [[geoffrey-huntley]] — *(stub)* credited as creator of the [[ralph-loop|Ralph loop]] and "one of the pioneers" of session orchestration. Secondhand mention only (via Cole Medin); no primary source yet.

## Syntheses

- [[willison-vs-karpathy]] — the wiki's first cross-author synthesis. Willison gives practices and operational discipline; Karpathy gives paradigms and analytic frames. Where they overlap, where they diverge, what's still missing from both.
- [[ghosts-and-the-bitter-lesson]] — anti-anthropomorphism at two stages: Sutton (don't encode your cognition intuitions into the *training*) and Karpathy (don't project your cognition intuitions onto the *resulting system*). The ghost is the artifact of taking Sutton seriously; jagged intelligence is the corollary of "scales with computation." Sutton not yet ingested.
- [[practitioner-discipline-vs-control-plane]] — names the wiki's first definitional split: Willison/Karpathy use *agentic engineering* to mean the practitioner discipline (human + coding agent); Kumar & Ramagopal use it to mean the control plane (swarm of role-differentiated agents coordinated by a Leader). The two compose — coding agents are components inside Worker Agents — and the PR-review gate is exposed as both the trust mechanism and the rate limiter when the rest of the cycle compresses.
- [[cole-medin-harness-engineering.excalidraw|cole-medin-harness-engineering]] *(diagram)* — visual map of Cole Medin's framework: three-layer stack (LLM → coding agent → AI layer), the six AI-layer components, the system-evolution feedback loop, and Stage 2's manual workflow alongside the automated Ralph loop. Embedded in [[2026-05-29-cole-medin-harness-engineering]].

## Sources

- [[2026-04-30-sequoia-ascent-karpathy]] — Andrej Karpathy in conversation with Stephanie Zhan, Sequoia Ascent 2026. Software 3.0, verifiability, jagged intelligence, vibe coding vs. agentic engineering, ghosts not animals, agent-native infrastructure, MenuGen examples.
- [[2026-05-23-what-is-agentic-engineering]] — Simon Willison, *Agentic Engineering Patterns* Ch. 1. Defines agentic engineering, agent, and coding agent; positions against vibe coding.
- [[2026-05-23-writing-code-is-cheap-now]] — Simon Willison, *Agentic Engineering Patterns* Ch. 2. The cost of code has dropped; the cost of *good* code hasn't; lists 9 dimensions of good code.
- [[2026-05-23-hoard-things-you-know-how-to-do]] — Simon Willison, *Agentic Engineering Patterns* Ch. 3. Hoard working examples; recombine them in agent prompts (worked OCR-PDF example).
- [[2026-05-23-ai-should-help-us-produce-better-code]] — Simon Willison, *Agentic Engineering Patterns* Ch. 4. Spend the cheap-code surplus on quality: async refactoring, exploratory prototyping, compound engineering.
- [[2026-05-23-anti-patterns-things-to-avoid]] — Simon Willison, *Agentic Engineering Patterns* Ch. 5. First anti-pattern: filing PRs with unreviewed agent code. Checklist for a good agentic PR.
- [[2026-05-23-how-coding-agents-work]] — Simon Willison, *Agentic Engineering Patterns* Ch. 6. Technical deep-dive on the harness + LLM + tools loop, tokens, token caching, system prompts, reasoning.
- [[2026-05-23-using-git-with-coding-agents]] — Simon Willison, *Agentic Engineering Patterns* Ch. 7. Git is a key tool; core and advanced Git prompts; the "sort out this git mess" universal prompt; history rewriting as editorial work.
- [[2026-05-23-subagents]] — Simon Willison, *Agentic Engineering Patterns* Ch. 8. Subagents preserve root context; three flavors (exploratory, parallel, specialist); Claude Code's `Explore` walked through with a real transcript.
- [[2026-05-26-first-run-the-tests]] — Simon Willison, *Agentic Engineering Patterns*. The four-word session-seeder that forces the agent to discover the test harness and puts it in a testing mindset for the rest of the session.
- [[2026-05-26-red-green-tdd]] — Simon Willison, *Agentic Engineering Patterns*. Test-first development is a "fantastic fit" for agents; the red step (confirming tests fail before implementation) is load-bearing; `Use red/green TDD` is shorthand for the full discipline.
- [[2026-05-26-agentic-manual-testing]] — Simon Willison, *Agentic Engineering Patterns*. Code execution is the defining capability of a coding agent; manual testing patterns (`python -c`, `curl` exploration, Playwright / agent-browser / Rodney for web UIs); Showboat for capturing exec'd commands and outputs as "show your work" artifacts; manual findings feed back into the suite via red/green.
- [[2026-05-26-agentic-engineering-swarms]] — Renuka Kumar & Prashanth Ramagopal (Cisco), guest post on the LangChain blog (2026-04-17). Multi-agent coordination model with Worker / Leader agents on LangGraph + LangSmith + LangMem; A2A and MCP protocols; second sense of *"agentic engineering"*; concrete Cisco pilot numbers (93% debug-time, 65% dev-time reductions; 200+ hours saved across 512 sessions); *"PR review process itself became the bottleneck"*.
- [[2026-05-28-andy-dev-dan-five-pillars]] — Andy Dev Dan, "Top #1 Opportunity for Senior Engineers: Agentic Engineering" (YouTube transcript). Five pillars: agent harness, software factory, extensible software, AFK / always-on agents (gated by tokeconomics), agentic access. Introduces *software factory / ADWs / ZTE*, *tokeconomics* + *token tax*, *custom harness as discipline*. Read with the channel-host / course-business caveat.
- [[2026-05-29-cole-medin-harness-engineering]] — Cole Medin, "Harness Engineering: What Separates Top Agentic Engineers Right Now" (YouTube transcript). The three-layer harness model (LLM → coding-agent → AI layer), the six AI-layer components, harness engineering as an evolution of [[context-engineering]] (= + control + mindset), "every mistake becomes a rule" / system evolution, separate plan/implement/validate sessions, security/stop-validation/lint hooks, and orchestration via the [[ralph-loop|Ralph loop]] + Archon. Read with the Archon-promotion / Google Cloud sponsor caveats.
