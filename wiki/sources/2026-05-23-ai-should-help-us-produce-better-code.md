---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/better-code/
source_date: 2026-05-23
tags: [agentic-engineering, technical-debt, refactoring, compound-engineering, exploratory-prototyping]
created: 2026-05-23
updated: 2026-05-23
status: developing
---

# AI should help us produce better code

The fourth chapter of *Agentic Engineering Patterns*. Direct rebuttal to the worry that AI tools will degrade code quality: Willison argues that shipping worse code with agents is *a choice*, and proposes three concrete ways agents should be used to push quality *up* — eliminating "simple but time-consuming" technical debt asynchronously, running cheap parallel prototypes to make better technology choices, and building a feedback loop ("compound engineering") that improves agent runs over time.

## Key takeaways

- **Quality is a choice, not an inevitable casualty.** If adopting coding agents demonstrably reduces the quality of code and features, the right response is to diagnose what in the process is hurting output and fix it. *"Shipping worse code with agents is a choice. We can choose to ship code that is better instead."*
- **Technical debt mitigation is best done by not taking it on.** A common category of technical debt is "simple but time-consuming" — and historically these get punted because more urgent work crowds them out. Examples Willison lists:
  - An original API design that doesn't cover a case that emerged later — fixing it requires changing dozens of call sites, so a near-duplicate API gets added instead.
  - A poor naming choice early on (his example: "teams" instead of "groups") that only gets cleaned up in the UI because doing it everywhere is too much work.
  - Duplicate-but-slightly-different functionality grown over time that needs combining.
  - A single file grown to several thousand lines that should be split.
- **Coding agents are ideal for this category.** Fire up an agent, tell it what to change, leave it churning in a branch or worktree. He favors **asynchronous coding agents** for these jobs — explicitly named: [Gemini Jules](https://jules.google.com/), [OpenAI Codex web](https://developers.openai.com/codex/cloud/), [Claude Code on the web](https://code.claude.com/docs/en/claude-code-on-the-web) — so refactor work doesn't interrupt foreground flow on the laptop. Workflow: evaluate the result in a PR; land it, re-prompt, or throw it away.
- *"The cost of these code improvements has dropped so low that we can afford a zero tolerance attitude to minor code smells and inconveniences."*
- **AI tools let us consider more options.** A major source of technical debt is *planning-step* mistakes — missing an obvious simple solution, or picking the wrong technology. LLMs help surface options that didn't make the radar; they tend to suggest **[Boring Technology](https://boringtechnology.club/)** because that's what dominates their training data, which he frames as a feature, not a bug.
- **Exploratory prototyping** is the strongest version of this: the best way to make a confident technology choice is to *prove* fit with a prototype. His example: "Is Redis a good choice for the activity feed on a site which expects thousands of concurrent users?" — best answered by wiring up a simulation and running a load test. Coding agents can build that simulation from a single well-crafted prompt, dropping the cost to near zero — cheap enough that you can run **multiple experiments in parallel** and pick the winner.
- **Compound engineering** (term from Dan Shipper and Kieran Klaassen at Every; original write-up: [Compound Engineering: How Every codes with agents](https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents)). Every coding project ends with a retrospective — the **compound step** — that documents what worked, feeding it forward into instructions for future agent runs. The loop is: agents follow instructions → instructions evolve from experience → future runs get better.
- Bigger picture: small quality improvements compound. Time-consuming quality work used to be hard to justify; now there's no excuse not to invest in quality *while* shipping features. *"Coding agents mean we can finally have both."*

## Connections

- Direct extension of [[2026-05-23-writing-code-is-cheap-now]]: that chapter laid out the economic shift and the 9-point "good code" definition; this one prescribes how to spend the cheap-code surplus to *raise* quality. Together they form the spine of [[economics-of-code]].
- The async-refactor pattern, the worktree workflow, and the "simple but time-consuming" debt taxonomy are the substance of [[refactoring-with-agents]].
- Compound engineering is concrete content for [[compound-engineering]] — and it gives a name to the "agents *can* learn if you deliberately update the harness" thread from [[2026-05-23-what-is-agentic-engineering]].
- Exploratory prototyping connects to [[hoarding-working-examples]]: a successful prototype isn't just a decision input, it's a hoardable artifact.
- The "evaluate the result in a PR" workflow is the precondition that [[2026-05-23-anti-patterns-things-to-avoid]] then constrains — the PR is meant to be reviewed by *you* before others.
- Author: [[simon-willison]].

## Raw file

`raw/AI should help us produce better code - Agentic Engineering Patterns.md`
