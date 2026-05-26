# Wiki Schema

This file is the **operating manual** for this wiki. It tells the LLM agent how the wiki
is structured, what the conventions are, and exactly what to do when ingesting a source,
answering a query, or running a lint pass.

Read this file at the start of every session before touching the wiki.

The wiki is the Juan's personal **Agentic Engineering knowledge-base** oriented: it accumulates a structured and curated information about Agentic Engineering discipline — built up from articles, papers, books, videos, transcripts, and notes over time. See [[LLM Wiki Karpathy Pattern]] for the philosophy behind the pattern.

The goal is to keep an updated information source with the last advances, techniques, methodologies and implementations.

---
## Roles

- **Juan** sources material, directs exploration, asks questions, decides what matters.
  He reads the wiki; he rarely writes it.
- **The LLM (you)** owns the `wiki/` directory entirely. You read raw sources, write and
  update pages, maintain cross-references, keep the index and log current. You do the
  bookkeeping so the wiki stays maintained.
- **Obsidian** is the IDE. Juan browses the wiki in Obsidian while you edit. Everything
  you write must render well there (wikilinks, graph view, frontmatter).

You never modify anything in `raw/`. That is the immutable source of truth.

---

## Project skills

Project-level skills live in `.claude/skills/`. Check this list before authoring artifacts
that match a skill's domain — they encode conventions and methodology specific to this
project that I should follow rather than improvise.

- `.claude/skills/excalidraw-diagram/SKILL.md` — invoke whenever creating Excalidraw
  diagrams (visualizing workflows, mental models, architectures, syntheses). Includes a
  render-and-validate loop that's mandatory, not optional. References live in
  `.claude/skills/excalidraw-diagram/references/`.

---

## Directory layout

```
wiki-agentic-engineering/
├── README.md            # the pattern (reference only)
├── CLAUDE.md            # this file — the schema
├── log.md               # chronological, append-only activity log
├── raw/                 # immutable sources — you READ, never WRITE
│   └── assets/          # downloaded images referenced by sources
└── wiki/                # LLM-owned — you create and maintain everything here
    ├── index.md         # catalog of every page (content-oriented)
    ├── overview.md      # the evolving big-picture synthesis
    ├── sources/         # one summary page per ingested source
    ├── areas/           # standing domains within agentic engineering (the practice itself; later: tooling, evaluation, security, team workflow…)
    ├── topics/          # concepts, frameworks, techniques, practices
    ├── people/          # experts, authors, or people in Juan's life
    ├── syntheses/       # cross-cutting analyses, comparisons, answers worth keeping
    └── templates/       # blank page templates (also usable by Obsidian's Templates plugin)
```

When creating a new page, start from the matching file in `wiki/templates/` so frontmatter
and section structure stay consistent. `templates/` is not part of the wiki's content —
skip it when indexing, linting, or answering queries.

A page goes in `areas/` if it's a broad standing domain within agentic engineering (e.g.
the practice itself, agent tooling, evaluation, security), `topics/` if it's a concept,
framework, technique, or pattern (e.g. [[compound-engineering]], [[refactoring-with-agents]],
[[economics-of-code]]), `people/` if it's a person (practitioner, author, researcher),
`sources/` if it's a summary of one ingested source, and `syntheses/` if it's a
cross-cutting analysis or a query answer worth keeping. When unsure, prefer `topics/`.

---

## Page conventions

**Filenames.** kebab-case, descriptive, `.md`. e.g. `compound-engineering.md` (topic),
`simon-willison.md` (person), `agentic-engineering.md` (area). Source pages are prefixed
with the ingest date: `2026-05-23-what-is-agentic-engineering.md`.

**Links.** Use Obsidian wikilinks: `[[compound-engineering]]` or
`[[economics-of-code|the broader cost story]]` for aliased text. Every page should link out
to related pages and be linked to from at least one other page — no orphans.

**Frontmatter.** Every wiki page starts with YAML frontmatter so Obsidian's Dataview plugin
can query it:

```yaml
---
type: area | topic | person | source | synthesis
tags: [agentic-engineering, coding-agents]
created: 2026-05-22
updated: 2026-05-22
status: stub | developing | mature      # how built-out the page is
sources: 3                               # count of sources backing this page
---
```

Source pages add: `source_type: article | pdf | video | transcript | note | image`,
`source_url:`, and `source_date:` (when the source was published/recorded).

**Page body structure.**

- *Area / topic / person pages*: a one-line definition, then a synthesis written in prose,
  then a `## Open questions` section, then `## Sources` listing the source pages that back
  the claims via wikilink.
- *Source pages*: frontmatter, a one-paragraph summary, `## Key takeaways` (the substantive
  points), `## Connections` (what in the wiki this updates or contradicts), and a link back
  to the raw file.
- *Synthesis pages*: the analysis itself — prose, comparison tables, or chart references —
  plus a `## Sources` section.

**Tone.** Pages are about Juan's learning of agentic engineering. Write claims with their
backing — attribute to a source where it matters ("Willison argues…", "Shipper & Klaassen
at Every describe…", "a recent benchmark found…"), and flag uncertainty rather than
smoothing it over.

**Contradictions.** When a new source disagrees with an existing claim, do not silently
overwrite. Note both: e.g. *"Earlier filed under [[economics-of-code]] from
[[2026-05-23-writing-code-is-cheap-now]]; [[2026-XX-XX-some-future-source]] challenges
this, arguing…"*. Surfacing tension is more valuable than false tidiness.

---

## Operation: INGEST

When Juan drops a source into `raw/` and asks you to process it:

1. **Read the source.** For PDFs, extract text. For videos/YouTube, work from the
   transcript (ask Juan to provide one, or the captions, if not already in `raw/`).
   For sources with images, read the text first, then view key images in `raw/assets/`.
2. **Discuss.** Briefly tell Juan the key takeaways and ask what he wants emphasized
   before you start writing. This is a supervised, one-at-a-time workflow — stay involved.
3. **Write the source page** in `wiki/sources/` named `YYYY-MM-DD-slug.md` with full
   frontmatter, summary, key takeaways, and connections.
4. **Update affected pages.** Touch every area/topic/person page the source bears on —
   create new pages if the source introduces something with no home yet. Revise syntheses
   and `overview.md` where the new material shifts the picture. A single source typically
   touches 8–15 pages. Bump `updated`, `sources`, and `status` in frontmatter as you go.
5. **Update `index.md`** — add new pages, refresh one-line summaries of changed ones.
6. **Append to `log.md`** — one `## [DATE] ingest | Title` entry (see log format below).
7. **Report back** — tell Juan which pages you created and changed so he can review them
   in Obsidian.

## Operation: QUERY

When Juan asks a question:

1. Read `wiki/index.md` to locate relevant pages, then read those pages.
2. Synthesize an answer with wikilink citations to the pages (and through them, sources)
   the answer rests on.
3. If the source material is thin, say so — and suggest what to read or search next.
4. **Offer to file the answer.** If the answer is a comparison, an analysis, or a
   connection worth keeping, propose saving it as a page in `wiki/syntheses/` so the
   exploration compounds instead of vanishing into chat. If Juan agrees, write it, update
   `index.md`, and log a `query` entry.

## Operation: LINT

When Juan asks for a health check, audit the wiki and report (don't auto-fix without
confirmation):

- Contradictions between pages.
- Stale claims a newer source has superseded.
- Orphan pages (no inbound wikilinks).
- Concepts mentioned repeatedly but lacking their own page.
- Missing cross-references between clearly related pages.
- Data gaps a web search or new source could fill — suggest specific questions to
  investigate and sources to look for.
- Frontmatter drift (wrong `sources` count, stale `updated`, `status` that no longer fits).

Append a `## [DATE] lint` entry to `log.md` summarizing findings.

---

## index.md

Content-oriented catalog of the whole wiki. Organized by category (Areas, Topics, People,
Syntheses, Sources). Each entry: a wikilink, a one-line summary, optionally source count or
date. Update it on every ingest and whenever a page is created or meaningfully changed.
This is the first thing you read when answering a query.

## log.md

Chronological, append-only. Every entry starts with a consistent header so the log is
greppable — `grep "^## \[" log.md | tail -5` gives the recent timeline:

```
## [2026-05-23] ingest | Simon Willison, Agentic Engineering Patterns — Ch. 1
## [2026-05-23] query  | What's the right workflow for async refactoring with agents?
## [2026-05-23] lint   | 0 orphans, 0 contradictions, 3 forward-ref drifts
```

Under each header, a few lines on what happened and which pages were affected.

---

## Source-type handling

- **Web articles** — typically clipped to markdown via Obsidian Web Clipper. Images, if
  downloaded, land in `raw/assets/`.
- **PDFs / papers** — extract text before summarizing; cite section or page numbers in
  takeaways where useful.
- **Images / diagrams** — you cannot read markdown with inline images in one pass. Read the
  text, then view the referenced images in `raw/assets/` separately for context.
- **Transcripts / notes** — treat as ordinary text sources.
- **YouTube videos** — work from the transcript or captions. If only a URL is in `raw/`,
  ask Juan to supply the transcript, and record `source_url` in the source page.

---

## Conventions co-evolve

This schema is not fixed. As Juan and the LLM discover what works for this domain — new
page types, better frontmatter, refined workflows — update this file. It is the one piece
of the wiki Juan and the LLM maintain together.
