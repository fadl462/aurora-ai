# Technology Stack

## Frontend

| Layer | Choice | Why |
|---|---|---|
| Framework | React + Next.js | Server-rendering for fast first load on the dashboard; large ecosystem for the component library |
| Language | TypeScript | Type safety across a large, multi-surface frontend (chat, canvas, admin panel) |
| Styling | Tailwind CSS | Matches the token-based design system in [UI/UX Design System](08-ui-ux-design-system.md) |
| Data fetching | React Query | Handles the async/streaming nature of chat and job-based endpoints (research, automation) cleanly |
| Real-time | WebSockets | Canvas collaboration, live automation status, streamed chat |
| Mobile | React Native | Code-sharing with the web component library rather than three separate native codebases at this stage |

## Backend

| Layer | Choice | Why |
|---|---|---|
| Primary API framework | FastAPI (Python) | Async-native, strong typing via Pydantic, and Python is the natural fit for the AI/orchestration layer |
| Auxiliary services | NestJS (Node.js) | Used selectively where the team already has Node expertise or for I/O-bound services (e.g., webhook fan-out) — not a second framework for its own sake |
| Internal service communication | gRPC | Low-latency, strongly-typed contracts between the Orchestration Engine and capability engines |
| Job queue | Redis + a task queue (e.g., Celery or RQ) | Backs the Automation Engine's trigger → execute → report loop |

## Data

| Layer | Choice | Why |
|---|---|---|
| Primary database | PostgreSQL | Relational integrity for users, permissions, billing — see [Database Design](05-database-design.md) |
| Cache / queue / session store | Redis | Sub-millisecond reads for session and rate-limit state |
| Object storage | S3-compatible (AWS S3 or equivalent) | Uploaded files, generated documents, exports |
| Vector store | pgvector (initially) → dedicated vector DB if scale demands it | Start co-located with Postgres to avoid a second data store until query volume justifies the operational cost |

## AI layer

- **Model gateway:** a thin abstraction (`complete()` / `stream()` / `embed()`) over Anthropic, OpenAI, Google, and open-source/self-hosted model endpoints — this is what makes the Model Router in [System Architecture](03-system-architecture.md) provider-agnostic.
- **RAG pipeline:** chunking + embedding + reranking as a dedicated internal service, not inline in each engine, so retrieval quality improvements benefit every engine at once.
- **Tool-calling framework:** a shared contract (see [System Architecture §4](03-system-architecture.md#4-layers)) that every capability engine implements to become callable by any model.
- **Agent orchestration:** built on the tool-calling framework plus a persistence layer for agent state (`AGENT_RUN`, `TOOL_CALL` in [Database Design](05-database-design.md)) — not a separate framework bolted on later.

## Infrastructure

| Layer | Choice | Why |
|---|---|---|
| Containerization | Docker | Standard, matches team familiarity and CI tooling |
| Orchestration | Kubernetes | Independent scaling per engine (see [System Architecture §5](03-system-architecture.md#5-why-this-shape-not-a-monolith)) — chat scales on latency, automation scales on queue depth |
| GPU inference | Managed GPU clusters (cloud-provider or Anthropic/OpenAI/Google-hosted, depending on which models are self-hosted vs API-based) | Only self-host open-source models where cost or data-residency requirements justify it |
| CDN | Standard cloud CDN | Static assets, generated media |
| Observability | Structured logging + distributed tracing + metrics (e.g., OpenTelemetry-compatible stack) | Required for the per-request trace ID design in [System Architecture §6](03-system-architecture.md#6-cross-cutting-concerns) |
| CI/CD | Per-service pipelines, not one monolithic build | Matches the service-boundary architecture — a Research Engine change shouldn't trigger a Coding Studio redeploy |

## Deliberate non-choices (for now)

- **No custom-trained foundation model.** Aurora's differentiation is orchestration and workflow, not model training; using best-in-class third-party models via the gateway is faster to market and avoids a multi-year, capital-intensive detour.
- **No GraphQL as the primary API**, despite being listed as an option in the original brainstorm — REST + streaming covers v1–v3 needs with less operational complexity; GraphQL is reconsidered only if client-driven query flexibility becomes a real bottleneck.
- **No blockchain, no crypto payments** — not mentioned in the original brainstorm either, noted here only because platforms at this ambition level tend to attract the suggestion; it's out of scope.
