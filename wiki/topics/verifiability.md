---
type: topic
tags: [agentic-engineering, verifiability, jagged-intelligence, rl, feedback-loops]
created: 2026-05-25
updated: 2026-05-25
status: developing
sources: 1
---

# Verifiability and jagged intelligence

[[andrej-karpathy]]'s analytic frame for predicting *where* AI will dominate next and *why* current models have such uneven capability. The compact form: **traditional software automates what you can specify; LLMs automate what you can verify.** Tasks with automatic reward signals are practiceable in reinforcement learning, which is why coding, math, games, and benchmarks improve fast. Capability across tasks is **jagged**, not smooth — models spike where they were verifiably trained and underperform elsewhere.

## Synthesis

### The verifiability thesis

In [[2026-04-30-sequoia-ascent-karpathy]], Karpathy contrasts two automation regimes:

- **Traditional software** automates what you can **specify**. If you can write the rules, the computer can run them.
- **LLMs (with RL)** automate what you can **verify**. If you can detect whether an attempt succeeded or failed, the model can practice the task across millions of attempts.

The training pipeline behind this is concrete: frontier labs train LLMs in giant **reinforcement learning environments with verification rewards**. Tasks that are *resettable, repeatable, and rewardable* — math, coding, tests, benchmarks, games, many engineering tasks — get tight feedback loops and progress rapidly.

This is also why **coding agents feel dramatically better than ordinary chatbots**: coding gives the model continuous feedback. Tests pass or fail, programs run or crash, diffs can be inspected, benchmarks can be measured. The verifiability of code is what makes [[coding-agents]] uniquely effective relative to other LLM applications.

### Jagged intelligence

Verifiability alone doesn't predict capability. Karpathy's refinement: **what labs choose to emphasize** matters at least as much. Approximate formula:

```
capability spike ~= verifiability × training attention × data coverage × economic value
```

Each factor compounds: a task can be verifiable in principle and still underperform if labs haven't built RL environments for it. A task with low economic value may stay neglected even when it's perfectly verifiable.

Karpathy's worked illustrations:
- **Chess** improved sharply from GPT-3.5 to GPT-4 — not because general intelligence smoothly progressed everywhere, but reportedly because a large amount of chess data was added to the training mix.
- **"How many letters are in strawberry?"** was a famous failure case; it's now patched.
- **Driving vs. walking 50m to a car wash:** state-of-the-art models may tell you to walk *because it's close*, even though the question implies you're going to a car wash. *"How is it possible that a state-of-the-art model can refactor a 100,000-line codebase or find zero-day vulnerabilities, yet tells me to walk to the car wash? That's jaggedness."*

The takeaway: **frontier models do not come with a manual.** They are artifacts of pretraining mixes, RL environments, benchmark pressure, product priorities, and economic incentives. They spike in some places and behave strangely in others — *"jagged, alien tools"* (see [[agent-architecture]] on **ghosts not animals** for the mental-model framing).

### "Are you on the model's rails?"

The practical question Karpathy presses for any application:

> Are you in a region of the task space that is **verifiable** and was **heavily trained**?

If yes, the model flies and you can build aggressively. If no, you need to compensate:
- Better context (relevant info loaded explicitly — see [[hoarding-working-examples]], [[git-with-agents]]).
- Better tools (lean on tool-call coverage rather than internal model knowledge).
- Better evals (build your own scoring function so you can detect drift).
- Fine-tuning or your own RL environment (the most ambitious response).

### Founder implication: valuable, verifiable, undertrained

Karpathy's startup wedge follows directly: **find domains that are valuable, verifiable, and not yet heavily targeted by frontier labs.** Build a domain-specific environment where models can try actions and receive reliable rewards; fine-tune or run RL on it; benefit even if the base model is unremarkable in that area.

The most obvious verifiable domains (coding, math) are already saturated. Many *economically important* domains have latent verifiable structure that hasn't been exploited — *"that is a startup wedge."*

### Connection to the rest of the wiki

- **Coding** is the canonical verifiable domain. [[coding-agents]] are effective precisely because coding fits the verifiability profile. The "feedback loops" Karpathy names map directly onto Willison's [[economics-of-code|9-point good-code]] requirement that code be *tested* and *known to work*.
- **Test-runner subagents** ([[subagents]]) are an architectural use of verifiability — running the test suite is the canonical verifier.
- **`git bisect`** ([[git-with-agents]]) is verifiability applied to history — the bug-condition test is the reward signal.
- **Compound engineering** ([[compound-engineering]]) is a verifiability practice at the workflow level — the retrospective is a structured signal that the agent harness reads next time.
- **Tasteful simplification** (Karpathy's `microGPT` story) is an **off-rails** task — *"the models hate this"* — and a useful warning that not everything productive is verifiable.

## Open questions

- For a given task, how do you efficiently *detect* whether you're on the model's rails before committing engineering effort? Karpathy describes the diagnosis but not a recipe.
- What's the practical bar for "verifiable" in a startup context? Continuous numerical reward is the strongest form; sparse / binary signals are weaker; LLM-as-judge evaluations are weaker still but often practical (Karpathy mentions "a council of LLM judges" for writing).
- Are there meta-patterns for *making* a fuzzy domain more verifiable (decomposition, proxies, instrumentation)?
- How do you balance optimizing for current-model rails (today's wedge) against the model improving and absorbing your moat (tomorrow's exposure)?
- The formula above is rough. Are there cases where the four factors trade off non-multiplicatively — e.g., huge economic value compensating for low verifiability?

## Sources

- [[2026-04-30-sequoia-ascent-karpathy]]
