---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/agentic-manual-testing/
source_date: 2026-05-26
tags: [agentic-engineering, testing, manual-testing, playwright, browser-automation, show-your-work]
created: 2026-05-26
updated: 2026-05-26
status: developing
---

# Agentic manual testing

A chapter of *Agentic Engineering Patterns* covering the testing modes that are *not*
the automated suite: ad-hoc invocation of new code, exploration of APIs over `curl`,
browser automation against web UIs, and "show your work" artifacts. Willison opens with
the core claim — code execution is what makes coding agents fundamentally different
from raw LLMs — and argues that even with red/green TDD, manual testing routinely
catches things automated tests miss.

## Key takeaways

- **The defining capability, restated.** *"The defining characteristic of a coding agent
  is that it can execute the code that it writes. ... Never assume that code generated
  by an LLM works until that code has been executed."* Coding agents can confirm or
  iterate; LLMs that only emit code cannot.
- **Automated tests are not enough.** Passing tests don't mean the code works as
  intended — startup crashes, missing UI elements, untested edge cases all slip
  through. "Automated tests are no replacement for manual testing." Willison wants to
  see a feature working with his own eyes before release.
- **Agents can do manual testing too,** and it often surfaces problems the suite
  missed. Modes by language/surface:
  - **Python libraries:** `python -c "...code..."` is the canonical pattern. Agents
    will use it spontaneously, and prompting "Try that new function on some edge cases
    using `python -c`" reliably activates it.
  - **Other languages / compiled tools:** "Write code in `/tmp` to try edge cases of
    that function and then compile and run it." Using `/tmp` keeps scratch files out of
    the repo.
  - **JSON APIs:** "Run a dev server and explore that new JSON API using `curl`."
    Telling the agent to *explore* — not test a specific endpoint — gets broad coverage
    cheaply.
- **The manual → automated loop.** When manual testing finds a bug, fix it with
  red/green TDD ([[2026-05-26-red-green-tdd]]) so the case is captured in the permanent
  suite. Manual testing and the automated suite compound.
- **Browser automation for web UIs.** Long-avoided because tests broke on tiny HTML
  changes; agents now maintain them cheaply enough to be worth using.
  - **[Playwright](https://playwright.dev/)** (Microsoft) is the current heavyweight —
    multiple language bindings, all major browser engines. *"Test that with Playwright"*
    is often enough.
  - **[agent-browser](https://github.com/vercel-labs/agent-browser)** (Vercel) is a
    Playwright CLI wrapper designed specifically for agents.
  - **[Rodney](https://github.com/simonw/rodney)** (Willison's own) uses Chrome DevTools
    Protocol directly. The example prompt bakes in three tricks:
    1. Run via `uvx rodney --help` so the agent installs the tool on first use.
    2. The `--help` text is written to teach the agent both *what Rodney is* and *how
       to use it* — a deliberate agent-onboarding artifact.
    3. "Look at screenshots" hints to the agent to use `rodney screenshot` and then
       evaluate the resulting images with its own vision capabilities.
- **Show your work — Showboat.** [Showboat](https://github.com/simonw/showboat) builds
  Markdown documents that capture an agentic manual-testing run. Three core commands:
  - `note` — append a Markdown note.
  - `exec` — record a command, run it, and record its output. The *most important*
    one: it captures both the command and the real output, which "discourages the agent
    from cheating and writing what it hoped had happened into the document."
  - `image` — embed an image (e.g. a Rodney screenshot).

  Example prompt: *"Run `uvx showboat --help` and then create a `notes/api-demo.md`
  showboat document and use it to test and document that new API."*
- **The broader idea: agents showing their work.** Willison is "fascinated by the
  challenge of having agents show their work." Demos and documented experiments are
  useful confirmation that the agent comprehensively solved the problem — and the
  artifact-recording substrate is now mature enough to make this routine.

## Connections

- This chapter, with [[2026-05-26-first-run-the-tests]] and [[2026-05-26-red-green-tdd]],
  defines [[agentic-testing]] — the new topic page that synthesizes all three.
- The opening line — *code execution is the defining characteristic of a coding agent*
  — is the strongest restatement yet of the definition in
  [[2026-05-23-what-is-agentic-engineering]] and underpins [[coding-agents]].
- The Playwright / agent-browser / Rodney landscape is **tool-surface** content for
  [[agent-architecture]] — these are the actuator tools that turn web UIs into a
  verifiable substrate.
- Rodney's `--help` design (an agent-onboarding artifact) and Showboat's `exec`
  (anti-cheating capture) are concrete instances of [[agent-native-infrastructure]] —
  building tools whose interfaces are designed for the agent as user.
- The "agent showing its work" theme connects to [[agent-code-review]] — Showboat
  documents are exactly the kind of *evidence-of-work-done* signal Willison's
  good-agentic-PR checklist asks for.
- The manual → red/green loop is a concrete [[compound-engineering]] motion at the
  test-suite level: each manual finding becomes permanent regression protection.
- Karpathy's [[verifiability|"on the model's rails?"]] question gets a practical
  answer here: when a UI isn't verifiable by the existing harness, browser automation
  *makes* it verifiable.
- Author: [[simon-willison]].

## Raw file

`raw/Agentic manual testing - Agentic Engineering Patterns.md`
