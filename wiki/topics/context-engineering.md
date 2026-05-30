---
type: topic
tags: [agentic-engineering, context-engineering, context-window, prompting]
created: 2026-05-29
updated: 2026-05-29
status: stub
sources: 1
---

# Context engineering

The deliberate practice of curating **what goes into a coding agent's context window** — rules, examples, retrieved code, tool outputs, memory — so the model has the right information, and only the right information, to do the task well. Named in the wiki primarily as the **predecessor that [[agent-harness-engineering|harness engineering]] evolves from**.

## Synthesis

[[cole-medin|Cole Medin]] positions context engineering as "last year's big thing" and [[agent-harness-engineering|harness engineering]] as "this year's" — and is explicit that the two heavily overlap: *"most of the harness around the model… is just context engineering — your context injection, your actions through tools and MCPs, persistence, observability."* In his framing, harness engineering = context engineering **plus** two genuinely new ingredients: **control** (orchestrating sessions/sub-agents, the [[ralph-loop|Ralph loop]]) and the **system-evolution mindset** ([[compound-engineering|every mistake becomes a rule]]). See [[2026-05-29-cole-medin-harness-engineering]].

The wiki has been doing context engineering under other names since the start:

- [[agent-architecture]] establishes *why* it matters mechanically — the context window is the program ([[software-3-0]]), quality often degrades past ~200K tokens, and the harness replays the whole conversation each turn.
- [[subagents]] is, at root, a context-engineering move: dispatch heavy/verbose work to a fresh window to **preserve the parent's root context**.
- [[hoarding-working-examples]] supplies *examples* as a context ingredient; [[compound-engineering]] supplies accumulated *instructions*; [[agentic-testing]]'s `First run the tests` seeds the right context at session start.

This page is intentionally a **stub**: the wiki has only one source that names context engineering directly, and that source treats it mostly as the *baseline* harness engineering builds on rather than defining it in its own right. It exists to give the repeated cross-references a home and to mark a concept worth a dedicated source.

## Open questions

- **No primary source on context engineering itself.** The term is used as a known predecessor, not taught. A dedicated source (a canonical 2025 write-up) would let this page move past stub.
- Where is the real boundary between *context engineering* and *harness engineering*? Cole draws it at "control + mindset," but that line is one practitioner's cut and worth testing against other voices.
- Which of the wiki's existing practices are best understood as context engineering vs. something else? A cleaner taxonomy would help (cf. [[agent-architecture]], [[subagents]], [[compound-engineering]]).

## Sources

- [[2026-05-29-cole-medin-harness-engineering]]
</content>
