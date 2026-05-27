---
type: topic
tags: [agentic-engineering, agent-native, sensors, actuators, mcp, infrastructure, founder-opportunity]
created: 2026-05-25
updated: 2026-05-26
status: developing
sources: 2
---

# Agent-native infrastructure

[[andrej-karpathy]]'s framing of what software should look like when the primary user is *an agent acting for a human* rather than the human directly. The compact form: most software today is built around humans clicking screens; the world has to be rewritten with **sensors** (turn world-state into digital information) and **actuators** (let agents change things), exposed through agent-first surfaces (markdown docs, CLIs, APIs, MCP servers, structured logs, copy-pasteable instructions).

## Synthesis

### The user is increasingly the agent

In [[2026-04-30-sequoia-ascent-karpathy]], Karpathy presses a frustration into a thesis: docs still tell humans to *"go to this URL, click this button, open this settings panel."* But increasingly the user is **the human's agent**, not the human directly. The right product surface for agents differs from the right product surface for humans.

His favorite pet peeve: *"Why are people still telling me what to do? I don't want to do anything. What is the thing I should copy-paste to my agent?"* The implicit product spec is **agent-first documentation** — instructions an agent can act on without a human reading and translating.

### The agent-native surface inventory

Karpathy's enumeration of what a product needs to expose to be agent-native:

| Surface | What it does |
| --- | --- |
| Markdown docs | Agent-readable instructions, not human-tutorial prose. |
| CLIs | Scriptable command surfaces over functionality. |
| APIs | Programmatic access. |
| MCP servers | Standardized agent ↔ system protocol. |
| Structured logs | Machine-readable history. |
| Machine-readable schemas | Data the agent can navigate without scraping. |
| Copy-pasteable agent instructions | Skills the user can drop into a session. |
| Safe permissioning | Bounded authority for agent actions. |
| Auditable actions | Reviewable trails of what the agent did. |
| Headless setup flows | Deployment without manual clicking. |

The unifying property: **everything an agent needs is reachable without a human in the loop.**

### Sensors and actuators

Karpathy's higher-level mental model: the agent-native stack reduces to **sensors** and **actuators**.

- **Sensors** turn some state of the world into digital information the agent can consume: file contents, structured logs, screenshots, telemetry, search indexes, CLI output.
- **Actuators** let an agent change something: API calls, CLI commands, MCP tool invocations, generated code, deployed services, sent messages.

The future stack — in his framing — is **agents using sensors and actuators on behalf of people and organizations**, with the human providing direction and oversight. *"My agent will talk to your agent to figure out meeting details and other tasks."*

This maps directly onto the architectural picture in [[agent-architecture]]: tools are exactly the harness's set of sensors and actuators. The agent-native infrastructure thesis is the **product-level** version of that observation — services should expose richer, safer sensors and actuators to the agents that will be calling them.

### The MenuGen deployment benchmark

Karpathy's running benchmark for how mature the world is: the MenuGen deployment story. Building the app was easy; **wiring Vercel, auth, payments, DNS, secrets, and production settings was hard**, and almost entirely manual clicking. *"In a mature agent-native world, I should be able to say 'build MenuGen' and have the agent deploy the whole thing without manual clicking."*

This is a meaningful gap. The Software 3.0 layer ([[software-3-0]]) is increasingly capable; the deployment / configuration layer remains stubbornly Software 1.0 with UI surfaces designed for humans.

### Founder opportunity

The flip side of the thesis is a wedge. Founders building **net-new** infrastructure can default to agent-native — markdown docs, MCP server, CLI, structured logs, copy-paste skills — and skip the human-UI-first design that competitors would have to rebuild. Founders building **adapter layers** can wrap existing human-first products in agent-native surfaces. Both are real opportunities; the agent-native gap exists across most of the stack.

### Connection to the rest of the wiki

- The **sensors-and-actuators** framing is the product-level analog of the **tools-in-a-loop** definition of an agent in [[coding-agents]] and the harness picture in [[agent-architecture]].
- **MCP servers** specifically appear in [[subagents]] (vendor docs link out to MCP-based integrations) and in Karpathy's list here. MCP is becoming the standardized substrate for actuators.
- **Headless setup flows** connect to [[refactoring-with-agents]] — the async-agent worktree workflow only works when the surrounding deployment toolchain doesn't require a human in the UI.
- **Copy-pasteable agent instructions** are the public-facing form of the same artifact that [[hoarding-working-examples]] is about — Software 3.0 skills shipped as text blocks (the OpenClaw installer example in [[software-3-0]]).
- **Agent-onboarding `--help` text and exec-capturing artifact tools** are a worked instance of the thesis at the developer-tools layer. [[2026-05-26-agentic-manual-testing]] describes [Rodney](https://github.com/simonw/rodney) (whose `--help` is written so the agent learns both *what the tool is* and *how to use it* from a single CLI invocation, after `uvx`-installing itself on first call) and [Showboat](https://github.com/simonw/showboat) (whose `exec` command mechanically captures real command output to discourage agents from writing what they *hoped* had happened). Both treat the agent-as-user as a first-class design constraint. See [[agentic-testing]].
- **Auditable actions** and **safe permissioning** are the infrastructure-level expression of [[agent-code-review]]'s concern: the human owns responsibility for what the agent did.

## Open questions

- What does "agent-native" *look like* at the application layer (not just infra)? Is there an inventory of common UI patterns that should be paired with agent-readable equivalents?
- How does **MCP** fare as the de-facto agent-native protocol? Karpathy lists it alongside CLIs and APIs but doesn't predict winners.
- What does *safe* permissioning actually look like for high-stakes actuators (production deploys, financial transactions, customer-facing changes)? Karpathy mentions safety as a category but doesn't characterize designs.
- For agent-to-agent traffic ("my agent talks to your agent"), what are the standards? Today this is mostly imagined; what's the realistic 12-month evolution?
- Auditable-actions trails: is there a useful generic schema, or is this necessarily per-domain?

## Sources

- [[2026-04-30-sequoia-ascent-karpathy]]
- [[2026-05-26-agentic-manual-testing]]
