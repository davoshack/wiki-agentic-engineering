---
type: synthesis
tags: [meta, agentic-engineering]
created: 2026-05-22
updated: 2026-05-23
status: developing
sources: 8
---

# Overview

The big-picture synthesis of this wiki — what it knows about [[agentic-engineering]] and the practices, economics, mechanics, and habits that surround it, drawn together across every source ingested so far.

The LLM keeps this page current. When a new source meaningfully shifts the picture, this page is revised along with the affected area and topic pages.

## Current picture

The wiki currently rests on the first eight chapters of [[simon-willison]]'s *Agentic Engineering Patterns* guide. Together they make a self-consistent argument across four layers:

### 1. What the field *is*

[[agentic-engineering]] is the practice of developing software with the help of [[coding-agents|coding agents]] — software that runs tools in a loop toward a goal, with code execution as the defining tool. Examples: Claude Code, OpenAI Codex, Gemini CLI; the **asynchronous** flavor (Gemini Jules, Codex web, Claude Code on the web) is called out as its own pattern. The vocabulary point worth holding: agentic engineering ≠ **vibe coding** (Karpathy, Feb 2025 — unreviewed prototype-quality LLM output); agentic engineering covers the full range up through production work where the human verifies, tests, and is responsible for outcomes. (Sources: [[2026-05-23-what-is-agentic-engineering]].)

### 2. How it actually works

Under the hood, a coding agent is **a harness wrapping an LLM, extended with a system prompt and a set of callable tools, run in a loop.** That's most of the architecture; a simple version is a few dozen lines on top of an LLM API. [[agent-architecture]] details the pieces: LLMs work on tokens (providers charge per token, context windows top out around 1M but quality often degrades past 200K), chat templated prompts are a thin wrapper around stateless completion (so the harness replays the whole conversation each turn), **token caching** is the central cost optimization (and the reason coding agents deliberately avoid mutating earlier conversation), tools are functions called via a parsed-out `<tool>...</tool>` protocol, **system prompts** are often hundreds of lines and are the surface compound engineering writes to, and **reasoning/thinking mode** spends extra tokens talking through the problem and is particularly useful for debugging. (Source: [[2026-05-23-how-coding-agents-work]].)

The **context-window constraint** is what motivates [[subagents]]: a subagent is a fresh copy of the agent with a new context window, dispatched as a tool call. Three flavors — exploratory (Claude Code's `Explore` runs every new task), parallel (often using cheaper/faster models like Claude Haiku for independent file edits), and specialist (code reviewer, test runner, debugger — custom system prompts and/or tools). Cautionary note: the value is **context preservation**, not maximalist orchestration. (Source: [[2026-05-23-subagents]].)

### 3. Why it matters economically

Coding agents collapse the per-task cost of producing code to near zero, which invalidates many engineering intuitions built around code being expensive. But *good code* — defined by a 9-point checklist (works, tested, documented, simple, handles errors, etc.) — is still expensive, and meeting that bar remains the human's responsibility. See [[economics-of-code]]. Two cost layers actually matter: **engineering time** (the headline story) and **tokens** (the layer that token caching and subagents are designed to keep low). (Sources: [[2026-05-23-writing-code-is-cheap-now]], reinforced by the cost mechanics in [[2026-05-23-how-coding-agents-work]] and [[2026-05-23-subagents]].)

### 4. What to spend the surplus on — quality, plus what *not* to do

Two concrete productive uses: eliminate the class of technical debt that is "simple but time-consuming" using async agents in worktrees and PRs ([[refactoring-with-agents]]), and run cheap parallel **exploratory prototypes** to make better technology choices. The mechanism for making the gains stick is [[compound-engineering]] — end each project with a retrospective whose output is **edits to the system prompt and tool harness** for future agent runs (term from Shipper & Klaassen at Every). The first named **anti-pattern**: filing PRs containing agent-generated code you haven't reviewed yourself. Async refactoring does not mean async human responsibility; [[agent-code-review]] is the governance layer over [[refactoring-with-agents]]. (Sources: [[2026-05-23-ai-should-help-us-produce-better-code]], [[2026-05-23-anti-patterns-things-to-avoid]].)

### Cross-cutting habits

Two complementary habits sit underneath everything:

- **[[hoarding-working-examples|Hoard working examples]]** — keep a personal collection of runnable code that proves what you know how to do; point agents at it via `curl`, filesystem search, or `git clone`. Parallel subagents on cheap models accelerate hoard growth.
- **[[git-with-agents|Use Git ambitiously]]** — agents are fluent in basic *and* advanced Git, which removes the recall cost. `git bisect` becomes routine because agents handle the test-condition boilerplate. "Review changes made today" is a cheap session-seeding move. History rewriting is editorial work, not falsification. Frontier-model commit-message taste is often good enough to delegate. (Source: [[2026-05-23-using-git-with-coding-agents]].)

Hoarding accumulates *artifacts* (working code); [[compound-engineering]] accumulates *instructions* (how the agent should behave, encoded as system-prompt and harness edits). Both turn one-time effort into permanent leverage.

### State of the picture

Still one author deep. Willison is a credible primary source, but the wiki will get more interesting as sources from other practitioners, counterpoints, and empirical studies arrive. The most-load-bearing external references flagged so far: Shipper & Klaassen's [Every post on Compound Engineering](https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents); the linked [OpenAI Codex system prompt](https://github.com/openai/codex/blob/rust-v0.114.0/codex-rs/core/templates/model_instructions/gpt-5.2-codex_instructions_template.md) as a concrete public example of what a working system prompt looks like; vendor subagent docs (Codex, Claude, Gemini CLI, Mistral Vibe, OpenCode, VS Code, Cursor).

## Open questions

- **How do verification and review work at agent speed?** Old code-review intuitions assume a serial human author. Parallel asynchronous agents and parallel subagents change the shape of the problem. [[agent-code-review]] is the start of an answer; the team-scale version is still open.
- **Which old micro-tradeoffs flipped, and which didn't?** "Default-yes on every refactor" presumably isn't right either. The "simple but time-consuming" debt class is a clear *flipped* yes; less clear what's still a no.
- **What does updating the agent harness look like day-to-day?** [[compound-engineering]] names the practice and we now know the substrate is the system prompt + tool harness + repo-level instruction files. Still open: where lessons should live by default, how the system prompt is pruned, what makes a good "compound step."
- **How do you organize a hoard for agent consumption?** Public/searchable vs. local-only, snippet vs. repo, code vs. prompts/evals/transcripts.
- **Are the patterns portable across Claude Code, Codex, Gemini CLI, Mistral Vibe, OpenCode, VS Code, Cursor?** Subagent docs exist for all of them but the implementations differ; vendor-portability isn't yet established.
- **When does reasoning mode pay off vs. cost too much?** The dial exists; the right setting per task class isn't yet characterized.
- **What's the safe envelope for history-rewriting and `git reset`-style operations on shared branches?** Local rewriting is fine; shared-branch rewrites are dangerous. Agents need clear constraints.
- **What other anti-patterns belong in [[agent-code-review]]?** Willison's anti-patterns chapter currently lists only one; the gap is itself useful to track.
- **What other chapters of *Agentic Engineering Patterns* and what counter-perspectives are worth ingesting next?** The TOC keeps growing; deliberate adversarial views are still missing.
