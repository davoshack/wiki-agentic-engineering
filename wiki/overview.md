---
type: synthesis
tags: [meta, agentic-engineering]
created: 2026-05-22
updated: 2026-05-23
status: developing
sources: 3
---

# Overview

The big-picture synthesis of this wiki — what it knows about [[agentic-engineering]] and the practices, economics, and habits that surround it, drawn together across every source ingested so far.

The LLM keeps this page current. When a new source meaningfully shifts the picture, this page is revised along with the affected area and topic pages.

## Current picture

The wiki currently rests on three foundational chapters of [[simon-willison]]'s *Agentic Engineering Patterns* guide. They establish a coherent base layer that everything else can be built on top of:

- **What the field *is*.** [[agentic-engineering]] is the practice of developing software with the help of [[coding-agents|coding agents]] — software that runs tools in a loop toward a goal, with code execution as the defining tool. Examples: Claude Code, OpenAI Codex, Gemini CLI. (Source: [[2026-05-23-what-is-agentic-engineering]].)
- **Why it matters.** Coding agents collapse the cost of producing code to near zero, which invalidates many engineering intuitions built around code being expensive. But *good code* — defined by a 9-point checklist (works, tested, documented, simple, handles errors, etc.) — is still expensive, and meeting that bar remains the human's responsibility. See [[economics-of-code]]. (Source: [[2026-05-23-writing-code-is-cheap-now]].)
- **How to work with it.** Two early habits stand out. *"Fire off a prompt anyway"* — run the experiment that would previously have failed the cost/benefit test. And *[[hoarding-working-examples|hoard working examples]]* — keep a personal collection of runnable code that proves what you know how to do, then point agents at it via `curl`, filesystem search, or `git clone`. The payoff: a useful trick only has to be figured out once. (Source: [[2026-05-23-hoard-things-you-know-how-to-do]].)

A vocabulary point worth holding onto: **agentic engineering ≠ vibe coding**. Vibe coding (Karpathy, Feb 2025) means unreviewed, prototype-quality LLM output; agentic engineering covers the full range up through production-grade work where the human verifies, tests, and is responsible for outcomes.

The picture is one author deep right now. Willison is a credible primary source, but the wiki will get more interesting as sources from other practitioners, counterpoints, and empirical studies arrive.

## Open questions

- **How do verification and review work at agent speed?** Old code-review intuitions assume a serial human author. Parallel asynchronous agents change the shape of the problem.
- **Which old micro-tradeoffs flipped, and which didn't?** "Default-yes on every refactor" presumably isn't right either. We need better heuristics than the binary.
- **What does updating the agent harness look like in practice?** Willison flags that agents *can* learn across sessions — through deliberate updates to instructions and tools — but the sources don't yet describe what that workflow looks like day-to-day.
- **How do you organize a hoard for agent consumption?** Public/searchable vs. local-only, snippet vs. repo, code vs. prompts/evals/transcripts.
- **Are the patterns portable across Claude Code, Codex, Gemini CLI?** All sources so far come from a Claude-Code-leaning practitioner.
- **What other chapters of *Agentic Engineering Patterns* and what counter-perspectives are worth ingesting next?** Worth tracking Willison's table of contents and seeking adversarial views.
