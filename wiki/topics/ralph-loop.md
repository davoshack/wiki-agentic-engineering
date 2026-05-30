---
type: topic
tags: [agentic-engineering, orchestration, ralph-loop, harness-engineering, automation, software-factory]
created: 2026-05-29
updated: 2026-05-29
status: stub
sources: 1
---

# Ralph loop

A minimal, script-based pattern for **automating the orchestration of many coding-agent sessions**: a `while` loop that repeatedly runs fresh coding-agent sessions against a large scope of work, splitting it into tasks and handing artifacts forward, until a completion marker says the work is done. Attributed to [[geoffrey-huntley|Geoffrey Huntley]]; introduced to the wiki by [[cole-medin]] as the worked example of an **agent harness**.

## Synthesis

The Ralph loop is the simplest concrete instance of the "peak evolution" of [[agent-harness-engineering|harness engineering]] in [[2026-05-29-cole-medin-harness-engineering]] — moving from *engineering a single session's AI layer* to *orchestrating many sessions automatically*. [[cole-medin|Cole Medin]] presents it as deliberately un-fancy ("I'm not going to get too technical"): it's just a script.

The mechanics, as described:

1. **Give it a large scope** — a "massive PRD" / spec listing the items you want built.
2. **It splits the scope into individual tasks** and runs **coding-agent sessions one at a time** to handle them.
3. **It accumulates a log** across iterations (iteration one, two, three…), so progress is visible and resumable.
4. **The only exit condition is a completion marker** — a `done.txt` (Cole says `done.ext`) file the agent writes once it is confident the implementation *and* all validation are complete (e.g. "all 8 spec items from the original prompt are done"). The main `while` loop exits *only* when that marker exists.

The motivating constraint is the same one behind [[subagents]] and Cole's separate-session-per-phase advice: **a single session handed too much work gets token-overwhelmed and "falls flat on its face,"** no matter how good the AI layer is. Splitting the scope across many focused sessions keeps each one efficient; wrapping them in a loop removes the need to **babysit** the agent through a long task. Geoffrey Huntley is credited as the originator and "one of the pioneers" of this automate-the-stringing-together idea; the model is harness-agnostic (Claude Code, Codex, any coding assistant).

### Where it sits

- **A concrete [[software-factory]].** Andy Dev Dan's "dark factory" / ADWs describe the same *plan → implement → review → ship* pipeline at the conceptual level; the Ralph loop is a minimal, runnable realization of it. Two independent practitioner voices ([[andy-dev-dan]], [[cole-medin]]) now describe this orchestration shape.
- **Built with [[agent-harness-engineering|harness-engineering]] primitives.** The loop is "control" — the one capability Cole says genuinely distinguishes harness engineering from [[context-engineering]]. [[cole-medin|Cole's]] **Archon** is pitched as a tool for building Ralph-loop-style harnesses customized to your own process.
- **Evolution from [[subagents]].** Cole frames orchestrating *actual coding-agent sessions that hand off to each other* as "a true evolution from sub agents" — sessions are heavier and more independent than within-session sub-agent dispatch.
- **Solo-scale analog of [[multi-agent-coordination]].** Kumar & Ramagopal's Leader/Worker swarm is the org-scale, observability-and-memory-backed version; the Ralph loop is the single-engineer, single-script version of the same "many focused agents, coordinated" idea.
- **Verification is the gate.** The `done.txt` exit depends on the agent's own validation passing — connecting to [[agentic-testing]]'s stop-validation hooks and to the [[agent-code-review]] question of which checks can be trusted to an agent vs. must stay human.

## Open questions

- **No primary source.** The entire account is secondhand via Cole. Huntley's own write-up would clarify the real failure modes — e.g. how it avoids looping forever, how task-splitting actually decides boundaries, what stops the agent from writing `done.txt` prematurely.
- **Premature-completion risk.** The exit hinges on the agent being "confident" validation is complete. What deterministic checks (tests, lint, typecheck — cf. [[agentic-testing]]) gate the marker, and what happens when the agent is confidently wrong?
- **Cost / runaway behavior.** A loop of full coding-agent sessions against a big PRD is exactly the kind of always-on consumption [[tokeconomics]] warns about ("90% of agent cron jobs… burning cash"). When does a Ralph loop pay off vs. just doing the work in-session?
- **Human review at loop speed.** If the loop produces PRs autonomously, where does the [[agent-code-review]] gate sit — per task, per loop, or at the end? This is the [[practitioner-discipline-vs-control-plane|PR-review-as-bottleneck]] question in miniature.

## Sources

- [[2026-05-29-cole-medin-harness-engineering]]
</content>
