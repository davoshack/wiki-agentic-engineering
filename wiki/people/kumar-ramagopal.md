---
type: person
tags: [agentic-engineering, author, enterprise, cisco, langchain, multi-agent]
created: 2026-05-26
updated: 2026-05-26
status: developing
sources: 1
---

# Renuka Kumar & Prashanth Ramagopal

Joint authors of the wiki's first **enterprise / team-scale** source on agentic
engineering. Combined page because they co-wrote a single piece together; will split
into individual pages if separate work from either appears later.

- **Renuka Kumar, Ph.D** — Principal Software Engineer (Director) at Cisco.
- **Prashanth Ramagopal** — Senior Director of Engineering at Cisco.

## Synthesis

Kumar and Ramagopal published *"Agentic Engineering: How Swarms of AI Agents Are
Redefining Software Engineering"* as a guest post on the LangChain blog on
2026-04-17 ([[2026-05-26-agentic-engineering-swarms]]). The piece is the first source
in the wiki that uses *"agentic engineering"* in a sense substantively different from
the [[agentic-engineering|practitioner discipline]] of Willison and Karpathy: for them,
agentic engineering is a **multi-agent coordination model / control plane** with
Worker Agents and a Leader Agent that orchestrates cross-team workflows. The
[[multi-agent-coordination]] topic page is the home for that architecture; the
[[practitioner-discipline-vs-control-plane]] synthesis page handles the comparison.

A few features of their perspective worth holding alongside their pages here:

- **Enterprise practitioner vantage.** Cisco-internal pilot, real production
  constraints (state, checkpointing, audit trails, deterministic execution,
  interoperability), real cross-team scope. This is a meaningfully different position
  from [[simon-willison|Willison's]] solo-developer-shipping-tools angle or
  [[andrej-karpathy|Karpathy's]] AI-lab / startup-investor angle. The wiki's prior
  lint passes and [[willison-vs-karpathy]] synthesis explicitly flagged the absence of
  this vantage — this source fills that gap.
- **Numbers-first.** The post leads with quant claims (93% debug time reduction; 65%
  dev workflow time reduction; 200+ hours saved across 512 sessions / 70 users / one
  month) drawn from a controlled pilot with QE-assessed quality. Numbers should be
  read with caveats (single enterprise, internal-baseline methodology, no external
  replication yet) but they are the most concrete delivery-cycle numbers in the wiki.
- **Composition, not competition.** They frame their system explicitly as composing
  *with* AI coding agents rather than replacing them: *"Codex-class models are often
  embedded within Worker Agents or as a component in the workflow as reasoning or
  code-generation engines."* This repositioning matters for how the Willison/Karpathy
  literature should be read inside an enterprise context.
- **Where they think the gain actually is.** Not faster code generation — that, they
  say, is already handled by AI coding agents — but **compressing the work *around*
  the code**: cross-team coordination, context handoff, validation, downstream testing
  after PR merge. *"PR review process itself became the bottleneck introduced by
  human-in-the-loop"* is the headline observation.
- **LangChain bias.** The post is a LangChain guest post; the framework selection
  (LangGraph + LangSmith + LangMem) reflects an evaluation done in that context. Worth
  reading the architectural claims as partly framework-agnostic and partly LangChain
  ecosystem advocacy.

## Open questions

- What's the open-source or non-Cisco equivalent of the pilot? External replication of
  the numerical claims would strengthen the case considerably.
- Where do Kumar and Ramagopal stand on the Willison/Karpathy questions the wiki
  cares about — vibe coding vs. agentic engineering as defined there, the 9-point
  "good code" checklist, evaluation methodology, security boundaries on tool use? The
  post focuses on architecture and outcomes and doesn't engage these directly.
- Is the architecture they describe sensitive to LangChain specifically, or would it
  port cleanly to other agent frameworks? The five production requirements they list
  read as framework-agnostic; the implementation does not.
- Does either of them publish independently of the other in this space?

## Sources

- [[2026-05-26-agentic-engineering-swarms]]
