---
type: topic
tags: [agentic-engineering, prompting-patterns, hoarding, recombination, exploratory-prototyping]
created: 2026-05-23
updated: 2026-05-25
status: developing
sources: 5
---

# Hoarding working examples

Keep a personal, searchable collection of *running code* that proves you know how to do specific things, so that future-you (or your coding agent) can recombine those examples into solutions for new problems.

## Synthesis

### The pre-LLM rationale

[[simon-willison]] frames this as advice that was already valuable before coding agents existed. Much of the skill in building software is *knowing what's possible* and having at least a rough idea of how it could be done — answers to questions like "can a web page run OCR in pure JavaScript?", "can an iPhone app pair with a Bluetooth device when the app isn't running?", "can we process a 100 GB JSON file in Python without loading it all into memory?". The more such answers you've internalized, the better you can spot opportunities others miss.

The critical move: **the proof of an answer is running code, not just the belief that something is possible.** Theoretical knowledge that "X should work" is much weaker than having a working example sitting on disk. Willison's own hoarding venues are public and concrete:

- His [blog](https://simonwillison.net/) and [TIL blog](https://til.simonwillison.net/) — long-form and short-form write-ups of things he's figured out.
- 1000+ public [GitHub repos](https://github.com/simonw) — many small proof-of-concepts.
- [tools.simonwillison.net](https://tools.simonwillison.net/) — single-file HTML tools (HTML + embedded JS/CSS).
- [simonw/research](https://github.com/simonw/research) — larger agent-assisted research projects with working code plus a written report of what was learned.

### Why this matters more with coding agents

Coding agents change the value of the hoard for two reasons:

1. **The hoard becomes a reusable input to prompts.** A pattern Willison highlights as one of his favorites: tell the agent to build something new by **combining two or more existing working examples**. His canonical worked example (March 2024, Claude 3 Opus): he wanted browser-based OCR for PDFs, had a PDF.js snippet that turned a PDF into one image per page, and had a Tesseract.js snippet that OCRed an image. He pasted both into a single prompt with a description of the drag-and-drop tool he wanted, and the model produced a working proof-of-concept in one shot. A few iterations later, [tools.simonwillison.net/ocr](https://tools.simonwillison.net/ocr) was live.
2. **You only ever need to figure out a useful trick *once*.** If a trick is documented somewhere with a working code example, agents can consult that example to solve any future similarly-shaped problem. The hoard turns one-time effort into a permanent capability.

### How agents consume the hoard

Three concrete access patterns from [[2026-05-23-hoard-things-you-know-how-to-do]], each shown as an actual prompt:

- **Fetch from the public web with `curl`.** *"Use `curl` to fetch the source of `https://tools.simonwillison.net/ocr` and `https://tools.simonwillison.net/gemini-bbox` and build a new tool that lets you select a page from a PDF and pass it to Gemini to return bounding boxes for illustrations on that page."* He uses `curl` deliberately because Claude Code's built-in WebFetch summarizes the page rather than returning raw HTML — and for this use case the raw HTML *is* the example.
- **Search local directories.** *"Add mocked HTTP tests to the `~/dev/ecosystem/datasette-oauth` project inspired by how `~/dev/ecosystem/llm-mistral` is doing it."* The agent fires up a search sub-agent and pulls back only the details it needs.
- **Clone a repo to `/tmp`.** *"Clone `simonw/research` from GitHub to `/tmp` and find examples of compiling Rust to WebAssembly, then use that to build a demo HTML page for this project."*

All three are concrete instances of the agent-loop definition in [[coding-agents]] — the agent invokes `curl`, filesystem search, or `git` as tools toward the stated goal.

### Connection to the broader picture

The hoarding habit is amplified by, and amplifies, the cost shift described in [[economics-of-code]]. Because prototypes are now cheap to spin up ("fire off a prompt anyway"), the hoard grows faster; because the hoard exists, future prompts can produce better results from the same effort. The two patterns reinforce each other.

**Exploratory prototyping** (from [[2026-05-23-ai-should-help-us-produce-better-code]]) is a particularly clean instance of this loop. When you spin up a load-test simulation to prove a tech choice fits, you get two things at once: the *decision* (is Redis a good fit?) and a working example that demonstrates how to wire up that kind of simulation — which becomes a hoardable artifact for the next time a similar question comes up. And [[compound-engineering]] is the parallel pattern for *instructions* (what the agent should do) the way hoarding is for *artifacts* (what working code looks like); the two stack.

**Parallel subagents** (see [[subagents]]) make the "build many small experiments in parallel and keep the ones that work" loop fast enough that the hoard can grow noticeably faster than human serial attention allows. Combined with cheap models for the dispatched workers (Claude Haiku is Willison's named example), the cost of generating hoardable artifacts drops further.

### Karpathy's hoardable artifacts

[[andrej-karpathy]]'s body of work in [[2026-04-30-sequoia-ascent-karpathy]] illustrates a complementary form of hoarding — small, deliberately distilled artifacts designed for both humans and agents to inspect:

- **`microGPT`** — a complete GPT training and inference implementation in a single dependency-free Python file. Karpathy frames it as an educational artifact small enough that an agent can read it whole and a human can hold it in their head. It is the canonical hoardable artifact for "how does an LLM training loop actually work?".
- **The LLM Wiki Pattern** — Karpathy's [original gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) is *itself* a hoardable artifact: a paste-able description of a workflow that produces a knowledge base. This wiki is a direct application of that pattern.
- **The OpenClaw installation skill** — a block of text you paste into an agent to install a complex tool across many environments. The "shape" of a hoardable artifact in the [[software-3-0|Software 3.0]] paradigm: not code, but *agent instructions*.

Two things to note. First, Willison and Karpathy converge on the same practice from different angles: Willison's worked example (the OCR-PDF tool combining Tesseract.js + PDF.js) is *recombination*, while Karpathy's worked examples lean toward *distillation* (the smallest legible artifact for a domain). Both feed agents that can navigate and recombine them. Second, Karpathy's `microGPT` story includes a meta-observation: *"The models hate this. They can't do it. I kept trying to prompt an LLM to simplify more and more, and it just couldn't."* Tasteful simplification is currently off the model's rails (see [[verifiability]]), so the human hoarder's role in *creating* the artifact remains load-bearing.

## Open questions

- How should a hoard be *organized* so an agent can navigate it efficiently? Public/searchable (Willison's approach) vs. local-only have different tradeoffs.
- What's the right granularity for hoarded examples — single-file demos, repo-scale projects, snippets in notes?
- When the agent consults a hoarded example, how do you keep it from over-fitting to the example's style rather than adapting the *idea*?
- Are there hoardable artifacts beyond code — prompts, evaluations, harness configurations, agent transcripts — worth treating the same way?

## Sources

- [[2026-05-23-hoard-things-you-know-how-to-do]]
- [[2026-05-23-writing-code-is-cheap-now]]
- [[2026-05-23-ai-should-help-us-produce-better-code]]
- [[2026-05-23-subagents]]
- [[2026-04-30-sequoia-ascent-karpathy]]
