# API Specification

## 1. Design principles

- **Every capability engine is reachable directly**, not only through chat. The Research Engine, Document Studio, and Coding Studio each expose their own endpoints so integrators can use one capability without paying for a full chat round-trip.
- **Streaming by default for anything model-driven.** Chat, agent runs, and research reports stream via Server-Sent Events; only short, deterministic endpoints (auth, CRUD) are plain request/response.
- **Idempotency on anything that executes an action.** Automation and execution-layer endpoints require an `Idempotency-Key` header — retried requests must not double-send an email or double-trigger a workflow.

## 2. Base

```
https://api.aurora.ai/v1
```

Authentication via `Authorization: Bearer <token>` (OAuth2) or `X-API-Key` for server-to-server use.

## 3. Core endpoints (v1 scope)

### Chat

```
POST /v1/conversations
GET  /v1/conversations/{id}
POST /v1/conversations/{id}/messages          # streams a response
GET  /v1/conversations/{id}/messages
```

**Request — send a message**
```json
POST /v1/conversations/{id}/messages
{
  "content": "Summarize the attached report and flag any risk factors.",
  "attachments": ["file_9f2a..."],
  "model": "auto",
  "mode": "research"
}
```

**Response (streamed, final chunk shown)**
```json
{
  "message_id": "msg_88ac...",
  "role": "assistant",
  "content": "The report identifies three risk factors...",
  "model_used": "claude-sonnet-5",
  "citations": [
    {"source": "report.pdf", "page": 4}
  ],
  "confidence": 0.87
}
```

### Memory

```
GET    /v1/users/{id}/memory
POST   /v1/users/{id}/memory
DELETE /v1/users/{id}/memory/{item_id}
```

Memory is fully user-addressable — this is the API-level enforcement of the "user controls everything" principle from [Vision & Strategy](01-vision-and-strategy.md).

### Research

```
POST /v1/research/reports              # async job
GET  /v1/research/reports/{id}         # poll or subscribe to status
```

```json
POST /v1/research/reports
{
  "query": "Competitive landscape for AI orchestration platforms, 2025-2026",
  "sources": ["web", "news", "academic"],
  "depth": "standard"
}
```

### Agents & Automation

```
POST   /v1/agents                       # define an agent (system prompt, tools, model)
POST   /v1/agents/{id}/runs             # start a run
GET    /v1/agents/{id}/runs/{run_id}
POST   /v1/agents/{id}/runs/{run_id}/approve   # approve a pending tool call
POST   /v1/automations                  # define trigger → action workflow
```

### Documents

```
POST /v1/documents/convert
POST /v1/documents/compare
POST /v1/documents/extract
```

## 4. Errors

Standard problem-details shape:

```json
{
  "error": {
    "code": "model_provider_unavailable",
    "message": "The selected model is temporarily unavailable; retried with fallback model claude-sonnet-5.",
    "request_id": "req_1a2b3c"
  }
}
```

Every error includes a `request_id` correlated to the trace ID described in [System Architecture §6](03-system-architecture.md#6-cross-cutting-concerns), so support and debugging never start from "it didn't work."

## 5. Rate limiting

Returned via standard headers (`X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`). Limits are tiered by plan and are higher for asynchronous endpoints (research, automation) than for synchronous chat, since the former queue rather than block.

## 6. SDKs

v1 targets Python and JavaScript/TypeScript SDKs (matching the frontend and backend languages in [Tech Stack](09-tech-stack.md)); Go, Java, C#, and PHP are Phase 3+ once the API surface is stable enough that maintaining five SDKs isn't churn.

## 7. Versioning

Path-based (`/v1`, `/v2`), with a minimum 12-month deprecation window for any breaking change once the API is publicly available (Phase 3 onward).
