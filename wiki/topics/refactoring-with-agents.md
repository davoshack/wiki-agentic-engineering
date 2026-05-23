---
type: topic
tags: [agentic-engineering, refactoring, technical-debt, async-agents, workflow]
created: 2026-05-23
updated: 2026-05-23
status: developing
sources: 1
---

# Refactoring with agents

Using asynchronous coding agents to eliminate the category of technical debt that is "simple but time-consuming" — large-but-mechanical changes that historically got punted because they couldn't compete with more urgent work for human time.

## Synthesis

### The debt class agents are made for

[[simon-willison]]'s argument in [[2026-05-23-ai-should-help-us-produce-better-code]]: a major category of technical debt is *simple-but-time-consuming* — changes that are conceptually easy and well-understood, but require touching many files, and that's exactly why they don't get done. Concrete examples he gives:

- An original API design that doesn't cover an edge case that emerged later — fixing it would require changing dozens of call sites, so a slightly different near-duplicate API gets added instead.
- A poor naming choice early on (his example: "teams" instead of "groups") that only gets cleaned up in the UI because doing it everywhere is too much work.
- Duplicate-but-slightly-different functionality grown over time that needs combining and reconciling.
- A single file grown to several thousand lines that should be split into separate modules.

These are *ideal* tasks for coding agents. The work is mechanical, the correctness criterion is clear, and a human is not the best use of time on them.

### The asynchronous workflow

Willison explicitly favors **asynchronous coding agents** for refactoring jobs so that the work doesn't interrupt foreground flow. Named tools:

- [Gemini Jules](https://jules.google.com/)
- [OpenAI Codex web](https://developers.openai.com/codex/cloud/)
- [Claude Code on the web](https://code.claude.com/docs/en/claude-code-on-the-web)

The pattern: fire up an async agent in a branch or worktree, leave it to churn in the background, evaluate the result later as a pull request. Three possible outcomes:

- **Good** → land it.
- **Almost there** → prompt the agent again with corrections.
- **Bad** → throw it away.

The "throw it away" branch is what makes the workflow economic: the cost of these code improvements has dropped so low that failed attempts are cheap. Willison's framing: *"we can afford a zero tolerance attitude to minor code smells and inconveniences."*

### Constraints on the pattern

The PR produced by the async agent is bound by the rules in [[agent-code-review]] — *you* are responsible for reviewing the agent's output before others see it. Asynchronous refactoring does not mean asynchronous human responsibility.

It's also worth holding this pattern next to [[economics-of-code|the broader cost story]]: the "fire off a prompt anyway" heuristic from chapter 2 generalizes; refactoring is just the most defensible case of it, because the value is well-understood even when the work is unglamorous.

## Open questions

- What kinds of refactors are *not* well-suited to async agents — those needing real-time judgment, deep architectural rework, performance tuning that needs profiling? Where's the line?
- How do you write the prompt for a multi-file refactor so the agent doesn't drift halfway through? Is one-shot the right shape, or is it better to ask for a plan first?
- How do you safely run several async refactor agents in parallel against the same codebase without merge-conflict chaos?
- What's the right cadence — opportunistic (whenever a smell shows up) or batched (a weekly "debt clearing" session)?

## Sources

- [[2026-05-23-ai-should-help-us-produce-better-code]]
