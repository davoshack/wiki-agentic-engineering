---
type: person
tags: [agentic-engineering, practitioner, youtuber, harness-engineering, archon]
created: 2026-05-29
updated: 2026-05-29
status: stub
sources: 1
---

# Cole Medin

A YouTuber in the AI-coding / agentic-engineering space and the creator of **Archon**, an open-source "harness builder." Enters the wiki as the **second practitioner voice on [[agent-harness-engineering]]**, alongside [[andy-dev-dan]].

## Synthesis

Cole's contribution in [[2026-05-29-cole-medin-harness-engineering]] is the **clearest structural model of the harness** in the wiki so far. Where [[andy-dev-dan|Andy Dev Dan]] asserts harness *primacy* ("whoever controls the harness controls your results") without diagramming it, Cole supplies the diagram:

- A **three-layer model** — the LLM (reasoning) → the coding agent you pick (Claude Code / Codex / Pi, itself a vendor-built harness) → **the AI layer you actually build**.
- The **six components of the AI layer** — global rules, skills, MCP servers, codebase search (LSP / knowledge graphs), hooks, sub-agents.
- A **two-stage account** of the discipline: engineering the AI layer *within a single session* (a direct evolution of [[context-engineering]]), and *orchestrating many sessions* into an automated workflow (the [[ralph-loop|Ralph loop]] as the worked example).

His sharpest framing is the **mindset** one: *"every mistake becomes an opportunity to improve your harness"* — what he calls **system evolution**, the human as feed-forward operator. This is [[compound-engineering]] relocated to the harness layer and elevated to a posture, and it's the most direct answer the wiki has to the open question of whether harness engineering is "new harnesses" or "compounded modifications to a base."

**Caveats worth holding** (a flag, not a dismissal):

- He **promotes Archon**, his own open-source harness builder, as the recommended on-ramp. He demonstrably ships (the video shows working systems), and the pitch is open-source rather than a paid course — so the conflict is softer than [[andy-dev-dan|Andy's]] course business, but it's still a vendor-of-his-own-tool stance.
- The video carries a **paid Google Cloud Agent CLI sponsor segment** that is advertising, not analysis.
- Style is **explainer-grade and comparatively measured** — he explicitly calls out which parts of "harness engineering" are buzzword fluff vs. worth knowing, which is a point in his favor relative to influencer-maximalist framings.

A useful posture: Cole is a good source for the *structure and vocabulary* of the harness (the layers, the six components, the session-orchestration pattern); treat the Archon recommendation as one option among harness builders, not a settled choice.

## Open questions

- What is Cole's actual background / day job? The video reads as a content creator's explainer; knowing whether he ships production systems professionally would calibrate how much weight his prescriptions carry.
- **Archon** is referenced as his open-source harness builder but the wiki has no primary source on it. Ingesting its docs/README would let this page and [[agent-harness-engineering]] characterize a *second* concrete harness substrate (alongside the PI harness [[andy-dev-dan|Andy]] depends on).
- He links a "companion repo" and a deeper-dive video on rules/skills/LSP/hooks — either would deepen the [[agent-harness-engineering]] component-by-component account.
- How does Cole's three-layer model line up with [[andy-dev-dan|Andy's]] harness/factory/access-surface decomposition? They're describing overlapping territory with different cuts; a reconciliation would be a worthwhile synthesis once a third harness-engineering source lands.

## Sources

- [[2026-05-29-cole-medin-harness-engineering]]
</content>
