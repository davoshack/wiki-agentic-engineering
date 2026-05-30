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

## [2026-05-25] meta   | Wired up the excalidraw-diagram skill; redid the synthesis diagram

Discovered I'd authored an Excalidraw file from scratch instead of using the project's
`excalidraw-diagram` skill — the skill wasn't surfaced because its folder
(`excalidraw-diagram-skill/`) didn't match the `name: excalidraw-diagram` in its
frontmatter (and its own internal references). Fixed:

- Renamed `.claude/skills/excalidraw-diagram-skill/` → `.claude/skills/excalidraw-diagram/`
  so auto-discovery works and the SKILL.md's render-command path resolves.
- Fixed `.python-version` (was `excalidraw-render` — a project name — instead of `3.12`).
- Patched the render template to pin `@excalidraw/excalidraw@0.18.1` without `?bundle`;
  the unpinned `?bundle` variant on esm.sh has a broken transitive dependency
  (`@braintree/sanitize-url@6.0.2`) that 404s.
- Added a "Project skills" section to `CLAUDE.md` so the skill is referenced in always-
  loaded context as a belt-and-suspenders against discovery failures.

Then redid [[ghosts-and-the-bitter-lesson]]'s diagram following the skill end-to-end:
read references, ran the design steps (the curve *is* the Ghost rather than a box labeled
"Ghost"), built JSON, ran the mandatory render-view-fix loop for 3 iterations until both
the vision check and the defect check passed. The new file is `.excalidraw` (raw JSON,
per skill convention), the PNG is the embedded artifact in the synthesis markdown, and
the old `.excalidraw.md` was deleted.

## [2026-05-25] diagram | Venn diagram for [[willison-vs-karpathy]]

Built `wiki/syntheses/willison-vs-karpathy.excalidraw` following the skill end-to-end.
Visual pattern chosen: **Venn diagram** — genuinely isomorphic to the synthesis's central
argument (two perspectives that overlap substantially, each contributing things the
other doesn't, with shared blind spots outside both). Strip the text and the structure
alone communicates the claim.

Color encoding: orange = Willison (practitioner discipline), purple = Karpathy (AI /
paradigms), red = blind spots. Two ellipse outlines (no fill, transparent background)
so the overlap region is naturally defined by the intersecting arcs. Region labels +
short bullets in each of the three zones; blind spots with marker dots below a dashed
divider; synthesis pull-quote at the bottom.

Passed the render-view-fix loop on iteration 1 — Venn geometry was planned with ellipse
math first (verified bullet x-coordinates fall inside their intended zones at the
relevant y-coordinates), so no defects to fix on the first render. PNG embedded in
[[willison-vs-karpathy]].

## [2026-05-26] ingest | Simon Willison, *Agentic Engineering Patterns* — testing trio

Fourth Willison ingest. Three short chapters on testing processed together as a unit,
per Juan: *First run the tests*, *Red/green TDD*, *Agentic manual testing*. Judgment
call confirmed with Juan: synthesize all three into one new topic page
[[agentic-testing]] rather than split into automated vs manual subpages — the three
modes describe a single compounding loop and read better together.

Pages created:
- Sources: [[2026-05-26-first-run-the-tests]], [[2026-05-26-red-green-tdd]], [[2026-05-26-agentic-manual-testing]]
- Topic: [[agentic-testing]] (synthesizes automated TDD + manual testing + four-word-prompt-as-compressed-discipline)

Pages updated:
- [[coding-agents]] — strengthened the code-execution-as-defining-capability claim with the new chapter's opening line; pointer to [[agentic-testing]]; source count to 8.
- [[economics-of-code]] — connected the *tested* / *we know it works* dimensions of the 9-point checklist to [[agentic-testing]]; source count to 7.
- [[verifiability]] — added a pointer that [[agentic-testing]] is the operational practice that wires the verifier into a project; noted browser automation as making previously-hard-to-verify UI substrates verifiable; source count to 4.
- [[agent-code-review]] — added a Showboat / exec-capture paragraph as the concrete substrate for evidence-of-work-done; source count to 3.
- [[compound-engineering]] — added the *manual finding → red/green → permanent test* loop as the suite-level compounding motion (third granularity alongside repo files and the system prompt); source count to 4.
- [[agent-architecture]] — added a browser-automation tool-surface paragraph (Playwright / agent-browser / Rodney) with the vLLM-screenshot pairing; source count to 3.
- [[agent-native-infrastructure]] — added Rodney's `--help`-as-agent-onboarding and Showboat's `exec` mechanical-capture as worked instances of the thesis at the dev-tools layer; source count to 2.
- [[agentic-engineering]] (area) — added an *agentic-testing* habit bullet; source count to 12.
- [[simon-willison]] — added "tool-builder, not just tool-user" note (Rodney, Showboat, `llm`); source count to 11.
- `wiki/overview.md` — cross-cutting habits expanded from three to four (added agentic-testing); "eight chapters" → "eleven chapters"; source count to 12.
- `wiki/index.md` — added [[agentic-testing]] to the Practices group; added the three new source entries.

Pattern worth flagging across these chapters: *four-word prompts as compressed
discipline.* "First run the tests" and "Use red/green TDD" each load a substantial
chunk of pre-existing software-engineering practice. This is the same family as
[[git-with-agents]]'s *"sort out this git mess for me"* — compact phrases that get
disproportionate leverage from models trained on years of human engineering text.
Named explicitly in [[agentic-testing]].

## [2026-05-26] ingest | Kumar & Ramagopal (Cisco), *Agentic Engineering: How Swarms of AI Agents Are Redefining Software Engineering*

Major ingest — first non-Willison, non-Karpathy source; first enterprise / team-scale
vantage in the wiki; first source to use *"agentic engineering"* in a sense
substantively different from the practitioner-discipline definition the wiki had been
developing. Three judgment calls confirmed with Juan: surface the definitional
contradiction in the area page and overview rather than silently overwriting; one
consolidated topic page ([[multi-agent-coordination]]) rather than two; one combined
person page ([[kumar-ramagopal]]) rather than two thin ones. Also filed a dedicated
cross-cutting synthesis ([[practitioner-discipline-vs-control-plane]]) because the
split is load-bearing enough to warrant its own page.

Pages created:
- Source: [[2026-05-26-agentic-engineering-swarms]]
- Topic: [[multi-agent-coordination]] — Worker/Leader pattern, A2A vs MCP, the four-stage Worker loop, LangGraph/LangSmith/LangMem, pilot results, the PR-review-bottleneck observation.
- Person: [[kumar-ramagopal]] (combined page).
- Synthesis: [[practitioner-discipline-vs-control-plane]] — names the two senses of the term, shows how they compose (coding agents are components inside Worker Agents), tracks the vocabulary trajectory.

Pages updated:
- [[agentic-engineering]] (area) — added a callout at the top carrying both definitions side by side; added a new habit bullet pointing to [[multi-agent-coordination]]; source count to 13.
- [[overview]] — promoted to three voices; added a new "6. The team / organization side — the control plane" section; "State of the picture" rewritten (gap partly filled; second-enterprise source now load-bearing); two new open questions (vocabulary trajectory, swarm-scale safety); the verification-and-review open question expanded with the bottleneck observation; source count to 13.
- [[coding-agents]] — added a "Coding agents as components inside larger systems" section repositioning the Willison/Karpathy subject as a primitive inside Worker Agents; source count to 9.
- [[subagents]] — added a "Subagents vs. multi-agent swarms — same word, different unit" disambiguation; source count to 2.
- [[compound-engineering]] — extended the *transient signal → durable instruction* loop from three granularities to four (added swarm memory / LangMem as the organization-scale analog); source count to 5.
- [[agent-native-infrastructure]] — added an A2A / MCP / Leader-Agent-tool-gateway paragraph; MCP gets a second source backing it; A2A is named for the first time; source count to 3.
- [[agentic-testing]] — added a "Post-PR testing as the new compression frontier" section (Cisco pilot's headline finding: gains came from compressing post-PR-merge testing, not faster code generation); source count to 4.
- [[agent-code-review]] — added a "Review as the new bottleneck at team scale" section; explicit three-sub-question framing for what to do about it; source count to 4.
- `wiki/index.md` — new "Organization / team scale" topic section; new person entry; new synthesis entry; new source entry.

Definitional-contradiction handling note: Per CLAUDE.md, the wiki carries both senses
of *"agentic engineering"* explicitly rather than silently picking one. The
practitioner-discipline sense remains primary in [[agentic-engineering]] (area) but
the control-plane sense is surfaced at the top of that page with pointers to
[[multi-agent-coordination]] and [[practitioner-discipline-vs-control-plane]]. Worth
revisiting whether the field settles on one meaning over time.

## [2026-05-28] ingest | Andy Dev Dan, "Top #1 Opportunity for Senior Engineers: Agentic Engineering"

Fourth primary voice added to the wiki. Andy Dev Dan is a YouTube channel host, owner
of *agenticengineer.com*, and seller of two courses (*Tactical Agent Coding*, *Agent
Horizon*). The source is a 26-minute "raw" monologue framed as a note-to-self,
explicitly referencing Karpathy's Sequoia Ascent talk as validation. Three judgment
calls confirmed with Juan: (a) spin out 3 new topic pages for genuinely new concepts
rather than fold everything; (b) faithful summary with an "about this source" caveat
at the top of the source page (channel-host with course business, several sales-shaped
claims); (c) leave [[willison-vs-karpathy]] alone for now rather than extend into a
multi-author synthesis — too much else in flux.

Pages created:
- Source: [[2026-05-28-andy-dev-dan-five-pillars]] (with top-of-page caveat)
- Person: [[andy-dev-dan]] (third primary practitioner voice, individual-senior-engineer vantage)
- Topics: [[agent-harness-engineering]], [[software-factory]], [[tokeconomics]]

Pages updated:
- [[agent-architecture]] — opening paragraph now points forward to [[agent-harness-engineering]] for the *discipline of building your own harness*; source count to 4.
- [[agent-native-infrastructure]] — added a callout linking the **token tax** as the economic case for the same agent-native work Karpathy frames in capability terms; source count to 4.
- [[economics-of-code]] — added a "return side — tokeconomics" subsection at the end of the verifiability layer; source count to 8.
- [[compound-engineering]] — added a "compound engineering ⊆ the software factory" subsection (substrate-level loop + workflow-level loop stack); source count to 6.
- [[multi-agent-coordination]] — added a "connection to solo-scale orchestration" subsection noting Andy's 3-tier orchestrator/team-leads/workers structure as the individual-engineer analog of Kumar & Ramagopal's Worker/Leader pattern; source count to 2.
- [[agentic-engineering]] (area) — opening synthesis now names Andy as third practitioner voice; habits list expanded with three new bullets (agent-harness-engineering, software-factory, tokeconomics) and the token-tax sharpening on the existing agent-native-infrastructure bullet; source count to 14.
- [[overview]] — promoted from three voices to four; expanded the cost-and-return discussion to three layers (engineering time / tokens / tokeconomics); added a substrate-maximalist paragraph naming the harness / factory / agentic-access stack; "state of the picture" rewritten with Andy's contributions and new remaining gaps (no primary PI-harness source; willison-vs-karpathy synthesis is now 2-of-4); source count to 14.
- `wiki/index.md` — added [[agent-harness-engineering]] to Foundations, [[tokeconomics]] to Economics-and-analytic-frames, [[software-factory]] to Practices; new person entry; new source entry; updated date.

The willison-vs-karpathy synthesis was deliberately left alone (per Juan). Worth
revisiting in a future lint pass — adding Andy as a third practitioner column and
Kumar/Ramagopal as the enterprise vantage would turn it into a 4-voice comparison.
Could be a new "four-voices" synthesis rather than an extension.

Vocabulary additions (now canonical in the wiki): *software factory / dark factory /
ADWs / ZTE*, *tokeconomics / token tax / token arbitrage*, *AFK agents* (as L3
deployment), *custom harness as discipline*, *specialization is the moat*, *"models
matter less and less"* (substrate-maximalism). Worth tracking against future sources
to see which terms persist and which fade.

## [2026-05-29] ingest | Cole Medin, "Harness Engineering: What Separates Top Agentic Engineers Right Now"

YouTube transcript (PDF, bilingual EN/ES auto-transcript). Cole Medin — AI-coding YouTuber,
creator of the open-source **Archon** harness builder. Source carries an Archon plug and a
paid Google Cloud Agent CLI sponsor segment; substance is comparatively measured. This is the
**second voice on [[agent-harness-engineering]]** (was single-source / Andy only), and the
fifth voice overall in the wiki.

Core contributions:
- **Three-layer harness model**: LLM (reasoning) → vendor coding-agent you pick (Claude Code /
  Codex / Pi) → the **AI layer you build**. The layer-2/3 distinction (rented vs. yours) is the
  load-bearing one.
- **Six AI-layer components**: global rules, skills, MCP servers, codebase search (LSP /
  knowledge graphs), hooks, sub-agents.
- **Harness engineering ≈ context engineering + control + ownership-mindset.** First source to
  name [[context-engineering]] as the predecessor.
- **"Every mistake becomes a rule" / system evolution** — compound engineering at the harness
  layer, as a mindset. Resolves the standing open question on whether harness engineering is
  "new harnesses" or "compounded modification of a base" (firmly the latter).
- **Orchestration as peak evolution** — separate plan/implement/validate sessions with markdown
  handoffs; parallel review agents (security/correctness/simplicity) gating PRs; the
  [[ralph-loop|Ralph loop]] (Geoffrey Huntley) as the minimal runnable factory; token-overwhelm
  as the rationale for decomposing.
- **Hooks**: pre-tool-use security, stop-validation (deterministic tests/lint/typecheck + forced
  iteration), lint-after-edit.

Pages created (4):
- Source: [[2026-05-29-cole-medin-harness-engineering]] (with Archon/sponsor caveat)
- People: [[cole-medin]] (second harness-engineering voice), [[geoffrey-huntley]] (stub; Ralph-loop
  originator, secondhand mention only)
- Topics: [[ralph-loop]] (stub), [[context-engineering]] (stub; created to home repeated
  cross-refs and the predecessor framing)

Pages updated (9):
- [[agent-harness-engineering]] — major: second voice; added the three-layer model, six-component
  AI-layer inventory, the context-engineering-evolution decomposition, and "system evolution";
  resolved the new-harness-vs-compound open question; source count 1 → 2.
- [[compound-engineering]] — added "every mistake becomes a rule" as the mindset form of the same
  loop at the harness layer; source count 6 → 7.
- [[software-factory]] — Cole as independent corroborating voice for the orchestration shape; Ralph
  loop as a concrete minimal factory; token-overwhelm rationale; source count 1 → 2.
- [[subagents]] — added the third unit ("orchestrated session" between sub-agent and Worker/Leader
  swarm); separate-session-per-phase with markdown handoffs; source count 2 → 3.
- [[agentic-testing]] — added the deterministic stop-validation hook as the mechanical complement to
  prompted testing discipline; source count 4 → 5.
- [[agent-code-review]] — added parallel single-focus reviewer agents as the agent-reviewer tier of
  the two-tier gate; source count 4 → 5.
- [[andy-dev-dan]] — noted Cole as partial independent corroboration of harness-primacy (both have
  commercial offerings).
- [[agentic-engineering]] (area) — expanded the harness-engineering habit bullet with Cole's
  structural model; source count 14 → 15.
- [[overview]] — promoted four → five voices; added Cole's three-layer model + system evolution +
  orchestration to the substrate section; rewrote "state of the picture" (harness engineering now
  2-source; no adversarial voice yet since both harness voices have commercial offerings; new
  load-bearing references: a primary harness-substrate source, a canonical context-engineering
  source); source count 14 → 15.
- `wiki/index.md` — added [[context-engineering]] + refreshed [[agent-harness-engineering]] line
  (Foundations), [[ralph-loop]] (Practices), [[cole-medin]] + [[geoffrey-huntley]] (People), source
  entry; updated date.

Note: [[context-engineering]] and [[ralph-loop]] are stubs resting on this single (secondhand, for
Ralph) source — flagged for a primary-source follow-up. The two harness-engineering voices both have
commercial offerings (Andy's courses, Cole's Archon), so the harness-primacy thesis is now corroborated
but still lacks a disinterested or skeptical source — the standing counter-perspective gap.

## [2026-05-30] diagram | Cole Medin, harness engineering — visual map

Built `wiki/syntheses/cole-medin-harness-engineering.excalidraw` following the project's
`excalidraw-diagram` skill end-to-end. Six sections in one composition:

1. **3-layer stack** (concentric rectangles, left) — LLM → coding agent → AI layer, mirroring
   Cole's "wrapper around the model" metaphor structurally rather than just labeling it.
2. **6 AI-layer components** (2×3 grid, center-right) — Rules, Skills, MCP, Codebase Search,
   Hooks, Sub-agents; Hooks visually highlighted (orange) because Cole flags it as the
   underused-but-most-leveraged component.
3. **Hooks evidence panel** (dark code-style strip) — concrete callout of Cole's three favored
   hook uses: `pre_tool_use`, `stop`, `post_edit`.
4. **System Evolution band** — Mistake → Diagnose → Add rule/hook/skill → Improved harness
   sequence with a dashed return arrow, anchored by the "every mistake becomes an opportunity"
   quote.
5. **Stage 2 / Foundational workflow** (bottom-left) — manual Plan / Implement / Validate
   sessions with markdown handoff artifacts between them.
6. **Ralph loop** (bottom-right) — automated pipeline inside a `while not done.txt:` dashed
   enclosure: PRD → Plan agent → Implement → 3 parallel reviewers (security, correctness,
   simplicity) → PR, with a bash snippet and the `done.txt → exit` escape branch.

Render-view-fix loop: one defect on first render (Ralph-loop return arrow routed awkwardly
*through* the dashed `while` enclosure, going down-and-back instead of looping around). Fixed by
rerouting the arrow *over the top* of the pipeline (PR → up → left → down to Plan agent), which
also reads more naturally as "loop back to the next iteration." Second render passed both the
vision check and the defect check.

Embedded in [[2026-05-29-cole-medin-harness-engineering]] under a new `## Diagram` section;
added to [[index]] under Syntheses; `index.md` date bumped 2026-05-29 → 2026-05-30.
