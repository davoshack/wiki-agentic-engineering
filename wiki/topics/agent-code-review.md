---
type: topic
tags: [agentic-engineering, code-review, pull-requests, collaboration, anti-patterns]
created: 2026-05-23
updated: 2026-05-26
status: developing
sources: 3
---

# Agent code review

The human responsibility that sits between an agent producing code and a teammate being asked to read it. The first-pass review is the author's job, not the reviewer's — and the artifacts of that review (manual-test notes, screenshots, commentary) are the trust signals that make agentic PRs collaborate well.

## Synthesis

### The anti-pattern to avoid

[[simon-willison]]'s sharpest claim in [[2026-05-23-anti-patterns-things-to-avoid]]: **don't file pull requests with code you haven't reviewed yourself.** Opening a PR with hundreds or thousands of lines of unreviewed agent output delegates the actual work to the reviewers, who could have prompted an agent themselves. *"What value are you even providing?"*

This isn't a workflow preference; it's a contract. Once you put code up for review you are asserting that it is ready for other people to spend their time on it. The initial review pass is yours.

### What a good agentic PR looks like

Willison's positive checklist from the same chapter:

1. **The code works, and you are confident it works.** This is points 1–2 of the [[economics-of-code|9-point good-code definition]] — *it works*, and *we know it works*. Linked supporting essay: [Your job is to deliver code that works](https://simonwillison.net/2025/Dec/18/code-proven-to-work/).
2. **The change is small enough to be reviewed efficiently.** Several small PRs beat one big one. Splitting code into separate commits is easy now that an agent can do the git finagling for you — so there's no excuse for the giant PR.
3. **The PR includes additional context** explaining the higher-level goal — link the relevant issues or specs. The agent has the local view; the reviewer needs the global view.
4. **You reviewed the PR description.** Agents write convincing-looking PR descriptions. It is "rude to expect someone else to read text that you haven't read and validated yourself."

### Evidence of work done

Because it's so easy now to drop unreviewed code on other people, Willison recommends including explicit signals of the review pass:

- Notes on how you manually tested the change.
- Comments on specific implementation choices and why you accepted them.
- Screenshots or short videos of the feature working.

These are read as a promise to the reviewer that their time will not be wasted digging into details you skipped past.

[[2026-05-26-agentic-manual-testing]] gives this requirement a concrete substrate. Willison's [Showboat](https://github.com/simonw/showboat) records a Markdown document of an agentic manual-testing run, with `note`, `exec` (records command + real output, designed to discourage the agent from writing what it *hoped* had happened), and `image` (e.g. screenshots from Rodney) — precisely the evidence-of-work-done signals this checklist asks for, in artifact form. The same chapter also pairs nicely with [[agentic-testing]]'s automated side: "the tests pass" is itself an evidence signal, and the *manual finding → red/green → permanent test* loop produces a tighter PR than either mode alone.

### The relationship to async refactoring

The async-agent workflow described in [[refactoring-with-agents]] produces PRs as its primary output — so this topic is the *governance layer* on top of that pattern. Asynchronous code production does not imply asynchronous human responsibility; the author still owns the first review pass regardless of how the code was produced.

## Open questions

- How does this scale to a team where multiple people are running async agents in parallel and PRs are piling up? Are there review-load patterns that work?
- What review checklist or tooling can systematize the "evidence of work done" requirement so it's a default, not a virtue?
- Where does AI-assisted *reviewing* fit (agent reading PR diffs, flagging issues)? Does it ease the load or invite a new layer of unreviewed-agent-on-unreviewed-agent collisions?
- Are there anti-patterns Willison hasn't yet listed in this chapter that are worth tracking ahead of him? (The chapter is explicitly a stub with one entry so far.)

## Sources

- [[2026-05-23-anti-patterns-things-to-avoid]]
- [[2026-05-23-ai-should-help-us-produce-better-code]]
- [[2026-05-26-agentic-manual-testing]]
