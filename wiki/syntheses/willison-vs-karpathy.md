---
type: synthesis
tags: [meta, agentic-engineering, comparison, multi-author]
created: 2026-05-25
updated: 2026-05-25
status: developing
sources: 9
---

# Willison vs. Karpathy: practices and paradigms

The wiki's first cross-author synthesis. With both voices now represented — eight chapters from [[simon-willison]]'s *Agentic Engineering Patterns* guide and Karpathy's [[2026-04-30-sequoia-ascent-karpathy|Sequoia Ascent 2026 talk]] — it's worth stepping back to compare. The short version: they agree on substance and divide labor on framing. Willison gives the wiki its *practices and operational discipline*; Karpathy gives it the *paradigms and analytic frames*. Where they overlap, they reinforce. Where they don't overlap, each fills a gap the other leaves.

## What each is contributing

### Willison — practices and operational discipline

The eight chapters ingested so far form a coherent practitioner's manual. The throughline is **what to *do* now that coding agents are real**:

- Define the field and the vocabulary ([[2026-05-23-what-is-agentic-engineering]], [[2026-05-23-how-coding-agents-work]]).
- Characterize the economic shift and what "good code" means in the new regime ([[2026-05-23-writing-code-is-cheap-now]]).
- Prescribe what to spend the cheap-code surplus on — refactoring, exploratory prototyping, compound engineering ([[2026-05-23-ai-should-help-us-produce-better-code]]).
- Name the first anti-pattern (unreviewed PRs) and the good-PR checklist ([[2026-05-23-anti-patterns-things-to-avoid]]).
- Give concrete prompt vocabulary for hoarding ([[2026-05-23-hoard-things-you-know-how-to-do]]), Git ([[2026-05-23-using-git-with-coding-agents]]), and subagents ([[2026-05-23-subagents]]).

Willison's frame is **continuity with pre-LLM craft**. Many patterns ("hoard working examples", "review your own PR", "use Git ambitiously") are explicit extensions of advice that was already good — amplified by the new substrate.

### Karpathy — paradigms and analytic frames

The Sequoia talk is fewer pages but denser with named ideas. The throughline is **how to think about what just happened**:

- **December 2025** as a discrete inflection point.
- **Software 1.0 / 2.0 / 3.0** as the paradigm progression ([[software-3-0]]).
- **Verifiability** + **jagged intelligence** as the analytic frame for *where* AI dominates ([[verifiability]]).
- **Vibe coding vs. agentic engineering** as the canonical floor/ceiling framing (Karpathy coined both terms; this is now the source-of-record).
- **Ghosts not animals** as the mental model for LLM behavior ([[agent-architecture]]).
- **Agent-native infrastructure** built around sensors and actuators ([[agent-native-infrastructure]]).
- Founder-oriented questions: *what becomes possible? what software should disappear? where is the verifiable, valuable, undertrained wedge?*

Karpathy's frame is **paradigm-naming**. He invests heavily in giving the new things names that stick, then uses those names to do analysis.

## Where they align

The substantive agreement is large enough to be worth tabulating:

| Topic | Willison's framing | Karpathy's framing | How they reinforce |
| --- | --- | --- | --- |
| Vibe coding | Keep the narrow Karpathy definition (unreviewed prototype-quality output); don't let it expand to cover all LLM-assisted work | Vibe coding **raises the floor**; agentic engineering **raises the ceiling** | Karpathy's floor/ceiling sharpens what Willison was defending |
| "Good code" / quality bar | 9-point checklist (works, known to work, solves right problem, handles errors, simple, tested, documented, future-affording, "ilities") | Agentic engineering preserves *"correctness, security, taste, and maintainability"* | Karpathy's compact list maps directly onto Willison's checklist |
| Human's role | Choose what to build, equip with tools, specify, verify, iterate | Spec design, plan supervision, diff inspection, evaluation loops, permissioning, worktree isolation | Identical decomposition; Willison enumerates, Karpathy lists |
| Code review responsibility | First review pass is *your* job; agent PR descriptions need reviewing too | MenuGen Stripe/Google email bug — agent produces plausible code, human needs system-design judgment | Same point with different worked examples |
| Hoarding artifacts | Personal collection of runnable code that proves capability | `microGPT` as a dependency-free educational artifact; LLM Wiki Pattern; copy-pasteable installation skills | Karpathy's examples are concrete instances of Willison's pattern |
| Compounding lessons | Compound engineering (Shipper/Klaassen) — retrospectives → updated harness | *"Define context / tools / feedback loop / guardrails"* recipe; agent-native docs as durable artifacts | Karpathy's recipe describes what gets compounded |
| Cost shift | Code is cheap, *good* code is still expensive | Less scarce: code/recall/boilerplate. More scarce: understanding/taste/eval/security | Same economic claim from different angles |
| Verifiable feedback | Code's testability is what makes agents work in coding (Git ch. on automated tests in merge-conflict resolution) | Verifiability is the central analytic frame for *where* AI dominates | Karpathy gives Willison's practical observation a name |
| Sub-agents / tools | Tool-call loop; subagent flavors (exploratory, parallel, specialist) | Sensors and actuators as the product-level surface | Willison's *agent-side* mechanics + Karpathy's *world-side* surfaces are the same idea on opposite sides of the boundary |

The overall pattern: **Willison observes a practice; Karpathy gives it a frame**, or **Karpathy names a paradigm; Willison gives it a workflow**.

## Where they diverge — emphases, not contradictions

There are no clean contradictions. But each emphasizes things the other doesn't:

- **Willison underweights** the paradigm-shift question: he largely takes the current toolset (Claude Code, Codex, Gemini CLI) as a baseline and asks *"how do I work well inside it?"* He doesn't press the *"some apps should stop existing"* claim or the *"context window is the new program"* claim. The Software 3.0 reframe is absent.
- **Karpathy underweights** operational discipline: the Sequoia talk gestures at *"design specs, supervise plans, inspect diffs, write tests, create evaluation loops, manage permissions, isolate worktrees"* in a single sentence; Willison spends entire chapters on each. No prompt vocabulary, no PR checklists.
- **Willison is silent on founders / startup strategy.** Karpathy spends time on the founder lens (valuable + verifiable + undertrained domains, agent-native infrastructure as a wedge, MenuGen as an "apps that should disappear" example).
- **Karpathy is silent on the day-to-day artifacts** that make a team productive: no Git workflow chapter, no anti-patterns list, no good-PR checklist, no async-agent + worktree pattern.
- **Tone.** Willison's writing is even and grounded in worked examples from his own shipped projects. Karpathy's is more sweeping, more willing to predict (December 2025 inflection, neural computers in the limit, 10x→much-more-than-10x engineers).

A useful way to read them together: **Karpathy tells you what's happening and where to look; Willison tells you what to do tomorrow morning.**

## What's still missing from the wiki after both voices

Both authors share blind spots worth noting:

- **No empirical / adversarial perspective.** Both are AI-positive practitioners. Skeptics, large-scale quality studies, security-research perspectives, and enterprise-context framings are absent from both.
- **Limited treatment of teams / collaboration.** Both are framed for individual or small-team practice. Multi-team coordination, code-ownership norms, review-load-at-scale aren't addressed by either.
- **Light on evaluation methodology.** Both name "evals" as important; neither walks through what good ones look like in practice.
- **No vendor-comparison.** Willison links across Claude Code / Codex / Gemini CLI and names vendor-specific behaviors in passing; Karpathy treats vendor differences as out of scope. The portability question raised across multiple wiki pages remains unresolved.
- **Compound engineering operational mechanics.** Both reference the pattern; neither walks through what a good "compound step" actually looks like or where the compounded instructions live by default.

## Implications for the wiki

- **Vocabulary is now stable.** "Coding agents," "harness," "tools in a loop," "vibe coding," "agentic engineering," "Software 3.0," "verifiability," "jagged intelligence," "ghosts not animals," "sensors and actuators" — these terms have canonical sources now. Future ingests can use them without re-defining.
- **The paradigm/practice split is a useful spine.** When ingesting future sources, ask: is this contributing a new *frame* (extending Karpathy's layer) or a new *practice* (extending Willison's layer)?
- **Counter-perspectives should be deliberately sought.** Both authors are sympathetic to the same overall thesis. The wiki's blind spots are theirs.

## Sources

- [[2026-05-23-what-is-agentic-engineering]]
- [[2026-05-23-writing-code-is-cheap-now]]
- [[2026-05-23-hoard-things-you-know-how-to-do]]
- [[2026-05-23-ai-should-help-us-produce-better-code]]
- [[2026-05-23-anti-patterns-things-to-avoid]]
- [[2026-05-23-how-coding-agents-work]]
- [[2026-05-23-using-git-with-coding-agents]]
- [[2026-05-23-subagents]]
- [[2026-04-30-sequoia-ascent-karpathy]]
