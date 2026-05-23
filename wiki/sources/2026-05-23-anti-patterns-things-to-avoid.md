---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/anti-patterns/
source_date: 2026-05-23
tags: [agentic-engineering, anti-patterns, code-review, pull-requests, collaboration]
created: 2026-05-23
updated: 2026-05-23
status: developing
---

# Anti-patterns: things to avoid

The fifth chapter of *Agentic Engineering Patterns*. Currently lists a single anti-pattern, which Willison flags as common and deeply frustrating: filing pull requests containing agent-generated code that the author has not reviewed themselves. The chapter doubles as a positive specification of what a *good* agentic PR looks like.

## Key takeaways

- **The anti-pattern: inflicting unreviewed code on collaborators.** *"Don't file pull requests with code you haven't reviewed yourself."* A PR with hundreds or thousands of lines of unreviewed agent output delegates the actual work to the reviewers — who could have prompted an agent themselves. The framing: *"What value are you even providing?"*
- The initial review pass is the author's responsibility, not something to farm out.
- **Characteristics of a good agentic engineering PR** (Willison's checklist):
  1. **The code works, and you are confident it works** — links out to his [Your job is to deliver code that works](https://simonwillison.net/2025/Dec/18/code-proven-to-work/) post.
  2. **The change is small enough to review efficiently** without inflicting too much cognitive load on the reviewer. *Several small PRs beat one big one;* splitting code into separate commits is easy with a coding agent doing the git finagling.
  3. **The PR includes additional context** explaining the higher-level goal the change serves — link relevant issues or specifications.
  4. **You reviewed the PR description too.** Agents write convincing-looking PR descriptions; it's "rude to expect someone else to read text that you haven't read and validated yourself."
- Recommended evidence-of-work-done: notes on manual testing, comments on specific implementation choices, screenshots or video of the feature working. These signals demonstrate to the reviewer that their time will not be wasted digging into the details.

## Connections

- The corollary to [[2026-05-23-ai-should-help-us-produce-better-code]]: that chapter says "evaluate the result in a PR; land it, re-prompt, or throw it away"; this chapter says the PR has to be reviewed by *you* before it lands in front of anyone else. Both are the substance of [[agent-code-review]].
- "Code works, and you know it works" is a direct callback to points 1–2 of the [[economics-of-code|9-point good-code checklist]] from [[2026-05-23-writing-code-is-cheap-now]].
- The "small PRs, agent handles git finagling" point is itself a workflow pattern enabled by the cost collapse in [[economics-of-code]].
- The "PRs as the unit of agent output" framing is implicit in [[refactoring-with-agents]] — async agents produce PRs, and PRs are governed by this chapter.
- Author: [[simon-willison]].

## Raw file

`raw/Anti-patterns things to avoid - Agentic Engineering Patterns.md`
