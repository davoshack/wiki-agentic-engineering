---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/first-run-the-tests/
source_date: 2026-05-26
tags: [agentic-engineering, testing, tdd, prompts, session-seeding]
created: 2026-05-26
updated: 2026-05-26
status: developing
---

# First run the tests

A short chapter of *Agentic Engineering Patterns*. Willison's argument: automated tests
are no longer optional in the agent era, and "First run the tests" is a four-word
session-seeding prompt that loads a surprising amount of testing discipline into the
agent's behavior for the rest of the session.

## Key takeaways

- **Tests aren't optional anymore.** The historical excuse for skipping tests — they're
  time-consuming and expensive to maintain as code evolves — collapses when an agent can
  produce or update them in minutes. They're also "vital for ensuring AI-generated code
  does what it claims to do. If the code has never been executed it's pure luck if it
  actually works when deployed to production."
- **Tests are also onboarding material for the agent.** Ask Claude Code about an
  existing feature and it will very likely find and read the relevant tests on its way to
  an answer.
- **The session-seeder prompt:** at the start of a new session against an existing
  project, prompt:

  > First run the tests

  Or, for projects with a known harness:

  > Run "uv run pytest"

- **Why four words can carry so much weight.** The prompt does three things at once:
  1. Tells the agent a test suite exists and forces it to discover how to run it — making
     the agent almost certain to re-run tests after future changes.
  2. Most harnesses print a rough test count, which acts as a proxy for project size and
     hints that the agent should grep the tests when it wants to learn more.
  3. Puts the agent in a *testing mindset* so it naturally extends the suite as it works.
- **Pattern parallel.** "First run the tests" is the same shape of prompt as
  "Use red/green TDD" ([[2026-05-26-red-green-tdd]]): a compact phrase that activates a
  substantial chunk of pre-existing software-engineering discipline already baked into
  the models.

## Connections

- The foundational topic page for this and the two sibling chapters is
  [[agentic-testing]] (new).
- "Tests as the verifier" is the workflow-level instance of [[verifiability]]: tests are
  the canonical reward signal, and this prompt is how you make sure the signal is wired
  in from turn one.
- Directly supports the *tested* and *we know it works* dimensions of the
  [[economics-of-code|9-point good-code checklist]].
- Pairs with [[agent-code-review]]: a PR with "the tests pass" as evidence-of-work-done
  is partly because of this seeding move.
- Connects to [[hoarding-working-examples]] and [[git-with-agents]] in the broader
  family of *short prompts that compress real engineering discipline.*
- Author: [[simon-willison]].

## Raw file

`raw/First run the tests - Agentic Engineering Patterns.md`
