# Executive Summary

## The one-paragraph pitch

Aurora AI OS is a unified AI workspace that replaces the "one chat window, one model" pattern with an operating system for intelligence: a routing layer that selects the right model and tools per task, specialized engines for research/memory/automation/execution, a multi-surface canvas beyond chat, and an agent and plugin ecosystem that lets the platform grow without a rewrite. It targets individuals, teams, and enterprises who have outgrown a single chatbot but don't want to stitch together six separate AI tools.

## The problem

- General-purpose assistants are excellent at conversation but weak at **sustained, multi-step work**: research that spans dozens of sources, automations that run unattended, documents that need real editing rather than regeneration.
- Power users already stitch together a chat tool, a research tool, an automation tool (Zapier/Make), and a document tool. Each hand-off loses context.
- Enterprises need governance (SSO, audit logs, data residency) that consumer chat products don't prioritize, and internal AI tools are usually single-purpose and hard to extend.

## The bet

A platform that owns the **orchestration layer** — deciding which model, tool, or agent handles a task — is more durable than a platform that owns one great model. Model quality will commoditize; workflow ownership, memory, and integration depth compound over time.

## What ships first (v1, not v50)

Contrary to a "build everything" plan, Phase 1 is intentionally narrow: universal chat with multi-model routing, file upload and basic memory, and authentication. Every later capability (research engine, agents, automation, canvas) is additive and independently shippable. See [Roadmap](10-roadmap.md).

## What makes it different

1. **Orchestration-first, not chat-first** — the chat window is a client of the orchestration engine, not the product itself.
2. **User-controlled memory** — visible, editable, deletable, not an opaque background process.
3. **Modular by construction** — every capability is a service behind an API; the plugin system is not bolted on later.
4. **Enterprise-credible from day one** — RBAC, audit logging, and data residency are Phase 3 concerns, not Phase 6 afterthoughts (moved earlier than the original roadmap draft — see [Roadmap](10-roadmap.md) rationale).

## What could go wrong

- **Scope creep.** The original brainstorm behind this repo listed ~30 modules and 50 planning documents. Without discipline this becomes a platform that's always "almost done." The roadmap enforces a shippable-slice discipline for exactly this reason.
- **Model-provider dependency.** Multi-model support mitigates but doesn't eliminate exposure to upstream pricing, rate limits, and policy changes from Anthropic, OpenAI, Google, etc.
- **Trust and safety at agent scale.** Letting agents execute actions (send email, modify databases, deploy code) multiplies the blast radius of a bad output. See [Security & Compliance](07-security-and-compliance.md) for the approval-tier model this repo proposes.

## Where to go next

- Full rationale: [Vision & Strategy](01-vision-and-strategy.md)
- What gets built and why: [Product Requirements](02-product-requirements.md)
- How it's built: [System Architecture](03-system-architecture.md)
