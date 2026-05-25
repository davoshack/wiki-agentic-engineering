---
type: source
source_type: transcript
source_url: https://karpathy.bearblog.dev/sequoia-ascent-2026/
source_date: 2026-04-30
tags: [agentic-engineering, software-3-0, verifiability, jagged-intelligence, vibe-coding, agent-native, ghosts-vs-animals, llm-wiki-pattern]
created: 2026-05-25
updated: 2026-05-25
status: developing
---

# Sequoia Ascent 2026: Karpathy in conversation with Stephanie Zhan

Andrej Karpathy's fireside chat at Sequoia Ascent 2026 (April 30, 2026), published as both an LLM-generated summary and a lightly cleaned transcript on his blog. The conversation is wide-ranging but coheres around a single thesis: AI is becoming a **new operating layer for digital work**, and the unit of programming is shifting from typing code to orchestrating agents. Karpathy introduces or sharpens several major frames: the **December 2025 agentic inflection**, **Software 3.0**, **verifiability** + **jagged intelligence**, the canonical **vibe coding vs. agentic engineering** distinction (he coined both), **ghosts-not-animals** as a mental model, and **agent-native infrastructure** built around sensors and actuators.

## Key takeaways

### December 2025 agentic inflection

- Karpathy: *"I have never felt more behind as a programmer."* For most of 2025, tools like Claude Code and Codex required frequent correction. **Around December 2025 he experienced a step change** — generated chunks got larger, more coherent, more reliable; he started trusting the agents with more of the work.
- The **unit of programming changed** from typing lines of code to delegating "macro actions": implement this feature, refactor this subsystem, research this library, set up this service, write tests + run + fix, compare approaches and propose a plan.
- *"The programmer is increasingly not just a code writer, but an orchestrator of agents."*

### Software 3.0

- **Software 1.0:** humans write explicit code.
- **Software 2.0:** humans create datasets, objectives, and neural networks; the program is learned into weights.
- **Software 3.0:** humans program LLMs through **prompts, context, tools, examples, memory, and instructions**. The LLM is the **interpreter**; the **context window is the lever**.
- Installation example: instead of a brittle shell script with conditionals across many environments, the installer is a **block of text you paste into an agent**. The agent reads the local environment, debugs errors, adapts to the machine. Less precise, more adaptive.

### MenuGen and "software that should disappear"

- **MenuGen** (a worked example from his blog) was a traditional app: photo of restaurant menu → OCR dish names → image generator → render UI. Required frontend, APIs, image gen, deploy, auth, payments, secrets.
- The **Software 3.0 version**: take the photo, give it to a multimodal model (Gemini + Nano Banana), ask it to *render dish images directly onto the menu image*. Much of the app disappears. The neural network does the transformation directly.
- *"AI is not just a faster way to build the old apps. Some apps should stop existing as apps."*

### The new opportunity isn't just faster programming

- LLMs automate **forms of information processing that were not previously programmable.**
- His **LLM Wiki Pattern** is the cleanest example: instead of RAG over raw documents each time, an agent incrementally compiles raw sources into a persistent markdown wiki — summaries, entity pages, concept pages, contradictions, cross-links, logs, evolving synthesis. *"No classical program could robustly maintain that kind of knowledge base across messy human documents. But an LLM can."*
- The reframe: *"Don't only ask, 'What existing workflow can AI speed up?' Also ask, 'What information transformation was impossible before, but is now natural?'"*

### Verifiability

- *"Traditional software automates what you can specify. LLMs and reinforcement learning automate what you can verify."*
- If a task has an automatic reward / success signal, models can practice it. That's why math, coding, tests, benchmarks, games, and many engineering tasks improve so quickly — they're **resettable, repeatable, and rewardable**.
- It's also why **coding agents feel dramatically better than ordinary chatbots**: coding gives the model feedback. Tests pass or fail, programs run or crash, diffs can be inspected, benchmarks can be measured.

### Jagged intelligence

- A refinement to verifiability. Capability isn't only about whether a task is verifiable — it also depends on whether **labs emphasized the task** during training, post-training, synthetic data, and RL.
- Rough formula: **`capability spike ~= verifiability × training attention × data coverage × economic value`**.
- Chess illustration: GPT-4's chess improvement may not have been smooth general-intelligence progress — a large amount of chess data was reportedly added to the pretraining mix.
- Models *"spike in some places and behave strangely in others."* The famous strawberry-letter-count bug has been patched; the new example is asking whether to drive or walk 50m to a car wash — state-of-the-art models may tell you to walk *because it's close*. *"How is it possible that a state-of-the-art model can refactor a 100,000-line codebase or find zero-day vulnerabilities, yet tells me to walk to the car wash? That's jaggedness."*
- Practical question: ***"Are you on the model's rails?"*** Inside the verifiable + trained region, the model flies; outside it, you may need better context, tools, fine-tuning, your own evals, or your own RL environment.

### Vibe coding vs. agentic engineering — canonical definition

- **Vibe coding raises the floor.** It lets almost anyone create software by describing what they want. Fine for prototypes and personal tools.
- **Agentic engineering raises the ceiling.** It is the **professional discipline of coordinating fallible agents while preserving correctness, security, taste, and maintainability.** What serious teams need.
- *"The agentic engineer does not blindly accept generated code. They design specs, supervise plans, inspect diffs, write tests, create evaluation loops, manage permissions, isolate worktrees, and preserve quality."*
- **MenuGen payment-bug worked example**: the agent tried to match Stripe purchases to Google accounts using email addresses. Plausible code, *bad system design* (Stripe email and Google login email can differ). Need a persistent user ID. *"A human needs enough product and engineering judgment to insist on persistent user IDs."*
- The frontier skill is **not** memorizing API details (`dim` vs `axis`, `reshape`, `permute`, `transpose`, `keepdim`). Agents have good recall for that. The human still needs the underlying concepts: storage, views, memory copies, invariants, identity, security boundaries, the shape of the system.

### Hiring should change

- Coding puzzles are *increasingly mismatched* with the actual skill.
- A better interview: **build a substantial project with agents, deploy it, make it secure, then have adversarial agents try to break it.** Tests: can the candidate decompose work for agents, write useful specs, preserve quality while moving fast, review generated work, secure and harden a system, use agents as leverage rather than produce slop?
- *"The old 10x engineer idea may become much more extreme. People who master agentic workflows may outperform others by far more than 10x."*

### Founder opportunity: valuable verifiable environments

- The most obvious verifiable domains (math, coding) are heavily targeted by frontier labs.
- But **many economically important domains may have latent verifiable structure that hasn't yet been exploited.** A founder can create a domain-specific environment where models try actions and receive reliable rewards, then fine-tune / RL on it.
- *"That is a startup wedge."*

### Agent-native infrastructure

- Most software is still built **for humans clicking through screens.** Docs say "go to this URL, click this button, open this settings panel."
- Increasingly the user is **the human's agent**, not the human directly. Products need agent-native surfaces:
  - Markdown docs
  - CLIs
  - APIs
  - MCP servers
  - Structured logs
  - Machine-readable schemas
  - Copy-pasteable agent instructions
  - Safe permissioning
  - Auditable actions
  - Headless setup flows
- The mental model: **sensors** turn world-state into digital information; **actuators** let agents change things. *"The future stack is agents using sensors and actuators on behalf of people and organizations."*
- The **MenuGen deployment story** is the benchmark: building the app was easy compared to wiring Vercel, auth, payments, DNS, secrets, production settings. *"In a mature agent-native world, I should be able to say 'build MenuGen' and have the agent deploy the whole thing without manual clicking."*
- *"My favorite pet peeve: why are people still telling me what to do? I don't want to do anything. What is the thing I should copy-paste to my agent?"*

### Ghosts, not animals

- LLMs are *not animals*. No biological drives, no embodied survival pressure, no curiosity, no play, no intrinsic motivation in the animal sense.
- They are **statistical simulations of human artifacts**, shaped by pretraining, post-training, RL, product feedback, and economic incentives.
- Anthropomorphic expectations mislead. *"These systems can be brilliant in one moment and bizarrely dumb in the next. They are not smooth human minds. They are jagged, alien tools."*
- The right posture: **neither dismissal nor blind trust — empirical familiarity.** Learn where they work, where they fail, what they were trained for, how to build guardrails around them.

### Education: outsource thinking, not understanding

- The quoted line he keeps returning to: *"You can outsource your thinking, but you can't outsource your understanding."*
- Even when agents do more of the work, the human still needs **understanding** to direct them — to know what's worth building, what question matters, what result is suspicious, what tradeoff is acceptable.
- LLM knowledge bases (wikis) are *"tools for transforming information into understanding"* — not just answer machines.
- His **microGPT** project — a full GPT training and inference implementation in a single dependency-free Python file — is an educational artifact small enough for both humans *and agents* to inspect. Karpathy notes: *"The models hate this. They can't do it. I kept trying to prompt an LLM to simplify more and more, and it just couldn't. You feel like you are outside the RL circuits."* (i.e., a tasteful-simplification task is *not* on the rails.)

### Big-picture summary

- The scarce thing is shifting:
  - **Less scarce**: code generation, API recall, boilerplate, first drafts, repetitive setup, simple transformations.
  - **More scarce**: understanding, taste, eval design, security, system boundaries, agent orchestration, domain-specific feedback loops, knowing when the model is off the rails.
- Karpathy's compact recipe for the new work:
  ```
  define the context
  define the tools
  define the feedback loop
  define the guardrails
  let agents work
  preserve human understanding
  ```

## Connections

- **Major new author — first source not by Willison.** Karpathy is the originator of "vibe coding" that Willison's [[2026-05-23-what-is-agentic-engineering]] cited secondhand. Here he provides the **canonical floor/ceiling framing** that supersedes our previous secondhand treatment. Updates [[coding-agents]] (the vibe-coding section) and prompts a comparison synthesis with Willison.
- **Software 3.0** is a wholly new paradigm-naming frame with no prior home in the wiki; gets its own page [[software-3-0]].
- **Verifiability and jagged intelligence** are bundled here as one analytic frame; together they get [[verifiability]].
- **Agent-native infrastructure** (sensors/actuators, MCP, agent-first docs) is new; gets [[agent-native-infrastructure]].
- **Ghosts-vs-animals** is a mental-model framing; folded into [[agent-architecture]] as a section.
- Karpathy's recipe (`define context / tools / feedback loop / guardrails / let agents work / preserve human understanding`) aligns directly with the architectural picture in [[2026-05-23-how-coding-agents-work]] and the practices in [[compound-engineering]] and [[agent-code-review]].
- Karpathy's MenuGen payment-bug example mirrors Willison's [[agent-code-review]] concern (agents produce plausible but bad-judgment code; humans own the spec).
- Karpathy's "10x engineer goes much further" claim is a stronger version of Willison's [[economics-of-code]] argument about the surplus.
- Karpathy's [LLM Wiki Pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) is **the literal inspiration for this wiki**. The pattern is referenced in `README.md` and the wiki is structured around it.
- Comparison page: [[willison-vs-karpathy]].
- Author: [[andrej-karpathy]].

## Raw file

`raw/Sequoia Ascent 2026 summary.md`
