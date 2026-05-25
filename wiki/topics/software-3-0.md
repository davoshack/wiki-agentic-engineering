---
type: topic
tags: [agentic-engineering, paradigms, software-3-0, context-window, programming-paradigms]
created: 2026-05-25
updated: 2026-05-25
status: developing
sources: 1
---

# Software 3.0

[[andrej-karpathy]]'s framing of the latest shift in how software is produced. The compact form: **Software 1.0** is humans writing explicit code; **Software 2.0** is humans creating datasets, objectives, and neural-network architectures (the program is *learned* into weights); **Software 3.0** is humans programming **LLMs** through prompts, context, tools, examples, memory, and instructions. The **context window** is the new lever; the **LLM is the interpreter**.

## Synthesis

### The paradigm progression

| Paradigm | What humans write | What runs |
| --- | --- | --- |
| **Software 1.0** | Explicit code | Code on a CPU |
| **Software 2.0** | Datasets + objectives + architectures | Learned weights in a neural net |
| **Software 3.0** | Prompts + context + tools + examples + memory + instructions | An LLM interpreting that context |

Karpathy's claim in [[2026-04-30-sequoia-ascent-karpathy]] is that once LLMs were trained on a sufficiently broad task distribution, they implicitly became **programmable computers**. The user's lever is what's in the context window; the LLM "executes" by interpreting it and performing computation in digital information space.

This is a different *kind* of program — less precise, more adaptive. The Software 3.0 installer Karpathy describes is no longer a brittle shell script with cross-platform conditionals but **a block of text you paste into an agent**, which reads the local environment, debugs errors, and adapts. The shell-script form is rigid Software 1.0; the paste-block is Software 3.0.

### "Some software should stop existing"

The starkest implication is that **certain whole applications should disappear into direct model transformations.** Karpathy's worked example: **MenuGen**.

- **Old (Software 1.0/SaaS):** photo of menu → OCR → image generator → frontend, deploy, auth, payments, secrets. A complete app with infrastructure.
- **Software 3.0:** photo of menu → multimodal model (Gemini + Nano Banana) → returns the menu image with dish pictures rendered directly into the pixels.

Most of the old app was scaffolding around a transformation the model can now perform directly. The reframe Karpathy presses on founders: *"AI is not just a faster way to build the old apps. Some apps should stop existing as apps."*

### Connection to architecture

The mechanics ([[agent-architecture]]) explain *how* a Software 3.0 program runs: an LLM with a context window, system prompt, and tools, in a loop. The Software 3.0 framing is the *paradigm-level* description of what's happening when you do that. Two practical consequences sit at this interface:

- **The context window is the program.** Anything you fit into it — prompts, examples, repo content, tool definitions, accumulated lessons via [[compound-engineering]] — is the program's source. Anything you keep out is unavailable to the interpreter.
- **Context-management practices are now programming practices.** Hoarded artifacts ([[hoarding-working-examples]]), subagents ([[subagents]]), and Git-driven session seeding ([[git-with-agents]]) are all ways of curating what the interpreter sees.

### Connection to the cost story

[[economics-of-code]] argues that producing code became cheap. Software 3.0 is a complementary claim: even when code-production is cheap, **some software shouldn't be produced at all** because the LLM can directly transform input into output without intermediate code. The cost saving compounds — first cheaper code, then less code needed.

### Information transformations that weren't possible before

Karpathy's other Software 3.0 illustration is the **LLM Wiki Pattern** (the pattern this wiki is built on): take messy human documents, incrementally compile them into a persistent markdown knowledge base — summaries, entity pages, contradictions, evolving syntheses — that no classical program could maintain. The reframe he presses: *"Don't only ask 'what existing workflow can AI speed up?' Also ask 'what information transformation was impossible before, but is now natural?'"*

## Open questions

- The paradigm progression suggests a possible Software 4.0 — Karpathy gestures at *"completely neural computers"* where neural nets are the host process and CPUs become coprocessors. How close is that, and what's the practical implication today?
- Where is the line between a Software 3.0 program and a Software 1.0 program that *uses* an LLM? Many production systems will be hybrids. Are there design principles for choosing which layer does which work?
- For founders: how do you tell when an app *should* disappear into a direct model transformation vs. when scaffolding is still load-bearing (latency, cost, correctness guarantees, UI affordances)?
- How does the "context window is the program" framing interact with [[compound-engineering|the compounding-instructions practice]]? Is the system prompt the persistent runtime configuration, while per-task context is the program?

## Sources

- [[2026-04-30-sequoia-ascent-karpathy]]
