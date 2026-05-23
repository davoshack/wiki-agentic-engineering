---
type: synthesis
tags: [meta, agentic-engineering]
created: 2026-05-22
updated: 2026-05-23
status: developing
sources: 5
---

# Overview

The big-picture synthesis of this wiki — what it knows about [[agentic-engineering]] and the practices, economics, and habits that surround it, drawn together across every source ingested so far.

The LLM keeps this page current. When a new source meaningfully shifts the picture, this page is revised along with the affected area and topic pages.

## Current picture

The wiki currently rests on the first five chapters of [[simon-willison]]'s *Agentic Engineering Patterns* guide. Together they make a self-consistent argument with four moves:

- **What the field *is*.** [[agentic-engineering]] is the practice of developing software with the help of [[coding-agents|coding agents]] — software that runs tools in a loop toward a goal, with code execution as the defining tool. Examples: Claude Code, OpenAI Codex, Gemini CLI; the **asynchronous** flavor (Gemini Jules, Codex web, Claude Code on the web) is called out as its own pattern. (Source: [[2026-05-23-what-is-agentic-engineering]].)
- **Why it matters.** Coding agents collapse the cost of producing code to near zero, which invalidates many engineering intuitions built around code being expensive. But *good code* — defined by a 9-point checklist (works, tested, documented, simple, handles errors, etc.) — is still expensive, and meeting that bar remains the human's responsibility. See [[economics-of-code]]. (Source: [[2026-05-23-writing-code-is-cheap-now]].)
- **What to spend the surplus on — quality, not slop.** Two concrete uses: eliminate the class of technical debt that is "simple but time-consuming" using async agents in worktrees and PRs ([[refactoring-with-agents]]), and run cheap parallel **exploratory prototypes** to make better technology choices. The mechanism for making the gains stick is [[compound-engineering]] — end each project with a retrospective whose output is updated instructions for future agent runs (term from Shipper & Klaassen at Every). (Source: [[2026-05-23-ai-should-help-us-produce-better-code]].)
- **What not to do.** The first named anti-pattern is filing PRs containing agent-generated code you haven't reviewed yourself. Async refactoring does not mean async human responsibility; [[agent-code-review]] is the governance layer over [[refactoring-with-agents]]. (Source: [[2026-05-23-anti-patterns-things-to-avoid]].)

A complementary habit underneath all of this: **[[hoarding-working-examples|hoard working examples]]** — keep a personal collection of runnable code that proves what you know how to do, then point agents at it via `curl`, filesystem search, or `git clone`. The payoff is that a useful trick only has to be figured out once. Hoarding and compound engineering are the same idea applied to different layers: hoarding accumulates *artifacts* (working code), compound engineering accumulates *instructions* (how the agent should behave). Both turn one-time effort into permanent leverage.

A vocabulary point worth holding onto: **agentic engineering ≠ vibe coding**. Vibe coding (Karpathy, Feb 2025) means unreviewed, prototype-quality LLM output; agentic engineering covers the full range up through production-grade work where the human verifies, tests, and is responsible for outcomes.

The picture is still one author deep. Willison is a credible primary source, but the wiki will get more interesting as sources from other practitioners, counterpoints, and empirical studies arrive. The most-load-bearing external reference flagged so far is Shipper & Klaassen's [Every post on Compound Engineering](https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents).

## Open questions

- **How do verification and review work at agent speed?** Old code-review intuitions assume a serial human author. Parallel asynchronous agents change the shape of the problem. [[agent-code-review]] is the start of an answer; the team-scale version is still open.
- **Which old micro-tradeoffs flipped, and which didn't?** "Default-yes on every refactor" presumably isn't right either. The "simple but time-consuming" debt class is a clear *flipped* yes; less clear what's still a no.
- **What does updating the agent harness look like day-to-day?** [[compound-engineering]] names the practice; the operational details — where instructions live, how they're pruned, what makes a good "compound step" — are not yet specified in the sources.
- **How do you organize a hoard for agent consumption?** Public/searchable vs. local-only, snippet vs. repo, code vs. prompts/evals/transcripts.
- **Are the patterns portable across Claude Code, Codex, Gemini CLI?** All sources so far come from a Claude-Code-leaning practitioner, though async-agent recommendations span vendors.
- **What other anti-patterns belong in [[agent-code-review]]?** Willison's chapter currently lists only one; tracking the gap is itself useful.
- **What other chapters of *Agentic Engineering Patterns* and what counter-perspectives are worth ingesting next?** Worth tracking Willison's table of contents and seeking adversarial views.
