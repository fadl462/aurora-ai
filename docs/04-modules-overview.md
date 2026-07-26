# Modules Overview

The original planning conversation produced two overlapping lists (a 33-item "platform structure" and a 10-module "master product" breakdown covering much of the same ground). This document consolidates both into one canonical module list, grouped by function, with each module scoped to a release phase from the [Roadmap](10-roadmap.md).

## How to read this table

- **Phase** — earliest roadmap phase the module ships in (see [10-roadmap.md](10-roadmap.md))
- **Type** — `Core` (part of the orchestration platform itself) vs `Plugin` (built on the platform, could be third-party)

## Foundation

| Module | Phase | Type | Scope |
|---|---|---|---|
| Authentication | 1 | Core | Email, OAuth (Google/Microsoft/GitHub/Apple), MFA, passkeys, session & device management |
| Home Dashboard | 1 | Core | Recent chats, pinned projects, quick actions, notifications — the productivity landing page instead of a blank chat box |
| Universal Chat | 1 | Core | Multi-modal input (text/image/document), conversation branching, citations, export |
| Multi-Model Gateway | 1 | Core | Model-agnostic routing (Claude, GPT, Gemini, Llama, open-source); manual or Auto Mode selection |
| Memory Engine | 1 | Core | User-visible, editable, deletable long-term memory: preferences, style, project context |

## Productivity

| Module | Phase | Type | Scope |
|---|---|---|---|
| Document Studio | 2 | Core | Read/write/edit/merge/split/convert/compare across PDF, Word, Excel, PowerPoint, CSV; OCR; version comparison |
| Research Engine | 2 | Core | Web, academic, patent, financial, and news search with citation generation, fact-checking, and confidence scoring |
| Knowledge Vault | 2 | Core | User-uploaded documents, videos, websites, and databases indexed for retrieval (RAG) |
| Coding Studio | 2 | Core | AI-assisted IDE: completion, bug fixing, refactoring, testing, git integration, sandboxed execution |
| Data Analytics | 2 | Plugin | Spreadsheet/SQL assistance, statistics, forecasting, dashboard generation |

## Agents & Automation

| Module | Phase | Type | Scope |
|---|---|---|---|
| Agent Framework | 3 | Core | Role-scoped agents with their own tools, memory scope, and system prompt (not simulated personas on a shared generic prompt) |
| Automation Engine | 3 | Core | Trigger → reason → tool-call → execute → report loop, with configurable human-approval gates |
| Execution Layer | 3 | Core | Governs AI-initiated actions against connected systems (see [Security & Compliance](07-security-and-compliance.md) for the approval-tier model) |
| Developer Platform / API | 3 | Core | REST + streaming API, SDKs, webhooks — the surface third-party integrations and plugins build on |

## Media & Creative

| Module | Phase | Type | Scope |
|---|---|---|---|
| Image Studio | 5 | Plugin | Generate/edit/upscale, background removal, logo and UI asset generation |
| Video Studio | 5 | Plugin | Generation, editing, subtitles, avatars, dubbing |
| Audio Studio | 5 | Plugin | Transcription, voice synthesis, meeting summaries, noise removal |
| Website & App Builder | 4 | Plugin | No-code site/app generation from natural-language specs |

## Collaboration & Workspace

| Module | Phase | Type | Scope |
|---|---|---|---|
| AI Canvas | 5 | Core | Unified surface combining chat, documents, whiteboards, diagrams, code, and live dashboards |
| Real-Time Collaboration | 5 | Core | Multi-user editing, presence, comment threads, task assignment, change approval |
| Team Workspaces | 4 | Core | Departments, shared projects, shared knowledge, role management |
| Personal AI Assistant | 5 | Plugin | Proactive daily planning, inbox summarization, meeting prep, surfaced next actions |

## Platform & Ecosystem

| Module | Phase | Type | Scope |
|---|---|---|---|
| Plugin System | 5 | Core | Third-party apps, extensions, widgets, and custom AI tools via public SDK |
| Agent & Plugin Marketplace | 5 | Core | Publish, discover, install, rate, and (later) sell agents and plugins |
| API Platform | 3 | Core | REST, GraphQL, streaming, OAuth, SDKs for major languages |
| Observability | 3 | Core | Usage, latency, cost, and quality-score tracking per feature and per tenant |

## Enterprise & Governance

| Module | Phase | Type | Scope |
|---|---|---|---|
| Enterprise Platform | 4 | Core | SSO, Active Directory, RBAC, audit logs, data residency, private/on-prem deployment |
| Security Center | 4 | Core | Zero Trust posture, MFA, device management, threat detection, session management |
| Admin Panel | 4 | Core | User & org management, billing, moderation, feature flags |
| Billing | 4 | Core | Free/Pro/Business/Enterprise tiers, usage-based API billing, marketplace revenue share |
| Compliance | 4 | Core | SOC 2, ISO 27001, GDPR, HIPAA readiness (see [Security & Compliance](07-security-and-compliance.md)) |

## What changed from the original brainstorm

- **Deduplicated** the "Platform Architecture" list and the "Master Product" module breakdown — they described the same ~20 capabilities twice with different names (e.g., "Research Engine" and "AI Research Engine" were the same module).
- **Removed premature specificity** that reads as filler rather than requirements — e.g., listing "ISO27001, SOC2, GDPR, HIPAA" as bullet points without a plan is a compliance *aspiration*, not a module. That detail now lives in [Security & Compliance](07-security-and-compliance.md) with an actual sequencing.
- **Reclassified roughly a third of the original list as Plugins**, not Core. Video/audio generation, the app builder, and the personal assistant don't need to be part of the orchestration core to exist — building them as plugins against the Phase 3 API keeps the core small and testable.
- **Cut "AI Thinking Modes" and "AI Agents" as separate top-level modules** (Quick/Deep/Research/Legal/Medical/... modes, and a long list of named agent personas). These are not modules — they're *configurations* of the Agent Framework and Model Router. Encoding "Legal Mode" as a hard-coded platform feature doesn't scale; encoding it as an agent definition (system prompt + tool scope + model preference) that anyone can create does.
