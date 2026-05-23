---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/what-is-agentic-engineering/
source_date: 2026-05-23
tags: [agentic-engineering, coding-agents, definitions]
created: 2026-05-23
updated: 2026-05-23
status: developing
---

# What is agentic engineering?

The opening chapter of Simon Willison's *Agentic Engineering Patterns* guide. Defines the term **agentic engineering** as "the practice of developing software with the assistance of coding agents," grounds it in a working definition of **agent** ("software that runs tools in a loop to achieve a goal"), and frames the shift in what the human developer's job becomes when typing code is no longer the bottleneck.

## Key takeaways

- **Agentic engineering** = developing software with the assistance of coding agents. Named examples: [Claude Code](https://code.claude.com/), [OpenAI Codex](https://openai.com/codex/), [Gemini CLI](https://geminicli.com/).
- Willison's working definition of an **agent**: *"Agents run tools in a loop to achieve a goal."* The "agent" is software that calls an LLM with the user's prompt plus a set of tool definitions, executes whichever tools the LLM requests, and feeds the results back into the LLM.
- For coding agents, the critical tool is one that can **execute code**. Code execution is described as "the defining capability that makes agentic engineering possible" — without it, LLM output is "of limited value." With it, agents can iterate toward software that demonstrably works.
- Writing code has never been the *whole* job of a software engineer. The craft has always been figuring out *what* code to write: navigating tradeoffs across many possible solutions for a unique set of circumstances and requirements.
- The human's job in the agentic-engineering era: provide the agent with the right tools, specify problems at the right level of detail, and verify/iterate on results until confident they're robust and credible.
- LLMs don't learn from past mistakes, but **coding agents can** — provided the human deliberately updates the instructions and tool harness based on what's learned.
- Used effectively, coding agents let humans be **more ambitious** with the projects they take on, producing more and better code aimed at more impactful problems.
- Distinction from **vibe coding**: Karpathy coined "vibe coding" in February 2025 to describe prompting LLMs while you "forget that the code even exists" — i.e., unreviewed, prototype-quality output. Willison argues we should *preserve* the original narrow definition rather than letting it expand to cover all LLM-assisted code, because we need language for the difference between unreviewed prototype code and code brought up to production standard.
- The guide itself is explicitly a work in progress; chapters will be added and revised as patterns evolve.

## Connections

- Establishes the core vocabulary for the entire wiki — see [[agentic-engineering]] (the area) and [[coding-agents]] (the topic page that consolidates the agent-loop definition and the vibe-coding distinction).
- The "what's left for humans" framing sets up [[economics-of-code]], which is the subject of [[2026-05-23-writing-code-is-cheap-now]].
- The point that agents *can* learn (through deliberately updated instructions and harnesses) finds its named home in [[compound-engineering]] — the retrospective-driven loop from [[2026-05-23-ai-should-help-us-produce-better-code]]. The complementary artifact-level pattern is [[hoarding-working-examples]] from [[2026-05-23-hoard-things-you-know-how-to-do]].
- Author: [[simon-willison]].

## Raw file

`raw/What is agentic engineering? - Agentic Engineering Patterns.md`
