# Security & Compliance

## 1. Why this doc exists earlier than the original plan had it

The original roadmap placed security and compliance in Phase 6, alongside launch. That's a common and expensive mistake: RBAC, audit logging, and encryption-at-rest are architectural decisions, not features you layer on afterward. This repository moves the *design* of these systems to Phase 3 (see [Roadmap](10-roadmap.md)) even though full certification (SOC 2, ISO 27001) realistically can't complete until there's a stable system to audit.

## 2. Identity & access

- **Authentication:** email/password (with breach-password checking), OAuth (Google, Microsoft, GitHub, Apple), SAML/OIDC SSO for enterprise, passkeys, and MFA (TOTP + WebAuthn).
- **Authorization:** role-based access control (RBAC) at the organization, workspace, and project level. Roles are not hard-coded to "admin/member" — organizations can define custom roles with scoped permissions.
- **Session management:** short-lived access tokens, refresh tokens with rotation, device-level session listing and revocation.

## 3. The approval-tier model for AI-initiated actions

This is the core safety mechanism for the Execution Layer and Automation Engine (see [Modules Overview](04-modules-overview.md)). Every action an agent or automation can take is classified into a risk tier at definition time:

| Tier | Examples | Default behavior |
|---|---|---|
| **Read-only** | Search, summarize, query a connected system | Auto-approved, always |
| **Low-risk write** | Draft a document, create a calendar hold, generate a report | Auto-approved, logged, undoable |
| **Medium-risk write** | Send an internal Slack message, update a CRM record | Requires approval unless explicitly pre-authorized by the user for that specific automation |
| **High-risk / external-facing** | Send an external email, modify a database, deploy code, spend money | Always requires explicit human approval per action, no exceptions |

This tiering is enforced at the data layer via `TOOL_CALL.approval_status` (see [Database Design](05-database-design.md)), not only in application logic, so it can't be silently bypassed by a code change in one service.

## 4. Data protection

- **Encryption in transit:** TLS 1.2+ everywhere, including internal service-to-service calls.
- **Encryption at rest:** AES-256 for object storage and database volumes; enterprise tier supports customer-managed keys (BYOK).
- **Data residency:** organization-level region pinning (`ORGANIZATION.data_residency_region` in the schema), enforced at the API gateway routing layer.
- **Training data usage:** user content is never used to train third-party or first-party models without explicit, revocable, per-organization opt-in. This is a contractual commitment, not just a UI toggle.
- **Retention:** configurable per organization; deleted conversations and memory are purged from primary stores within a defined SLA and from backups on the next backup rotation.

## 5. Audit & observability

- Every state-changing action (config change, permission change, tool execution above read-only tier) writes an immutable `AUDIT_LOG_ENTRY`.
- Admins get a queryable audit log UI (see [Modules Overview — Admin Panel](04-modules-overview.md)) filterable by actor, action type, and date range.
- Security-relevant anomalies (impossible-travel login, mass export, repeated failed MFA) trigger alerts, not just log entries.

## 6. Compliance roadmap

| Certification | Target phase | Notes |
|---|---|---|
| SOC 2 Type I | Phase 4 | Achievable once RBAC, audit logging, and encryption are stable in production |
| SOC 2 Type II | Phase 6 | Requires a sustained observation period after Type I |
| GDPR readiness | Phase 4 | Data residency, right-to-deletion, and data processing agreements |
| HIPAA readiness | Phase 6 | Only pursued if healthcare vertical demand justifies the BAA and infrastructure overhead |
| ISO 27001 | Phase 6 | Aligned with SOC 2 Type II timeline to share audit evidence |

## 7. Threat model highlights

- **Prompt injection via uploaded documents or web content** — the Research Engine and Knowledge Engine must treat retrieved content as untrusted data, not instructions, with the Orchestration Engine responsible for enforcing that boundary (mirrors the architecture in [System Architecture](03-system-architecture.md)).
- **Agent privilege escalation** — an agent's `allowed_tools` scope (see schema) is enforced at the Tool-Calling Framework, not by the agent's own system prompt; a compromised or poorly-written prompt cannot grant itself new tool access.
- **Cross-tenant data leakage** — vector store queries and knowledge retrieval are always scoped by organization/project ID at the query level, never filtered post-retrieval.
