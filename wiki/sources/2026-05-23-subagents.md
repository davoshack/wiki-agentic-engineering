---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/subagents/
source_date: 2026-05-23
tags: [agentic-engineering, subagents, context-management, parallelism, specialist-agents]
created: 2026-05-23
updated: 2026-05-23
status: developing
---

# Subagents

The eighth chapter of *Agentic Engineering Patterns*. Frames subagents as the principal mechanism for managing the **context-limit** constraint: when a coding agent dispatches a subagent, it spawns a fresh copy of itself with a new context window. Walks through three flavors — exploratory (Claude Code's `Explore`), parallel (multiple at once, often on cheaper models like Haiku), and specialist (custom system prompts and/or tools for roles like code reviewer / test runner / debugger). Closes with a cautionary note against over-fragmenting tasks and links to official subagent docs across vendors.

## Key takeaways

- **Context limits are the constraint that motivates subagents.** LLMs are restricted by how many tokens they can fit in working memory. Limits "generally top out at around 1,000,000, and benchmarks frequently report better quality results below 200,000." Carefully managing context to fit those limits is critical for good results.
- **Subagents** are a simple but effective way to handle larger tasks without burning through the top-level agent's context. *"When a coding agent uses a subagent it effectively dispatches a fresh copy of itself to achieve a specified goal, with a new context window that starts with a fresh prompt."*
- Subagents work mechanically just like any other tool call: the parent dispatches them and waits for the response.

### Claude Code's `Explore` subagent (worked example)

- Whenever Claude Code starts a new task against an existing repo, it first **dispatches an `Explore` subagent** to map out the repo and surface what's relevant. Walks through a real transcript where the prompt was: *"Make the chapter diffs also show which characters have changed in this diff view with a darker color of red or green for the individually changed segments of text within the line"*.
- The `Explore` subagent's *starter prompt* was a structured search across templates, Python, JavaScript, and CSS, with explicit keywords (`diff`, `chapter`, `revision`, `history`, `compare`) and directories (`templates/`, `static/`, `blog/`) to search.
- Aside Willison flags: *"It's interesting to see models prompt themselves in this way — they generally have good taste in prompting strategies."*
- The subagent returned a "comprehensive summary" of findings (with file paths and line ranges), giving the parent everything it needed to start editing without having loaded the whole repo into its own context.

### Three flavors of subagent

1. **Exploratory (parent pauses).** The simplest case. The parent dispatches one subagent and waits. The principal advantage: the subagent works with a fresh context, so the exploration doesn't spend tokens from the parent's available limit.
2. **Parallel.** The parent dispatches several subagents at the same time, potentially using **faster and cheaper models such as Claude Haiku** to accelerate. For editing many files where the files are *not* dependent on each other, this is a significant speed boost. Sample prompt: *"Use subagents to find and update all of the templates that are affected by this change."*
3. **Specialist.** Some coding agents allow subagents to run with custom system prompts and/or custom tools so they take on a specific role. Examples Willison lists:
   - **Code reviewer** — reviews code, identifies bugs, feature gaps, design weaknesses.
   - **Test runner** — runs the test suite. Particularly valuable when the suite is large and verbose, because the subagent can hide the full output from the main agent and report only failures.
   - **Debugger** — specializes in debugging, spending its token allowance reasoning through the codebase and running snippets to isolate reproduction steps and root cause.

### Cautionary note

- *"While it can be tempting to go overboard breaking up tasks across dozens of different specialist subagents, it's important to remember that the main value of subagents is in preserving that valuable root context and managing token-heavy operations. Your root coding agent is perfectly capable of debugging or reviewing its own output provided it has the tokens to spare."*

### Vendor support

Official subagent docs linked: [OpenAI Codex](https://developers.openai.com/codex/subagents/), [Claude](https://code.claude.com/docs/en/sub-agents), [Gemini CLI](https://geminicli.com/docs/core/subagents/), [Mistral Vibe](https://docs.mistral.ai/mistral-vibe/agents-skills#agent-selection), [OpenCode](https://opencode.ai/docs/agents/), [VS Code](https://code.visualstudio.com/docs/copilot/agents/subagents), [Cursor](https://cursor.com/docs/subagents).

## Connections

- This chapter is the natural follow-on from [[2026-05-23-how-coding-agents-work]]: that chapter introduced **context limits** as a fundamental constraint; this one introduces the principal architectural response. Both are foundational pieces of [[agent-architecture]].
- Parallel subagents (especially with cheaper models like Haiku) are an economic optimization layered on top of [[economics-of-code]] — they trade root-context tokens for cheaper subagent tokens, and trade serial latency for parallel latency. The "fire off a prompt anyway" heuristic at agent scale.
- Specialist subagents formalize roles already gestured at in other chapters: the **code reviewer** specialist is the automatable version of the human review described in [[agent-code-review]]; the **test runner** specialist is a way to keep verbose output out of the parent's context (relevant to test-driven workflows referenced in [[2026-05-23-using-git-with-coding-agents]]).
- The "exploratory subagent runs `git log` etc. to map the codebase" pattern overlaps directly with the "review changes made today" session-seeding move in [[2026-05-23-using-git-with-coding-agents]] — both are forms of cheap context-loading at session start.
- The new dedicated topic is [[subagents]].
- Author: [[simon-willison]].

## Raw file

`raw/Subagents - Agentic Engineering Patterns.md`
