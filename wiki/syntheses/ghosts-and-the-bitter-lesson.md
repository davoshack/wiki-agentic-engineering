---
type: synthesis
tags: [meta, agentic-engineering, mental-model, bitter-lesson, ghosts-vs-animals, philosophy]
created: 2026-05-25
updated: 2026-05-25
status: developing
sources: 1
---

# Ghosts and the Bitter Lesson

[[andrej-karpathy]]'s **ghosts-not-animals** framing and Richard Sutton's **The Bitter Lesson** (2019) are two anti-anthropomorphic stances about AI, applied at opposite ends of the same pipeline. Sutton speaks to the *researcher building the system*: don't bake in your human-knowledge intuitions about cognition — let general methods scale with compute. Karpathy speaks to the *practitioner using the resulting system*: don't anthropomorphize what comes out — it's not a human mind. Read together, they bracket the arc: same epistemic discipline applied at design-time and at use-time, with the alien artifact in between.

![[ghosts-and-the-bitter-lesson.png]]
*Diagram source: [[ghosts-and-the-bitter-lesson.excalidraw]] — built with the project's `excalidraw-diagram` skill.*

> **Wiki note**: Sutton is not yet ingested. The Bitter Lesson half of this page draws on [the original 2019 essay](http://www.incompleteideas.net/IncIdeas/BitterLesson.html), not a wiki source page. Once ingested, this page should be updated to cite [[2026-XX-XX-bitter-lesson|the source page]] directly and a `topics/bitter-lesson.md` page should anchor the upstream theoretical claim.

## The two frames, compactly

### Sutton — *The Bitter Lesson*

The biggest lesson from 70 years of AI research: **general methods that leverage computation** are ultimately the most effective by a wide margin. The two general methods are **search** and **learning**, both of which scale arbitrarily with compute. Researchers repeatedly try to bake in human-knowledge models of how cognition should work (chess heuristics, hand-engineered vision features, linguistic rules) — short-term wins, long-term losses to systems that just scale compute and data.

The prescription: build **meta-methods** that *find* complexity from data, not methods that *encode* your guesses about it. The bitterness is for researchers attached to their elegant theories about cognition; the lesson is that what works at scale doesn't respect those theories.

### Karpathy — *Ghosts, not animals*

The system that results from doing that is **not an animal**. No biological drives, no embodied survival pressure, no curiosity, play, or intrinsic motivation in the animal sense. It is a **statistical simulation of human artifacts**, shaped by pretraining, post-training, RL, product feedback, and economic incentives. *"Brilliant in one moment and bizarrely dumb in the next."* Anthropomorphic expectations mislead. The right posture is **empirical familiarity**: learn where it works, where it fails, what it was trained for, and how to build guardrails around it. See [[agent-architecture]] for the framing in its working context, and [[2026-04-30-sequoia-ascent-karpathy]] for the source.

## How they connect

### 1. Anti-anthropomorphism in two stages

| Stage | Whose intuitions are dangerous | What to do instead |
| --- | --- | --- |
| **Design** (Sutton) | The researcher's model of how cognition should work | Build general methods that scale; let the system learn |
| **Use** (Karpathy) | The user's model of what the resulting system is like | Treat it empirically; learn its actual shape, not the imagined one |

Same epistemic discipline, applied at sequential moments. Both insist human intuitions about cognition mislead; they just disagree about *which* intuitions are most dangerous in *which* role. Sutton's quarrel is with the researcher who thinks they know how to encode cognition. Karpathy's quarrel is with the user who thinks the resulting system thinks like they do.

### 2. The ghost is the natural artifact of taking Sutton seriously

If you spend decades scaling **general methods** with massive compute (Sutton's prescription), what you eventually produce is precisely what Karpathy describes: a system whose capabilities are *whatever fell out of the training mix*, shaped by pretraining mixture, RL environments, product feedback, and economic incentives.

This is exactly the mechanism Karpathy enumerates. The "shaped by" list in the ghosts framing reads as the *recipe* a Bitter-Lesson researcher would follow:

- Pretraining (general learning, scaled by compute) — Sutton's "learning" pillar.
- Post-training / RL (more general learning, with reward signals) — still Sutton.
- Product feedback and economic incentives (the human-side signal that decides *what* gets optimized) — the part Sutton's essay barely addresses.

Sutton predicted the *shape* of the system; Karpathy described what living with it actually feels like.

### 3. Jagged intelligence is the practitioner's view of "scales with computation"

Karpathy's [[verifiability|jagged intelligence]] formula — `capability ≈ verifiability × training attention × data coverage × economic value` — is essentially **Sutton's thesis written backwards from the practitioner's perspective**. Sutton says capability follows compute applied via general methods. Karpathy says capability spikes where labs *chose to apply* that compute and stagnates elsewhere.

The classic example (a state-of-the-art model can refactor a 100K-line codebase yet tells you to walk 50m to a car wash) is exactly the failure mode Sutton's framework predicts: general methods don't promise *uniform* competence — they promise competence wherever the computation was directed. Coding is heavily targeted with verifiable RL; common-sense everyday reasoning isn't, in the same way.

So **the ghost is jagged** because the Bitter Lesson doesn't give you uniformity for free. It gives you whatever you computed on.

### 4. Where the emphases part company

| Sutton | Karpathy |
| --- | --- |
| **Prescriptive** — to the researcher | **Descriptive** — to the practitioner |
| **Optimistic** — keep scaling; that's the win | **Pragmatic** — given the resulting system, here's how to live with it |
| Treats the alien-ness as a *consequence* worth accepting | Treats the alien-ness as a *condition* to handle (with guardrails, evals, harness updates) |
| Argues *what* to do at the research frontier | Argues *how to relate* to what falls out |

They don't disagree. They cover different ground in the same arc.

## What each leaves open

- **Sutton** doesn't address what you should *do* once you have the resulting system — that's where Karpathy picks up, and where the wiki's entire practice layer continues: [[agent-code-review]], [[refactoring-with-agents]], [[compound-engineering]], [[git-with-agents]].
- **Karpathy** doesn't engage with whether the alien-ness *narrows* over time as labs target more verifiable domains. A Sutton-style optimist would predict it does (more compute → more coverage). A skeptic would say the most economically valuable verifiable domains will be filled first and the rest left under-served indefinitely. The wiki currently has no source on either side of this disagreement.

## Implications for the wiki

- The Bitter Lesson is the **upstream theoretical claim** underneath multiple frames already in the wiki: [[verifiability]], jagged intelligence, the ghosts-not-animals section of [[agent-architecture]], and Karpathy's enumeration of what shapes the resulting system in [[2026-04-30-sequoia-ascent-karpathy]]. Ingesting Sutton would let those references resolve into a single canonical source.
- After ingesting Sutton, a `topics/bitter-lesson.md` page would be a natural home and could be wired in as a wikilink from at least [[verifiability]], [[agent-architecture]], and this page.
- The unresolved question above — *does jaggedness narrow with more compute, or stay structurally jagged?* — is a worth-tracking open question and the kind of place a deliberately adversarial source could land.

## Sources

- [[2026-04-30-sequoia-ascent-karpathy]] — the ghosts-not-animals framing in its full context.
- *(Not yet ingested)* Richard Sutton, "The Bitter Lesson" (2019), http://www.incompleteideas.net/IncIdeas/BitterLesson.html — the upstream theoretical claim. Treat the Bitter Lesson content above as drawn from outside the wiki until this is added.
