---
type: person
tags: [agentic-engineering, author, primary-source, paradigms]
created: 2026-05-25
updated: 2026-05-25
status: developing
sources: 1
---

# Andrej Karpathy

Founding member of OpenAI; former director of AI at Tesla (Autopilot); founder of [Eureka Labs](https://eurekalabs.ai/) (AI-native education). One of the most influential public commentators on AI, both as a teacher (his neural-networks lectures, micrograd, nanoGPT, microGPT) and as a coiner of vocabulary that the field then adopts. The second primary voice in this wiki (alongside [[simon-willison]]) and the originator of several of the frames the wiki rests on.

## Synthesis

A few features of Karpathy's perspective worth holding onto when reading his pages here:

- **Paradigm-namer.** Karpathy invests heavily in *naming* the shifts. **Software 1.0 / 2.0 / 3.0** (see [[software-3-0]]), **vibe coding** (Feb 2025 tweet that the field then absorbed), **agentic engineering** (used in the Sequoia talk as the disciplined complement to vibe coding), **jagged intelligence**, **ghosts-not-animals** (see [[agent-architecture]]). When a Karpathy term takes hold, it's load-bearing.

- **Teacher's bias toward distilled artifacts.** Many of his contributions are deliberately small, inspectable educational artifacts: `nanoGPT`, `microGPT` (a complete GPT training + inference implementation in a single dependency-free Python file). The educational framing is also load-bearing: in the Sequoia talk he says *"you can outsource your thinking, but you can't outsource your understanding"* — agents change the workflow but the human still has to understand.

- **Originator of the LLM Wiki Pattern that inspired this wiki.** His [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) and a [follow-up X post](https://x.com/karpathy/status/2039805659525644595) are credited in the project README. This wiki is a direct application of that pattern — making him uniquely entangled with the wiki's *form*, not just its *contents*.

- **Verifiability lens.** His framing — *"Traditional software automates what you can specify; LLMs automate what you can verify"* — is the cleanest analytic frame in the wiki for predicting which tasks AI will dominate next. The corollary, [[verifiability|jagged intelligence]], explains why state-of-the-art models can refactor 100K-line codebases yet tell you to walk to a car wash 50m away.

- **Founder lens.** Karpathy's talks tend to translate technical observations into startup wedges: find a **valuable, verifiable, undertrained** domain; build **agent-native infrastructure** (see [[agent-native-infrastructure]]); ask *"what software should disappear into direct model transformations?"* (his MenuGen example). This complements Willison's more practitioner-oriented framing.

The wiki's working analytic stance after ingesting both voices: Willison gives us the *practices* and the *operational discipline*; Karpathy gives us the *paradigms* and the *frames*. They mostly agree on substance — see [[willison-vs-karpathy]] for the explicit comparison.

## Open questions

- How does Karpathy's worldview evolve as he runs Eureka Labs? His current thinking is heavily shaped by being a founder *applying* these patterns to education.
- He's a prolific tweeter and blogger; the wiki has only one ingested source so far. Many of his ideas (Software 3.0, verifiability, ghosts vs. animals) have their own original posts that would be worth ingesting directly rather than relying only on the Sequoia summary.
- The LLM Wiki Pattern itself: where does it go from here? Is there a v2? Have other people written publicly about adopting it?
- What does Karpathy *disagree* with in the practitioner literature (Willison and others)? Most of his Sequoia comments align; explicit disagreements may be worth surfacing as the corpus grows.

## Sources

- [[2026-04-30-sequoia-ascent-karpathy]]
