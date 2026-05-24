---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/using-git-with-coding-agents/
source_date: 2026-05-23
tags: [agentic-engineering, git, version-control, workflow, prompting-patterns]
created: 2026-05-23
updated: 2026-05-23
status: developing
---

# Using Git with coding agents

The seventh chapter of *Agentic Engineering Patterns*. Argues that Git fluency in coding agents lets us be more ambitious with Git — we no longer need to memorize *how* to do things, just stay aware of what's possible. Walks through core prompts (basic commits and merges through to bisect), then dives into advanced history-rewriting and the "library extraction with preserved history" pattern.

## Key takeaways

- Git is **a key tool for working with coding agents**: version control gives us a recoverable record of every change, and *all* the coding agents are fluent in basic and advanced Git.
- *"This fluency means we can be more ambitious about how we use Git ourselves. We don't need to memorize how to do things with Git, but staying aware of what's possible means we can take advantage of the full suite of Git's abilities."*
- **Git essentials Willison foregrounds:** repositories, commits (timestamped bundles of changes with a message and author), branches, merges (multiple strategies: merge / rebase / squash / fast-forward), clones (carry the full history, making history-diving network-free), remotes (GitHub is most popular but Git is open source — any service supporting the Git protocol works).
- **Core prompts that work with any coding agent** — these are quoted as the prompts you'd actually type:
  - *"Start a new Git repo here"* — agent will run `git init`. ("repo" alone is assumed to mean Git repo.)
  - *"Commit these changes"* — usually `git commit -m "..."`.
  - *"Add `username/repo` as a github remote"* — wires up GitHub. (You'll need to create the repo first at [github.com/new](https://github.com/new).)
  - **"Review changes made today"** (also "recent changes" or "last three commits") — a great way to *seed a fresh agent session*. Runs `git log`, loads context with recent work and commit messages. You can then start talking about that code, suggest follow-ups, or propose the next change.
  - *"Integrate latest changes from main"* — on main, fetches; on a branch, integrates main in.
  - *"Discuss options for integrating changes from main"* — useful when you don't remember the merge/rebase/squash/fast-forward differences. Agents are good at explaining trade-offs, and *"everything in git can always be undone so there's minimal risk in trying new things."*
- **"Sort out this git mess for me"** — Willison's universal prompt, used surprisingly often. Example: fixing a cherry-pick that failed with a merge conflict. Coding agents *"can navigate the most Byzantine of merge conflicts, reasoning through the intent of the new code and figuring out what to keep and how to combine conflicting changes"*; if you have automated tests, the agent can verify they pass before finalizing the merge.
- **"Find and recover my code that does..."** — if you've lost work that was previously committed (or `git stash`ed), the agent can probably find it. Git's `reflog` captures details that haven't made it to a permanent branch; agents can search that and other branches.
- **"Use `git bisect` to find when this bug was introduced..."** — bisect is one of Git's most powerful debugging tools but has a steep learning curve (you need to express the bug as a test condition Git can run). Agents handle the boilerplate, which **upgrades bisect from an occasional-use tool to one you can deploy any time you're curious about historic behavior.**
- **Rewriting history is for editorial purposes, not falsification.** *"Don't think of the Git history as a permanent record of what actually happened — instead consider it to be a deliberately authored story that describes the progression of the software project."* Permanent record of mistakes is sometimes useful but the author makes editorial calls.
- **History-rewriting prompts:**
  - *"Undo last commit"* — `git reset --soft HEAD~1` (Willison: he never remembered the recipe, now doesn't have to).
  - *"Remove `uv.lock` from that last commit"* — finer-grained surgery on individual commits.
  - *"Combine last three commits with a better commit message"* — combine + rewrite the message.
- **Agents often have better commit-message taste than the human.** Willison used to insist on writing his own; he now accepts that frontier-model quality is "generally good enough, and often even better than what I would have produced myself."
- **Building a new repo from scraps of an older one** — library extraction with preserved history is the worked example. Sample prompt: *"Start a new repo at `/tmp/distance-functions` and build a Python library there with the `lib/distance_functions.py` module from here — build a similar commit history copying the author and commit dates in the new repo."* This used to be involved enough that most developers settled for a detached fresh copy; no longer.

## Connections

- The "review changes made today" session-seeding move is itself a small instance of [[compound-engineering]]: instead of building a permanent harness update, you let `git log` reconstruct context on demand at the start of each session.
- The "library extraction with preserved history" pattern is a concrete instance of [[hoarding-working-examples]] — a hoardable workflow that previously was too painful to attempt.
- The history-rewriting freedom relies on the [[economics-of-code|cheap-code economic shift]] — when undoing and retrying is cheap, the calculus on rewriting commits changes.
- Git fluency is one of the most-used tools in [[refactoring-with-agents]] (the async refactor PR workflow is entirely a Git workflow).
- The cautionary note from [[agent-code-review]] still applies: an agent that "sorts out the git mess" is still producing changes you need to review before pushing.
- Author: [[simon-willison]].

## Raw file

`raw/Using Git with coding agents - Agentic Engineering Patterns.md`
