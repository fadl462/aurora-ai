# Contributing

This repository is currently a **planning and design corpus** — the docs in `docs/` are the source of truth for scope and architecture until code exists.

## Proposing a change to a doc

1. Open an issue or PR describing the change and which document(s) it affects.
2. If the change affects scope (adding/removing a module or shifting a roadmap phase), update **both** [`docs/04-modules-overview.md`](docs/04-modules-overview.md) and [`docs/10-roadmap.md`](docs/10-roadmap.md) — they're designed to stay in sync (each module lists its target phase).
3. If the change affects the data model, update the ER diagram in [`docs/05-database-design.md`](docs/05-database-design.md) alongside any API changes in [`docs/06-api-specification.md`](docs/06-api-specification.md).
4. Keep cross-references (the `[text](file.md#anchor)` links between docs) accurate — a lot of this repo's value is that the docs point at each other instead of duplicating content.

## Style

- Prefer tables over prose lists for anything enumerable (features, phases, endpoints) — it's what makes these docs skimmable.
- Every new module or feature should note which roadmap phase it targets.
- Avoid restating content that already lives in another doc; link to it instead.

## Once code exists

This CONTRIBUTING guide will be extended with branch strategy, testing requirements, and PR review process once Phase 3 ([Roadmap](docs/10-roadmap.md)) begins and there's a codebase to contribute to.
