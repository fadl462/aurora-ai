<div align="center">

# Aurora AI OS

**The Intelligent Operating System for Everything**

*An architecture and product blueprint for a unified AI platform — reasoning, research, creation, automation, and execution in one workspace.*

[![Status](https://img.shields.io/badge/status-planning-blue)]()
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Docs](https://img.shields.io/badge/docs-in%20progress-orange)](docs/)

[Vision](docs/01-vision-and-strategy.md) ·
[Product Requirements](docs/02-product-requirements.md) ·
[Architecture](docs/03-system-architecture.md) ·
[Modules](docs/04-modules-overview.md) ·
[Roadmap](docs/10-roadmap.md)

</div>

---

## What is Aurora AI OS?

Most AI products today are a single chat window bolted onto a single model. Aurora AI OS is designed differently: as an **operating system for intelligence**, where chat is one surface among many, a routing layer chooses the right model and tools for each task, and specialized engines (research, memory, automation, execution) work together instead of being crammed into one prompt box.

This repository is the **planning and design corpus** for that platform: the product rationale, the system architecture, the module specifications, and the build roadmap. It exists so that an engineering team can start building without re-litigating scope or guessing at intent.

> **Status:** This is a pre-build planning repository. No production code lives here yet — see [`10-roadmap.md`](docs/10-roadmap.md) for what "done" looks like at each phase.

## Why this exists

The original goal was to compete with general-purpose assistants (Claude, ChatGPT, Gemini, Copilot) by being broader. Breadth alone isn't a strategy — it's a scope problem waiting to happen. This blueprint keeps the ambition but adds the things a scope list doesn't give you on its own:

- A **phased build order** so v1 is shippable in weeks, not after 50 documents are finished.
- A **module boundary model** so "add a feature" doesn't mean "touch the whole codebase."
- A **differentiation thesis** — what Aurora does that a wrapper around GPT-4 or Claude doesn't.
- Enough **technical specificity** (schemas, API shapes, security posture) that the docs are buildable, not just aspirational.

## Repository structure

```
aurora-ai-os/
├── README.md                          — you are here
├── docs/
│   ├── 00-executive-summary.md        — one-page pitch
│   ├── 01-vision-and-strategy.md      — why this, why now, who it's for
│   ├── 02-product-requirements.md     — PRD: users, features, success metrics
│   ├── 03-system-architecture.md      — services, data flow, diagrams
│   ├── 04-modules-overview.md         — every platform module, scoped
│   ├── 05-database-design.md          — core schema, storage strategy
│   ├── 06-api-specification.md        — REST/streaming contract, examples
│   ├── 07-security-and-compliance.md  — authN/Z, encryption, certifications
│   ├── 08-ui-ux-design-system.md      — design tokens, layout, accessibility
│   ├── 09-tech-stack.md               — chosen stack and rationale
│   ├── 10-roadmap.md                  — six phases, deliverables, sequencing
│   ├── 11-differentiators.md          — what makes this not "another wrapper"
│   └── 12-glossary.md                 — shared vocabulary for contributors
├── CONTRIBUTING.md
└── LICENSE
```

## Quick orientation by role

| If you are a... | Start with |
|---|---|
| Founder / product lead | [Executive Summary](docs/00-executive-summary.md), [Vision](docs/01-vision-and-strategy.md) |
| Engineer joining the build | [System Architecture](docs/03-system-architecture.md), [Tech Stack](docs/09-tech-stack.md), [Roadmap](docs/10-roadmap.md) |
| Designer | [UI/UX Design System](docs/08-ui-ux-design-system.md), [Modules Overview](docs/04-modules-overview.md) |
| Investor / stakeholder | [Executive Summary](docs/00-executive-summary.md), [Differentiators](docs/11-differentiators.md), [Roadmap](docs/10-roadmap.md) |
| Security / compliance reviewer | [Security & Compliance](docs/07-security-and-compliance.md) |

## Core philosophy

Aurora is built around ten verbs, not one:

`Think · Plan · Research · Create · Build · Automate · Learn · Remember · Collaborate · Execute`

A traditional chatbot only really does the first one. Aurora's architecture treats the other nine as first-class services with their own APIs, not as prompt tricks layered on top of a single model call. See [System Architecture](docs/03-system-architecture.md) for how that's implemented.

## License

Documentation and diagrams in this repository are released under the [MIT License](LICENSE) unless otherwise noted. Product and code names ("Aurora," "Project Genesis") are placeholders pending trademark clearance.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to propose changes to these documents.
