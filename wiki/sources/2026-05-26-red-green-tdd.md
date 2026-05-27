---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/red-green-tdd/
source_date: 2026-05-26
tags: [agentic-engineering, testing, tdd, prompts, verifiability]
created: 2026-05-26
updated: 2026-05-26
status: developing
---

# Red/green TDD

Short chapter of *Agentic Engineering Patterns*. Willison's argument: test-first
development is a *fantastic* fit for coding agents because it guards against the two
most common agent failure modes — code that doesn't work and code nobody needs — in one
move. "Use red/green TDD" is the four-word prompt that triggers the full discipline.

## Key takeaways

- **TDD recap, in Willison's compact form.** Test-Driven Development is "a programming
  style where you ensure every piece of code you write is accompanied by automated tests
  that demonstrate the code works." The most disciplined form is **test-first**: write
  the tests first, confirm they fail, then iterate the implementation until they pass.
- **Why test-first is a great fit for agents.** Coding agents have two characteristic
  risks: (a) writing code that doesn't actually work, and (b) writing code that is
  unnecessary and never gets used. Test-first protects against both — failing tests
  prove the implementation is needed, and passing tests prove it works.
- **The "red" step is load-bearing.** *"It's important to confirm that the tests fail
  before implementing the code to make them pass. If you skip that step you risk
  building a test that passes already, hence failing to exercise and confirm your new
  implementation."* That's the literal meaning of red/green: the red phase watches the
  tests fail; the green phase confirms they pass.
- **Compounding regression protection.** A comprehensive suite is "by far the most
  effective way to keep [existing] features working" as a project grows — and an
  agent-assisted workflow makes building one cheap.
- **The four-word prompt.** *"Every good model understands 'red/green TDD' as a
  shorthand for the much longer 'use test driven development, write the tests first,
  confirm that the tests fail before you implement the change that gets them to pass.'"*
  Example: *Build a Python function to extract headers from a markdown string. Use
  red/green TDD.*

## Connections

- Pairs with [[2026-05-26-first-run-the-tests]] as the second canonical *short prompt
  that loads a chunk of engineering discipline.* Both feed [[agentic-testing]].
- Direct instance of [[verifiability]]: red/green is the literal observation of a
  reward signal flipping from fail → pass.
- Reinforces the *tested*, *handles edge cases*, and *works* dimensions of the
  [[economics-of-code|9-point good-code checklist]].
- The end-state pattern from [[2026-05-26-agentic-manual-testing]] — *issues found
  during manual testing should be fixed with red/green TDD so the case enters the
  permanent suite* — closes the loop between manual and automated testing.
- The "code nobody needs" failure mode is the YAGNI complement to the
  [[refactoring-with-agents|"oversized files" / over-engineering]] anti-style; test-first
  is a structural defence.
- Author: [[simon-willison]].

## Raw file

`raw/Redgreen TDD - Agentic Engineering Patterns.md`
