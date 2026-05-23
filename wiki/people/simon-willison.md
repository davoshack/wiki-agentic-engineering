---
type: person
tags: [agentic-engineering, author, primary-source]
created: 2026-05-23
updated: 2026-05-23
status: developing
sources: 3
---

# Simon Willison

British software engineer and writer; co-creator of Django; creator of [Datasette](https://datasette.io/) and the [`llm`](https://llm.datasette.io/) CLI. One of the most-cited public commentators on practical LLM use, and the author of the *Agentic Engineering Patterns* guide that this wiki is currently built around.

## Synthesis

Willison's writing is the wiki's initial entry point into agentic engineering. His perspective has a few consistent features that are useful to remember when reading his pages here:

- **Practitioner, not theorist.** Claims tend to be grounded in working code he has actually shipped — his blog, [TIL blog](https://til.simonwillison.net/), 1000+ public [GitHub repos](https://github.com/simonw), and the [tools.simonwillison.net](https://tools.simonwillison.net/) collection are all primary evidence for the patterns he describes.
- **Definitional discipline.** He invests in tight, defensible definitions of contested terms and resists letting them drift. The chapters ingested so far define [[coding-agents|agent and coding agent]] precisely, defend the original narrow meaning of *vibe coding* against expansion, and decompose "good code" into a 9-point checklist rather than leaving it as a vibe.
- **Continuity with pre-LLM craft.** Several of his patterns are explicitly framed as extensions of advice that worked before LLMs (e.g., [[hoarding-working-examples|hoarding working examples]]). The LLM era amplifies the value of habits that were already worth having.
- **The guide is a living document.** *Agentic Engineering Patterns* is explicitly a work in progress; he expects to revise existing chapters as the field evolves.

## Open questions

- What other chapters of *Agentic Engineering Patterns* exist or are planned? Worth tracking the guide's table of contents for additions.
- Where does Willison stand on disputed questions in the field (e.g., evaluation, agent autonomy levels, security boundaries for tool use)?
- Which of his patterns are specific to Claude Code vs. genuinely agent-agnostic?

## Sources

- [[2026-05-23-what-is-agentic-engineering]]
- [[2026-05-23-writing-code-is-cheap-now]]
- [[2026-05-23-hoard-things-you-know-how-to-do]]
