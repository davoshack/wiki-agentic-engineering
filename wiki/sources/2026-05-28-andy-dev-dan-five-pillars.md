---
type: source
source_type: transcript
source_url: https://youtu.be/2KcITKKJikA
source_date: 2026-05
tags: [agentic-engineering, agent-harness, software-factory, tokeconomics, agentic-access, AFK-agents, custom-harness, ADWs]
created: 2026-05-28
updated: 2026-05-28
status: developing
---

# Top #1 Opportunity for Senior Engineers: Agentic Engineering

> **About this source.** Andy Dev Dan is the host of a YouTube channel and owner of *agenticengineer.com*; he sells courses (*Tactical Agent Coding*, *Agent Horizon*) and promotes specific third-party tools (the "PI agent harness" by Mario) throughout the talk. The video is explicitly framed as a "raw" note-to-self after a two-week break. The content is substantive and the five pillars below are a useful addition to the wiki — but several assertions are sales-shaped (*"top 500 companies all building software factories,"* *"90% of agent cron jobs dead useless,"* *"by end of 2026 agentic engineering will be the default"*) and should be read as claims-by-a-practitioner-influencer rather than reported facts. Calibrate accordingly.

A 26-minute monologue laying out **five pillars** Andy Dev Dan claims widen the gap between low- and high-performing agentic engineers: the **agent harness**, the **software factory**, **extensible software**, **always-on (AFK) agents**, and **agentic access**. The throughline is *"build the system that builds the system"*: stop sitting in the terminal vibe-coding features; own and customize the layer beneath the agent; treat tokens economically; and give agents API access to everything you reach yourself. The talk references [[andrej-karpathy|Karpathy's]] Sequoia Ascent comments as the moment "the industry follows," and positions Andy as someone who's been "betting on agentic engineering since Claude Code released in March 2025."

## Key takeaways

### Working definition

- Agentic engineering = *"the process of engineering with intelligence that can operate on your behalf."* Compared to the Willison and Karpathy definitions, Andy's frames the human as orchestrating *intelligence* (not just an agent loop), and centers the human's job as *building the substrate* the intelligence runs on.
- Recurring framing: **"vibe coding is the lowest hanging fruit"**; the ceiling is agentic engineering. Direct echo of [[andrej-karpathy|Karpathy's]] floor/ceiling framing (see [[coding-agents]] § vibe coding vs. agentic engineering).

### Pillar 1 — The Agent Harness

- *"Whoever controls the agent harness controls your results."*
- Claude Code, Codex, OpenCode are the **floor, not the ceiling**. Renting an out-of-the-box harness is "a great start, a terrible place to finish."
- Andy claims to build **"one new custom agent harness every single day"** using the third-party **PI agent harness** (built by "Mario"), which he describes as composable / pluggable / swappable.
- Worked example: **UIA J team** — a multi-agent orchestration setup with a 3-tier structure (orchestrator → team leads → workers) interacting in a chat-room-style interface. Triggered with prompts like *"ping your teams."* This is the smaller-scale, single-engineer analog of the Worker/Leader architecture in [[multi-agent-coordination]] from Kumar & Ramagopal.
- Another example: an **agent communication network** where multiple model-specific agents (e.g., "Opus 4.7 presentation agent" + "Gemini 3.5 flash helper agent") sit on a custom message bus that the main agent can talk to.
- What you can do once you own the harness: sandbox tools, sub-agent delegation, "damage control," model fallbacks, model routing, **specialization** (DevOps harness, testing harness, billing harness — *"specialization is the moat. One tool, many versions."*).

### Pillar 2 — The Software Factory ("dark factory" / ADWs / ZTE)

- *"Build factories, not features."* You're not the engineer who ships the feature; you're the engineer who builds the system that builds the feature.
- A **plan / spec prompt** is *"a prompt scaled"* — a more detailed prompt. But that's just the entry point; the factory also handles planning, plan review, scouting, validation, build, test, review.
- Andy uses the term **AI Developer Workflows (ADWs)** for the factory pattern in his *Tactical Agent Coding* course. Synonym he uses: **dark factory**.
- Aspirational endpoint: **ZTE — Zero Touch Engineering**, prompt → production with no manual intervention. Flagged as "super super advanced," not the current target.
- Claim he repeats: *"the top 500 companies, everyone is building a software factory; soon this will be a requirement."* (Unsourced — read with the caveat above.)
- Framed as **a new SWE skill** alongside backend / frontend / full-stack / DevOps.

### Pillar 3 — Extensible software

- *"Open to extension, closed to modification"* (the Open-Closed Principle) explicitly invoked, applied to the agent era.
- Why now: **models, prompts, tools, agents change constantly.** Brittle code with cascading `if` statements will hurt because *"your agents will be slow and make mistakes"* navigating it.
- Two scopes: **engineering work** (your harness — e.g. PI's swappability) and **production work** (whether you're shipping agentic products or traditional software).
- *"Pluggability is the key. Extensibility is the key. Composability is the key."*

### Pillar 4 — Always-On / AFK Agents, gated by a 3-level "tokeconomics" funnel

This is Andy's most distinctive analytical claim. He argues *"always on"* is a *consequence*, not a default — it's only correct once you've climbed a 3-level funnel:

1. **Token-maxing** (the floor) — just use more tokens. "Great place to start, terrible place to finish."
2. **Useful tokens** — generate measurable value. *"A lot of tokens getting generated, not a lot of value getting generated. This is the trick of engineering."*
3. **Token arbitrage / capture** — turn that value into actual revenue. Pay $1/token, generate $2 of value, capture the spread.

Only after Level 3 do you turn the system on 24/7 (AFK / always-on agents). At Level 3, **rising API bill becomes a new productivity KPI** — *"how many tokens can you spend?"* becomes the relevant question, the same way ad-spend scaling works once unit economics are positive.

He claims his own token usage is "actually quite low" — token growth is "a very very smooth curve" — because he keeps the focus on Level 3 rather than maxing at L1. Stated headline: *"90% of agent cron jobs running right now are dead useless and just burning cash."*

The framing is provocative and sharp. Caveats worth holding:
- The L1 → L2 → L3 model works cleanly for an AI lab (sells tokens at margin) or for a software business with a product / client revenue stream. It works less cleanly for a solo engineer using agents on internal work — what's the "captured revenue" of an agent that refactors your codebase faster? Probably translates to *"value to your employer or to your own time"* but Andy doesn't draw that line carefully.
- The "90% dead useless" number is unsourced.

### Pillar 5 — Agentic Access (sharp variant of agent-native infrastructure)

- *"Agents only command what they can programmatically reach."* This is Karpathy's [[agent-native-infrastructure|sensors-and-actuators]] thesis, re-stated as a prescription for the individual engineer's own stack.
- Tools to expose to agents: CLI tools, REST, webhooks, RPC clients, MCP servers.
- Limits: lock down `bash` so agents can't catastrophically nuke production / databases / volumes.
- New concept Andy adds: **the token tax** — *"anything your agent does that is unnecessary strictly because you haven't given it direct API access."* If your agent has to scrape a UI or read a screenshot because there's no API, that's a token tax. The mindset shift: pay the upfront cost of exposing access so your agents don't pay the recurring cost of working around its absence.
- Closes with: *"Agent first systems, agent first products, agent first workflows. Expose your CLIs and APIs everywhere. Code bases, products, devices, tools."*

### Closing meta-claim

- *"Models matter less and less. They matter for bleeding-edge work, but for 80–90% of the work we're doing on a daily basis, what matters is the systems you place around your agents."*
- This is a stronger version of Willison's "harness + tools in a loop" framing in [[agent-architecture]] — Andy elevates the *substrate* (harness, factory, access surface) above the *model* as the primary lever.
- The pillars are framed as "compounding advantages" the top 2% of engineers are accumulating week over week.

## Connections

- **Third practitioner voice.** First two: [[simon-willison]] (practices), [[andrej-karpathy]] (paradigms). Kumar & Ramagopal ([[kumar-ramagopal]]) speak from an enterprise / control-plane vantage. Andy speaks as a **single senior engineer at the leading edge** — the gap his pillars target is between high- and low-performing *individual* engineers, not between organizations.
- **Pillar 1 (harness)** extends [[agent-architecture]]'s "harness wraps the LLM" description into a *discipline of building your own*. Spun out as the new topic [[agent-harness-engineering]].
- **Pillar 2 (software factory)** parallels and intensifies [[compound-engineering]]: where compound-engineering accumulates *instructions* across runs, the software factory accumulates *whole pipelines* (planning + spec + build + test + review). The new topic is [[software-factory]]. ZTE is to the factory what agent-native deployment ([[agent-native-infrastructure]]) is to the world.
- **Pillar 3 (extensible software)** is a software-engineering principle ("open to extension, closed to modification") applied to a fast-changing AI substrate. No standalone page needed — folds into [[agent-harness-engineering]] (engineering scope) and gets a mention in [[agent-native-infrastructure]] (product scope).
- **Pillar 4 (AFK + tokeconomics)** is genuinely new analytic content. The 3-level funnel and "token tax" are the substance of [[tokeconomics]]. AFK / always-on is folded inside as the *output* of the funnel.
- **Pillar 5 (agentic access)** sharpens [[agent-native-infrastructure]] with the *token tax* lens — every missing API surface is paid in tokens over time.
- **Closing meta-claim ("models matter less")** is the strongest single-voice claim that the *substrate* > *model* in the wiki so far. Worth tracking against future sources that might push back.
- **Andy's 3-tier orchestrator → team-leads → workers** structure is conceptually a smaller-scale version of [[multi-agent-coordination]]'s Worker / Leader architecture (Kumar & Ramagopal at Cisco). Andy is doing it solo at a single-engineer scale; Kumar & Ramagopal are doing it at organization scale with LangGraph + LangSmith + LangMem as substrate.
- Andy explicitly references **[[andrej-karpathy|Karpathy's]] Sequoia Ascent talk** ([[2026-04-30-sequoia-ascent-karpathy]]) as the moment "the industry follows" — the source page should be read as positioned downstream of Karpathy's vocabulary lock-in.
- Author: [[andy-dev-dan]].

## Raw file

`raw/Top #1 Opportunity for Senior Engineers_ Agentic Engineering.pdf`
