# Log

Chronological, append-only record of activity on the wiki — ingests, queries, lint passes.
Each entry starts with `## [YYYY-MM-DD] type | label` so the log stays greppable:
`grep "^## \[" log.md | tail -5`.

## [2026-05-22] setup | Wiki scaffolded

Initialized the personal-knowledge wiki: directory structure, `CLAUDE.md` schema,
`wiki/index.md`, `wiki/overview.md`, and page templates. No sources ingested yet.

## [2026-05-23] ingest | Simon Willison, *Agentic Engineering Patterns* Ch. 1–3

First content ingest. Processed three foundational chapters of Simon Willison's guide
together in one pass (consolidated topic granularity, faithful-summary framing, per Juan).

Pages created:
- Sources: [[2026-05-23-what-is-agentic-engineering]], [[2026-05-23-writing-code-is-cheap-now]], [[2026-05-23-hoard-things-you-know-how-to-do]]
- Person: [[simon-willison]]
- Area: [[agentic-engineering]]
- Topics: [[coding-agents]], [[economics-of-code]], [[hoarding-working-examples]]

Pages updated:
- `wiki/index.md` — rebuilt with all new entries.
- `wiki/overview.md` — first real synthesis, replacing the placeholder.

## [2026-05-23] ingest | Simon Willison, *Agentic Engineering Patterns* Ch. 4–5

Second ingest in the same session. Two more chapters of Willison's guide, processed
together per Juan's standing preference (faithful summary, all-in-one). Two judgment
calls confirmed with Juan: refactoring/technical-debt content spun out as its own topic
page (rather than folded into economics-of-code), and no person pages for Shipper /
Klaassen yet — they're cited inline in the new compound-engineering page.

Pages created:
- Sources: [[2026-05-23-ai-should-help-us-produce-better-code]], [[2026-05-23-anti-patterns-things-to-avoid]]
- Topics: [[compound-engineering]], [[refactoring-with-agents]], [[agent-code-review]]

Pages updated:
- [[coding-agents]] — added async-agents subsection and a forward link to [[compound-engineering]] for the "agents can learn" thread.
- [[economics-of-code]] — added "spending the surplus on quality" section (technical debt, exploratory prototyping, Boring Technology, compound engineering, "we can finally have both").
- [[hoarding-working-examples]] — added an exploratory-prototyping paragraph and the artifacts-vs-instructions comparison with [[compound-engineering]].
- [[agentic-engineering]] (area) — expanded the habits list with [[compound-engineering]] and [[agent-code-review]]; added the surplus-on-quality framing.
- [[simon-willison]] — bumped source count to 5.
- `wiki/index.md` — added all new entries.
- `wiki/overview.md` — restructured current-picture into the four-move argument; updated open questions.

## [2026-05-23] lint   | 0 orphans, 0 contradictions, 3 forward-ref drifts, several data gaps

Audited 14 content pages across `wiki/`. Findings:

- **No orphans, no contradictions, no frontmatter drift.** All `sources:` counts match their `## Sources` lists; all pages at `status: developing`; cross-link density is high (top: [[simon-willison]] 15, [[2026-05-23-ai-should-help-us-produce-better-code]] 15).
- **3 source pages need forward references** added to their `## Connections` lists now that ch.4–5 introduced new topic pages absorbing their threads:
  - [[2026-05-23-what-is-agentic-engineering]] — add [[compound-engineering]] for the "agents can learn" thread (currently only points to [[hoarding-working-examples]], which is a sibling not the home).
  - [[2026-05-23-writing-code-is-cheap-now]] — add [[compound-engineering]] and [[refactoring-with-agents]] (ch.4 directly extends this chapter's argument).
  - [[2026-05-23-hoard-things-you-know-how-to-do]] — add [[compound-engineering]] (artifacts-vs-instructions parallel now made explicit in the hoarding topic page).
- **Concepts that may warrant their own pages later** (kept folded per "few consolidated topics" preference): vibe coding, exploratory prototyping, async coding agents.
- **Suggested sources to seek next**: Every's *Compound Engineering* post (would move [[compound-engineering]] from 1 source to 2 and answer several of its open questions); Willison's *Your job is to deliver code that works*; Karpathy's original vibe-coding tweet; Dan McKinley's *Boring Technology*; at least one deliberately adversarial perspective (skeptics, empirical quality studies, security, enterprise context).
- **Open questions with no current-source answer**: mechanics of compound engineering ("compound step", where instructions live); safe parallel async refactoring; vendor-portability of patterns; further anti-patterns beyond unreviewed PRs.

Drift fixes applied (Juan confirmed): the three source pages above now carry forward references to [[compound-engineering]] and (for ch.2) [[refactoring-with-agents]]. Other findings remain open as suggestions for future ingests.

## [2026-05-23] ingest | Simon Willison, *Agentic Engineering Patterns* Ch. 6–8

Third ingest in the same session. Three more chapters of Willison's guide processed
together (faithful summary, all-in-one). Judgment call confirmed with Juan: ch.6's
mechanics content spun out as its own [[agent-architecture]] topic page rather than
folded into [[coding-agents]] — too many distinct technical concepts (tokens, context
windows, system prompts, reasoning, token caching) to keep in one page.

Pages created:
- Sources: [[2026-05-23-how-coding-agents-work]], [[2026-05-23-using-git-with-coding-agents]], [[2026-05-23-subagents]]
- Topics: [[agent-architecture]], [[git-with-agents]], [[subagents]]

Pages updated:
- [[coding-agents]] — added cross-refs to [[agent-architecture]] and [[subagents]]; source count to 6.
- [[economics-of-code]] — added "token-cost layer" section covering token caching and subagent-driven cost optimization; source count to 5.
- [[compound-engineering]] — added "what 'the instructions' actually are" section grounding the practice in system prompts, repo-level instruction files (`CLAUDE.md`, `AGENTS.md`), and the tool harness; source count to 2.
- [[hoarding-working-examples]] — added paragraph on parallel subagents accelerating hoard growth; source count to 4.
- [[agentic-engineering]] (area) — synthesis now references [[agent-architecture]]; habits list expanded with [[git-with-agents]] and [[subagents]]; source count to 8.
- [[simon-willison]] — source count to 8.
- `wiki/index.md` — added all new entries.
- `wiki/overview.md` — restructured around the four-layer argument (what it is → how it works → why it matters → what to spend the surplus on); cross-cutting habits section added; open questions refreshed.

## [2026-05-23] lint   | 0 orphans, 0 contradictions, 5 missing cross-refs, 1 structural finding

Audited 17 content pages across `wiki/`. Findings:

- **No orphans, no contradictions, no frontmatter drift.** All `sources:` counts match their `## Sources` lists; cross-link density is high (top: [[simon-willison]] 21, [[2026-05-23-ai-should-help-us-produce-better-code]] 18, [[compound-engineering]] 18, [[economics-of-code]] 18).
- **5 missing cross-references** (asymmetric or skipped foundational links):
  - [[economics-of-code]] → [[coding-agents]] (entirely missing from a page that's *about* coding agents).
  - [[agent-architecture]] → [[economics-of-code]] (reverse direction exists; should be symmetric in the token / caching subsections).
  - [[agent-code-review]] → [[subagents]] (specialist code-reviewer subagents are the automatable version of this).
  - [[refactoring-with-agents]] → [[git-with-agents]] and [[subagents]] (the refactor workflow is a Git workflow + parallel subagents are the natural multi-file fan-out).
  - [[subagents]] → [[hoarding-working-examples]] (reverse direction exists; should be symmetric).
- **1 structural finding**: [[overview]] has no `## Sources` section though the schema requires one for synthesis pages. Inline wikilink citations exist throughout the prose. Either add the section or revise the schema.
- **Concepts possibly warranting their own page later** (not now per consolidated-topics preference): context-management (cross-cutting, currently split between [[agent-architecture]] and [[subagents]]); vibe coding, exploratory prototyping, async coding agents (status unchanged from prior lint).
- **Suggested sources to seek next**: at least one vendor subagent doc (Codex / Claude / Gemini CLI / Mistral Vibe / OpenCode / VS Code / Cursor) to give [[subagents]] a second source and characterize vendor differences; the linked Codex system prompt as a concrete example for [[agent-architecture]]; Every's Compound Engineering post (still the most load-bearing un-ingested external ref); Willison's *Your job is to deliver code that works*; Karpathy's original vibe-coding tweet; Dan McKinley's *Boring Technology*; deliberately adversarial perspectives.
- **Open questions with no current-source answer**: vendor portability of patterns; reasoning-mode economics; safe envelope for shared-branch history rewriting; detecting file dependencies before parallel-dispatching subagents; further anti-patterns; operational mechanics of compound engineering; reliability of author/date preservation in library extraction.

No fixes applied — awaiting confirmation.

## [2026-05-25] ingest | Andrej Karpathy at Sequoia Ascent 2026

Major ingest — first source by a second author and the originator of "vibe coding"
Willison's chapters had cited secondhand. Source is a 37KB combined summary + cleaned
transcript posted to Karpathy's blog (talk delivered 2026-04-30, transcript posted
shortly after). Three judgment calls confirmed with Juan: spin out 3 new topic pages
(rather than 4 — vibe coding stays folded in [[coding-agents]] with a major update);
fold ghosts-vs-animals into [[agent-architecture]] as a mental-model section; build
the wiki's first explicit cross-author synthesis page.

Pages created:
- Source: [[2026-04-30-sequoia-ascent-karpathy]]
- Person: [[andrej-karpathy]]
- Topics: [[software-3-0]], [[verifiability]] (incl. jagged intelligence), [[agent-native-infrastructure]]
- Synthesis (first one in the wiki): [[willison-vs-karpathy]]

Pages updated:
- [[coding-agents]] — major rewrite of the vibe-coding section using Karpathy's canonical floor/ceiling framing; added Karpathy's compact "define context / tools / feedback loop / guardrails" recipe; source count to 7.
- [[agent-architecture]] — added "ghosts not animals" mental-model section; source count to 2.
- [[economics-of-code]] — added "why coding specifically — the verifiability layer" section; source count to 6.
- [[compound-engineering]] — added "the recipe Karpathy compounds toward" section; source count to 3.
- [[hoarding-working-examples]] — added "Karpathy's hoardable artifacts" section (microGPT, LLM Wiki Pattern, OpenClaw skill) with the distillation-vs-recombination observation; source count to 5.
- [[simon-willison]] — added "reads alongside Karpathy" note pointing to the synthesis; source count unchanged.
- [[agentic-engineering]] (area) — opening synthesis now references Karpathy and the December 2025 inflection; habits list expanded with [[verifiability]] and [[agent-native-infrastructure]]; source count to 9.
- `wiki/index.md` — restructured topics into four groupings (Foundations, Economics-and-analytic-frames, Practices, World-side); added all new entries.
- `wiki/overview.md` — restructured around a five-layer argument (what it is → how it works → why it matters and where AI moves fastest → what to spend the surplus on → world side); cross-cutting habits expanded; open questions refreshed; source count to 9.

Multi-author note: the wiki is no longer "one author deep." Future ingests can use the
stabilized vocabulary (coding agents, harness, tools in a loop, vibe coding, agentic
engineering, Software 3.0, verifiability, jagged intelligence, ghosts not animals,
sensors and actuators) without re-defining. The paradigm/practice split (Karpathy /
Willison) is now a useful spine for placing future sources.

## [2026-05-25] query  | Ghosts-not-animals × Sutton's Bitter Lesson

Juan asked how Karpathy's ghosts-not-animals mental model relates to Sutton's
*The Bitter Lesson*. Answered as a synthesis: same anti-anthropomorphism applied at
sequential stages — Sutton at design-time (don't encode cognition intuitions into
training), Karpathy at use-time (don't project them onto the resulting system). The
ghost is the natural artifact of taking Sutton seriously; jagged intelligence is the
practitioner's view of "scales with computation." Filed the answer as
[[ghosts-and-the-bitter-lesson]] with an explicit note that Sutton is not yet ingested
(the Bitter Lesson content currently rests on outside material).

Suggested follow-up ingest: Sutton's [2019 essay](http://www.incompleteideas.net/IncIdeas/BitterLesson.html)
would resolve the dangling external reference and anchor a `topics/bitter-lesson.md` page,
with inbound wikilinks from [[verifiability]], [[agent-architecture]], and this synthesis.
