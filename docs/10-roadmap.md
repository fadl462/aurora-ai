# Roadmap

## Change from the original plan

The original brainstorm proposed ~50 planning documents and 6 phases totaling roughly a year before anything resembling a usable product exists, with security and compliance placed in the final phase. This roadmap keeps the six-phase shape but makes two changes:

1. **Security and governance foundations move to Phase 3**, not Phase 6 — see the rationale in [Security & Compliance §1](07-security-and-compliance.md#1-why-this-doc-exists-earlier-than-the-original-plan-had-it).
2. **Every phase ends with something a real user can use**, not just documents. Documentation and code are sequenced together per phase rather than "50 documents, then build."

## Phase 1 — Foundation (Weeks 1–4)

**Goal:** a working product decision, not yet a working product.

- Executive vision & strategy (this repo: [00](00-executive-summary.md), [01](01-vision-and-strategy.md))
- Product requirements ([02](02-product-requirements.md))
- Market and competitive analysis
- User personas and feature matrix ([02](02-product-requirements.md))
- Success metrics defined

**Exit criteria:** PRD approved; architecture doc drafted; no code required yet.

## Phase 2 — Experience & Technical Design (Weeks 5–12)

**Goal:** a buildable spec.

- Information architecture, user flows, wireframes
- UI Design System ([08](08-ui-ux-design-system.md)) and component library
- System architecture ([03](03-system-architecture.md)), database design ([05](05-database-design.md)), API spec ([06](06-api-specification.md))
- Interactive prototype for Universal Chat

**Exit criteria:** an engineer could start Phase 3 without asking "but how does X work?"

## Phase 3 — Core Platform (Weeks 13–28)

**Goal:** v1 (Chat Foundation) and v2 (Productivity Suite) ship to real users. Security foundations are built *with* the platform, not after it.

- Authentication, Home Dashboard, Universal Chat, Multi-Model Gateway, Memory Engine
- Document Studio, Research Engine, Knowledge Vault, Coding Studio
- **Security & governance foundations:** RBAC, audit logging, encryption at rest/in transit — moved earlier than the original plan (see [Security & Compliance](07-security-and-compliance.md))
- Public API v1 ([06](06-api-specification.md))
- Observability stack live from first production deploy, not added later

**Exit criteria:** a user can complete a real multi-step task (research → draft → export) end to end.

## Phase 4 — Agents, Automation & Enterprise (Weeks 29–44)

**Goal:** v3 and v4 — the platform becomes programmable, and enterprise-ready.

- Agent Framework, Automation Engine, Execution Layer (with the approval-tier model from [Security & Compliance §3](07-security-and-compliance.md))
- Team Workspaces, Enterprise Platform (SSO, RBAC at org scale), Admin Panel, Billing
- SOC 2 Type I and GDPR readiness pursued in parallel (see [compliance roadmap](07-security-and-compliance.md#6-compliance-roadmap))

**Exit criteria:** an enterprise buyer can complete a security review using what's shipped.

## Phase 5 — Ecosystem & Advanced Capabilities (Weeks 45–60)

**Goal:** v5 — the platform others build on.

- Plugin System, Agent & Plugin Marketplace
- AI Canvas, Real-Time Collaboration
- Media studios (Image, Video, Audio) — built as plugins against the Phase 3 API, not core platform work
- Personal AI Assistant, Website/App Builder

**Exit criteria:** a third-party developer ships a working plugin without platform-team involvement.

## Phase 6 — Scale & Certification (Weeks 61+)

**Goal:** the operational maturity that only comes from sustained production usage.

- SOC 2 Type II, ISO 27001, HIPAA readiness if vertical demand justifies it
- On-premise / private cloud deployment packaging
- Performance optimization based on real production telemetry (not speculative tuning)
- Public launch and go-to-market

## Phase-to-module map

For the full module list and which phase each ships in, see [Modules Overview](04-modules-overview.md) — every module in that document carries its target phase so this roadmap and the module inventory can't drift out of sync.

## Sequencing risks to watch

- **Phase 3 is the largest phase** (four core engines plus security foundations). If it slips, consider shipping Document Studio and Research Engine as a 3a/3b split rather than compressing security work to compensate — security is the one category that should not be the thing that flexes.
- **Phase 5's plugin ecosystem depends on Phase 3's API being stable.** Publishing the API too early (before Phase 3 exit criteria) risks a breaking v2 API change right as third-party developers are onboarding.
