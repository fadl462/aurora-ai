# Vision & Strategy

## Vision statement

> Build an AI operating system that combines reasoning, research, creativity, automation, execution, and collaboration into a single platform — one that serves individuals, teams, and enterprises without forcing them to stitch together separate tools for each capability.

## Why "operating system," not "chatbot"

A chatbot is a single surface: you type, it replies. An operating system is a set of services (a kernel, drivers, a file system, a UI shell) that applications are built on top of. Aurora borrows that shape:

| OS concept | Aurora equivalent |
|---|---|
| Kernel | Orchestration Engine — decides which model/tool/agent handles a request |
| Drivers | Model adapters (Claude, GPT, Gemini, Llama, open-source) behind one interface |
| File system | Knowledge Vault + Vector Store — durable, searchable state |
| Processes | Agents and automations — long-running, resumable units of work |
| Shell | Universal Chat + Canvas — the surfaces users actually touch |
| Permissions | RBAC, approval tiers, audit log |

This framing matters because it forces a design discipline: new capabilities are **services with contracts**, not new conditionals inside a single chat handler.

## Target users

1. **Individual power users** — researchers, writers, consultants, developers who currently juggle 3–5 separate AI tools.
2. **Small teams** — need shared workspaces, shared knowledge, and light automation without enterprise procurement overhead.
3. **Enterprises** — need SSO, audit logs, data residency, and the ability to deploy privately or on-premise; will not adopt without governance features present from the start.
4. **Developers / platform partners** — build and sell agents, plugins, and integrations on top of Aurora rather than starting from scratch.

## Strategic principles

These principles govern every architecture and roadmap decision in this repository:

- **Design modularly.** Each capability (chat, research, agents, memory, automation, coding, media generation) is an independent service with a defined API. A module can be rebuilt or replaced without touching the others.
- **Orchestrate, don't hard-code.** Feature logic doesn't live inside the chat handler. An orchestration engine decides which model, tool, or agent handles a given task, and that decision is inspectable.
- **Plugin-first.** New capabilities should be installable, not require a core platform release. This is what makes the 30-module wishlist in the original brainstorm tractable — most of those modules become plugins built on a stable core, not core features themselves.
- **Memory is the user's, not the platform's.** Users see what's remembered, and can edit, export, or delete it. This isn't just an ethical stance — it's what makes enterprise adoption possible under GDPR/HIPAA-type regimes.
- **Security is a Phase 1–3 concern, not a Phase 6 one.** Retrofitting RBAC and audit logging into a live system is materially harder than building on top of them. See [Roadmap](10-roadmap.md) for the sequencing change this drove versus the original plan.
- **Measure continuously.** Latency, cost per request, hallucination/quality scores, and task success rate are tracked from the first internal release, not added post-launch.

## What we are explicitly *not* building first

To keep the roadmap honest, some capabilities from the original brainstorm are intentionally deferred and are not part of the v1–v2 critical path:

- Video generation and voice cloning (Phase 5, media studios) — high infrastructure cost, not core to the orchestration thesis.
- Full marketplace monetization (agent sales, revenue share) — needs a working agent framework and real usage data first.
- On-premise / offline enterprise deployment — needs a stable service boundary to package; premature before Phase 3.

## Success looks like

- A user can complete a multi-step task (e.g., "research competitor pricing, build a comparison table, draft a summary email") in one workspace, without exporting/re-uploading between tools.
- An enterprise buyer can pass a security review using the Phase 3 feature set alone.
- A third-party developer can ship a working plugin against the public API without platform-team involvement.

See [Product Requirements](02-product-requirements.md) for how these translate into concrete features and metrics.
