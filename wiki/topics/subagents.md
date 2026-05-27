---
type: topic
tags: [agentic-engineering, subagents, context-management, parallelism, specialist-agents]
created: 2026-05-23
updated: 2026-05-26
status: developing
sources: 2
---

# Subagents

A subagent is a fresh copy of the coding agent, dispatched by the parent agent with a new context window to handle a specific task. The principal value is **context preservation** — keeping the parent's valuable root context free of the tokens spent on exploration, parallel edits, or verbose tool output.

## Synthesis

### The constraint that motivates subagents

[[simon-willison]] makes the case in [[2026-05-23-subagents]]: LLMs are limited by their **context window**. These limits "generally top out at around 1,000,000, and benchmarks frequently report better quality results below 200,000" — and they have not grown much over the past two years, even as model capabilities have. Carefully managing what's in context is critical to getting good results.

A subagent is the principal architectural response: *"When a coding agent uses a subagent it effectively dispatches a fresh copy of itself to achieve a specified goal, with a new context window that starts with a fresh prompt."* Mechanically it works like any other tool call — the parent dispatches, the subagent runs, the parent receives the result and continues.

### Three flavors

**1. Exploratory (parent pauses).** The simplest case. The parent dispatches one subagent and waits for the result. Claude Code's `Explore` subagent is the canonical example — Claude Code runs it whenever a new task starts against an existing repo, to map the codebase and surface what's relevant. The starter prompt is structured (specific keywords, specific directories, specific file types), and the response is a comprehensive summary the parent can act on without ever loading the whole repo itself.

Willison notes: *"It's interesting to see models prompt themselves in this way — they generally have good taste in prompting strategies."* The principal advantage: the exploration happens in fresh context, so it doesn't spend any of the parent's available tokens on intermediate findings.

**2. Parallel.** The parent dispatches **several subagents at the same time**, often using **faster and cheaper models** (Willison names Claude Haiku) to accelerate. For editing many files where the files don't depend on each other, this is a significant speed boost. Sample prompt: *"Use subagents to find and update all of the templates that are affected by this change."* This is the same economic logic as the "fire off a prompt anyway" heuristic from [[economics-of-code]], applied at agent scale: cheap parallel attempts, accept the ones that work.

**3. Specialist.** Some coding agents allow subagents to run with **custom system prompts** and/or **custom tools**, so each subagent can take on a specific role:
- **Code reviewer** — reviews code, flags bugs, feature gaps, design weaknesses. Automatable companion to the human review process in [[agent-code-review]].
- **Test runner** — runs the test suite. *Particularly valuable when the suite is large and verbose, because the subagent can hide the full output from the main agent and report back only failures.* This is a context-preservation play, not just a parallelism one.
- **Debugger** — specialized in isolating reproduction steps and root causes; spends its token allowance reasoning through the codebase and running snippets.

### Subagents vs. multi-agent swarms — same word, different unit

The word *"swarm"* gets used at two different scales in the literature and the wiki keeps them distinct.

- **Willison's subagents** (this page) are *fresh copies of the same coding agent*, dispatched **by a parent agent within a single user-driven session**, primarily to **preserve root context**. They're transient: they live and die inside the session that spawned them.
- **[[multi-agent-coordination|Worker-Agent swarms]]** ([[2026-05-26-agentic-engineering-swarms|Kumar & Ramagopal]]) are *persistent, role-differentiated* agents (development, testing, debugging, ops) coordinated by a **Leader Agent** across sessions and team boundaries. They communicate via the A2A protocol and accumulate long-term state in LangMem.

The two patterns are not in conflict — they sit at different organizational scales. A Worker Agent in a Kumar/Ramagopal swarm might internally dispatch Willison-style subagents (parallel file edits, specialist test runner, etc.) to do its work. *Parent → subagent* is the within-session axis; *Leader ↔ Worker → other Worker* is the cross-session, cross-team axis.

### Cautionary note

*"While it can be tempting to go overboard breaking up tasks across dozens of different specialist subagents, it's important to remember that the main value of subagents is in preserving that valuable root context and managing token-heavy operations. Your root coding agent is perfectly capable of debugging or reviewing its own output provided it has the tokens to spare."* The right question to ask before spinning out a specialist: *will this operation eat enough of the root context to hurt the parent's ability to finish the task?* If not, the simpler architecture wins.

### Where this fits

- This page is the practical-pattern layer over the **context-limit** constraint introduced in [[agent-architecture]] (from [[2026-05-23-how-coding-agents-work]]).
- The Explore-subagent's role at session start overlaps with the "review changes made today" pattern in [[git-with-agents]] — both are cheap context-loading at session start, one via a fresh subagent and one via `git log` into the root context.
- Specialist test-runner subagents are particularly interesting in light of the verbose-output problem common to large test suites — they're a way to consume a lot of tool output without polluting the parent's context.
- Vendor support is broad: official subagent docs exist for [OpenAI Codex](https://developers.openai.com/codex/subagents/), [Claude](https://code.claude.com/docs/en/sub-agents), [Gemini CLI](https://geminicli.com/docs/core/subagents/), [Mistral Vibe](https://docs.mistral.ai/mistral-vibe/agents-skills#agent-selection), [OpenCode](https://opencode.ai/docs/agents/), [VS Code](https://code.visualstudio.com/docs/copilot/agents/subagents), and [Cursor](https://cursor.com/docs/subagents).

## Open questions

- How do the different vendors' subagent implementations actually differ? Willison links the docs but doesn't compare them.
- For parallel subagents, what's the right way to detect "these files actually *do* depend on each other" before dispatching, to avoid conflicts on merge back?
- For specialist subagents, where do the custom system prompts and tools live? This is the per-role version of the harness-update story from [[compound-engineering]].
- Are there subagent patterns beyond Willison's three flavors that are emerging — e.g., research subagents that consult external sources, evaluator subagents that score parent output?
- The "main value is context preservation" framing is strong but the parallel-subagents-with-Haiku case is partly about latency, not context. Is there a clean way to think about when each motivation dominates?

## Sources

- [[2026-05-23-subagents]]
- [[2026-05-26-agentic-engineering-swarms]]
