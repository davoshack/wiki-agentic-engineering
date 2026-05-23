---
type: source
source_type: article
source_url: https://simonwillison.net/guides/agentic-engineering-patterns/hoard-things-you-know-how-to-do/
source_date: 2026-05-23
tags: [agentic-engineering, prompting-patterns, hoarding, recombination]
created: 2026-05-23
updated: 2026-05-23
status: developing
---

# Hoard things you know how to do

The third chapter of *Agentic Engineering Patterns*. Frames a pre-LLM piece of career advice — keep a personal collection of working code examples that prove you know how to do specific things — and explains how coding agents amplify the value of that hoard. Includes a concrete worked example (browser-based OCR-for-PDFs built by combining Tesseract.js and PDF.js examples).

## Key takeaways

- Core advice: **hoard things you know how to do**, in the form of *running code that proves the answer*.
- "A big part of the skill in building software is understanding what's possible and what isn't, and having at least a rough idea of how those things can be accomplished." A deep collection of answered "is X possible?" questions, each backed by a working example, is a key professional asset.
- *Knowing something is theoretically possible is not the same as having seen it done.* Working code is the proof.
- Willison's own hoarding venues: his [blog](https://simonwillison.net/), his [TIL blog](https://til.simonwillison.net/), 1000+ public [GitHub repos](https://github.com/simonw), the [tools.simonwillison.net](https://tools.simonwillison.net/) collection of single-file HTML tools, and the [simonw/research](https://github.com/simonw/research) repo for larger agent-assisted research projects.
- **Recombination prompting pattern**: tell an agent to build something new by combining two or more existing working examples. The OCR-PDF tool is the worked example: he combined a PDF.js "PDF → image per page" snippet and a Tesseract.js OCR snippet into a single drag-and-drop page. First model used was Claude 3 Opus (March 2024); the model produced a working proof-of-concept in one shot.
- Coding agents amplify the value of the hoard in at least three ways:
  - **Fetch from the public web.** Example prompt: *"Use curl to fetch the source of `https://tools.simonwillison.net/ocr` and `https://tools.simonwillison.net/gemini-bbox` and build a new tool that…"* — uses `curl` deliberately so the agent gets raw HTML rather than a summarized WebFetch view.
  - **Search local directories.** Example prompt: *"Add mocked HTTP tests to the `~/dev/ecosystem/datasette-oauth` project inspired by how `~/dev/ecosystem/llm-mistral` is doing it."* The agent fires up a sub-agent to find just what it needs.
  - **Clone repos to /tmp.** Example prompt: *"Clone `simonw/research` from GitHub to `/tmp` and find examples of compiling Rust to WebAssembly, then use that to build a demo HTML page for this project."*
- Key insight: coding agents mean *we only ever need to figure out a useful trick once*. If that trick is documented with a working code example, agents can re-use it on any future similarly-shaped problem.

## Connections

- Concrete instance of the "fire off a prompt anyway" heuristic from [[2026-05-23-writing-code-is-cheap-now]] — the hoard exists *because* prototypes are now cheap to spin up, and *for* future agent reuse.
- The recombination pattern is the substance of [[hoarding-working-examples]].
- Connects to [[coding-agents]]: the prompts above illustrate the tool-loop definition concretely — agents can invoke `curl`, filesystem search, and `git clone` as tools toward a goal.
- Author: [[simon-willison]].

## Raw file

`raw/Hoard things you know how to do - Agentic Engineering Patterns.md`
