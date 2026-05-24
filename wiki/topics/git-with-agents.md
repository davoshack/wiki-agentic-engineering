---
type: topic
tags: [agentic-engineering, git, version-control, workflow, prompting-patterns, debugging]
created: 2026-05-23
updated: 2026-05-23
status: developing
sources: 1
---

# Git with agents

Coding agents are fluent in Git's full surface — basic *and* advanced — which means the human no longer needs to memorize the recipes. The right mental shift is to stay aware of *what's possible* and let the agent handle the *how*. This unlocks several formerly-painful workflows: bisect on demand, fearless history rewriting, library extraction with preserved history, and the universal "sort this out for me" escape valve.

## Synthesis

### The shift in posture

[[simon-willison]] frames the change in [[2026-05-23-using-git-with-coding-agents]]: *"This fluency means we can be more ambitious about how we use Git ourselves. We don't need to memorize how to do things with Git, but staying aware of what's possible means we can take advantage of the full suite of Git's abilities."* The bottleneck for Git power-use was rarely Git's capability — it was the human's recall of incantations. Coding agents remove the recall cost.

### Core prompts

A library of phrasings that work with any coding agent (verbatim from Willison):

- **"Start a new Git repo here"** — `git init`. ("Repo" alone is assumed to mean Git.)
- **"Commit these changes"** — usually `git commit -m "..."`.
- **"Add `username/repo` as a github remote"** — wires up GitHub (you need to create the repo at [github.com/new](https://github.com/new) first).
- **"Review changes made today"** / "recent changes" / "last three commits" — runs `git log`, loads the agent's context with what you've been working on. This is **a great way to seed a fresh agent session**: instantly you can talk about that code, propose follow-ups, ask questions.
- **"Integrate latest changes from main"** — fetch on main, integrate when on a branch.
- **"Discuss options for integrating changes from main"** — when you can't recall merge / rebase / squash / fast-forward differences. Agents are good at explaining trade-offs; *"everything in git can always be undone so there's minimal risk in trying new things."*

### "Sort out this git mess for me"

Willison's universal prompt for the painful states: failed cherry-picks, merge conflicts, staging confusion. Coding agents *"can navigate the most Byzantine of merge conflicts, reasoning through the intent of the new code and figuring out what to keep and how to combine conflicting changes."* If automated tests exist, the agent can verify they still pass before finalizing.

### Recovery: "Find and recover my code that does..."

If you've lost committed (or `git stash`ed) work, the agent can usually find it. Git's **`reflog`** captures references that haven't made it to a permanent branch; agents can search that and other branches. Lost work that was never committed is unrecoverable, but anything that touched the index probably isn't truly gone.

### Bisect, upgraded

**`git bisect`** is one of Git's most powerful debugging tools but has a steep learning curve — you have to express the bug as a test condition Git can run. The boilerplate is real, which is why bisect typically sat unused except for the most painful regressions.

Coding agents handle the boilerplate. The effect: bisect **upgrades from an occasional-use tool to one you can deploy any time you're curious about historic behavior.** Prompt: *"Use git bisect to find when this bug was introduced..."*.

### Rewriting history as editorial work

A reframing worth holding onto: *"Don't think of the Git history as a permanent record of what actually happened — instead consider it to be a deliberately authored story that describes the progression of the software project. This story is a tool to aid future development."* The author makes editorial decisions about what to keep.

History-rewriting prompts that work:
- **"Undo last commit"** — `git reset --soft HEAD~1`. Willison: he never remembered the recipe and now doesn't have to.
- **"Remove `uv.lock` from that last commit"** — finer-grained per-file surgery.
- **"Combine last three commits with a better commit message"** — combine + rewrite.

Related claim from Willison: **frontier-model commit-message taste is usually good enough to delegate.** He used to insist on writing his own; he now lets the model do it because the quality is "generally good enough, and often even better than what I would have produced myself." This is a small but meaningful taste-delegation: the agent does the prose, the human approves at the PR/review step (still bound by [[agent-code-review]]).

### Library extraction with preserved history

A workflow Willison singles out as one he uses often: extract a module from a larger repo into a standalone library *while preserving the relevant commit history* (author, dates, messages). Sample prompt: *"Start a new repo at `/tmp/distance-functions` and build a Python library there with the `lib/distance_functions.py` module from here — build a similar commit history copying the author and commit dates in the new repo."* This used to be painful enough that most developers settled for a fresh detached copy. No longer.

### Where this fits

- The history-rewriting freedom rests on the [[economics-of-code|cheap-code economic shift]]: when the *experiment* of trying a different merge strategy or commit shape is nearly free, the cost-of-mistakes calculus changes.
- The async-refactor workflow in [[refactoring-with-agents]] is *entirely* a Git workflow (branches/worktrees, PRs); this page is the prompt vocabulary for the underlying mechanics.
- The "review changes made today" session-seeding move is a small instance of context preservation — the same family as the dedicated mechanism in [[subagents]].
- Agent-produced commit messages and PR descriptions are still bound by [[agent-code-review]]: you own what you ship, including the prose.

## Open questions

- How well do agents handle Git workflows in multi-developer / multi-branch enterprise repos vs. solo work? The examples here are all solo.
- What's the right safety boundary for history-rewriting on shared branches? Local rewriting is fine; force-pushing rewritten history to a shared remote is dangerous. Agents need clear constraints here.
- For the library-extraction pattern: how reliable is the agent at *preserving* author and date metadata exactly, vs. introducing small drift?
- Is there a pattern for "show me what this commit changed and why" that uses `git log -p` / `git show` to seed deep historical understanding the way "review changes made today" seeds recent context?

## Sources

- [[2026-05-23-using-git-with-coding-agents]]
