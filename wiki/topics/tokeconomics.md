---
type: topic
tags: [agentic-engineering, economics, tokeconomics, token-tax, token-arbitrage, AFK-agents, always-on]
created: 2026-05-28
updated: 2026-05-28
status: developing
sources: 1
---

# Tokeconomics

[[andy-dev-dan]]'s framing of how to think about token-spend economically across three levels — and his claim that **AFK / always-on agents** are only a correct deployment at the top level. Distinct from the [[economics-of-code|engineering-time + token-cost layers]] already in the wiki: those describe *cost*; tokeconomics describes *return* and gates an activation decision on it.

## Synthesis

[[2026-05-28-andy-dev-dan-five-pillars]] introduces a three-level funnel for thinking about token-spend:

| Level | What you're doing | Andy's framing |
| --- | --- | --- |
| **L1** | **Token-maxing** — use more tokens | *"Great place to start, terrible place to finish."* |
| **L2** | **Useful tokens** — generate measurable value | *"A lot of tokens getting generated, not a lot of value getting generated. This is the trick of engineering."* |
| **L3** | **Token arbitrage** — turn value into captured revenue | *"You pay $1 for a token, generate $2 of value, capture the difference."* |

The core claim is sequential: **you only correctly turn agents always-on (AFK) after L3.** Before that, an always-running agent is just burning cash on the wrong work. Andy's blunt summary: ***"There are a million agent cron jobs running. 90% of them are dead useless and just burning tokens."*** (Number unsourced — see [[andy-dev-dan]] § course-business framing — but the *direction* of the claim is hard to dispute.)

### The token tax — L1's recurring drag

The negative-direction concept Andy introduces alongside the funnel: ***the token tax.*** Definition: *"anything your agent does that is unnecessary strictly because you haven't given it direct API access."* If your agent has to scrape a web UI, parse a screenshot, or simulate clicks because there's no API — that's a recurring cost paid in tokens. Every missing surface is a tax compounded over every invocation.

This sharpens [[agent-native-infrastructure|Karpathy's sensors-and-actuators thesis]]: where Karpathy frames it as a *capability* gap (the agent can't reach what isn't exposed), Andy frames it as an *economic* gap (the agent reaches it inefficiently, and that inefficiency compounds in your token bill). The two views are complementary — exposing more surfaces both *enables* the agent and *cheapens* its operations.

### Token arbitrage — L3's prerequisite for scaling

At L3, **rising API bill becomes a productivity KPI.** Andy frames the economics the same way as ad-spend scaling: once your unit economics work (token-spend → captured-revenue), scaling becomes a business problem rather than a technical one. *"How many tokens can you spend?"* is the question; the limit is the supply of valuable work, not the budget.

This is most natural for:
- **AI labs** — selling tokens at a margin is the entire business.
- **Software businesses with product revenue** — agents producing customer-facing features generate revenue per feature shipped.
- **Service businesses with client engagements** — agents producing client deliverables earn billable value.

It's less obviously natural for:
- **Solo engineers on internal work.** What's the captured revenue of an agent that refactors your codebase faster? Plausibly *"value to your employer or to your own time"* — but Andy doesn't draw that translation carefully. Salary-as-revenue makes the funnel a *productivity* argument rather than a literal *arbitrage* one.
- **Research / exploration.** Some token-spend is generative ([[hoarding-working-examples|hoardable artifacts]], exploratory prototypes per [[economics-of-code]]) whose value is realized later, sometimes much later. The funnel doesn't model the time-shifted-value case.

The L3 framing is sharp and useful as a *forcing function*: *don't turn this on 24/7 until you can show it pays.* It's less useful as a *complete* economic model.

### AFK / always-on agents — the L3 deployment

**AFK** = "away from keyboard." An AFK or always-on agent is one running 24/7 in the background — cron jobs, daemons, scheduled agents, persistent listeners. Andy's stance: **AFK is the consequence of getting tokeconomics right, not a default deployment mode.** Once Level 3 holds, *of course* you turn it always-on; before that, you're just paying L1 token-tax around the clock.

The framing is distinct from the **asynchronous coding agent** category that lives in [[coding-agents|coding-agents § sync vs. async]] (Gemini Jules, Codex web, Claude Code on the web). Those are fire-once-and-walk-away patterns inside a human-initiated session — async, but not *always-on*. AFK is the truly-always-on case, and Andy's claim is that it should be reached *only* once the work it does has a positive token-arbitrage.

### Relationship to the rest of the wiki

- **[[economics-of-code]]** describes the *cost* side of the agent economy — engineering time and tokens. Tokeconomics is the *return* side: what those tokens *yield*, and the activation condition for scaling them. The two stack: cheap tokens (economics-of-code) only translate into ROI if you climb the funnel (this page).
- **[[agent-native-infrastructure]]** describes *what world-shape* you need for agents to act efficiently. The **token tax** is the economic case for that infrastructure work — pay the upfront cost of exposing surfaces, save the recurring tokens.
- **[[verifiability]]** (Karpathy) describes *where* AI works best — the verifiable, heavily-trained circuits. Tokeconomics inherits that: L2 ("useful tokens") is much easier to achieve when you're on the model's rails. Verifiable domains are also the natural home of L3 (you can *measure* the value being generated, which makes arbitrage tractable).
- **[[software-factory]]** is what L2 / L3 look like in practice: a factory whose output produces measurable value per prompt is, by definition, generating useful tokens. The factory frame and the funnel frame answer different questions about the same work.
- **[[multi-agent-coordination]]'s** Cisco pilot numbers (93% debug-time reduction, 65% dev-time reduction, 200+ hours saved across 512 sessions) are the closest thing the wiki has to an empirically-grounded L2 / L3 claim. Worth holding next to Andy's unsourced "90% dead useless" number.

## Open questions

- For solo internal work without external revenue, what does "captured revenue" translate to? Andy doesn't carry the funnel into that case cleanly. Possibilities: salary-implied hourly rate × time saved; engineering velocity translated into shipped features; option value of side-projects.
- How do you *measure* L2 in practice? "Useful tokens" is intuitive but operationally vague. Token-per-test-passed? Token-per-line-of-shipped-code? Token-per-bug-fixed? The unit choice matters and Andy doesn't pick one.
- The token tax framing implies an *upfront* investment that pays back. What's the right rule of thumb for amortization — how many agent invocations does it take to recoup the cost of exposing a new API?
- The L1→L2→L3 funnel is presented as strictly sequential. Are there cases where L1 ("just burn tokens to explore") is *correct* in itself — e.g., during research, prototyping, or [[hoarding-working-examples|hoard-building]]?
- For research / exploration / long-tail value: the funnel undervalues token-spend whose return is time-delayed. What's the right way to think about that?

## Sources

- [[2026-05-28-andy-dev-dan-five-pillars]]
