# Glossary

| Term | Definition |
|---|---|
| **Agent** | A role-scoped configuration (system prompt + allowed tools + memory scope + preferred model) that can be run independently of a chat thread. Defined in [Modules Overview](04-modules-overview.md). |
| **Approval tier** | The risk classification (read-only / low / medium / high) assigned to every AI-initiated action, governing whether it auto-executes or requires human approval. See [Security & Compliance §3](07-security-and-compliance.md#3-the-approval-tier-model-for-ai-initiated-actions). |
| **Auto Mode** | Model selection mode where the Model Router picks the model for a request based on task classification and cost/latency targets, rather than the user choosing explicitly. |
| **Canvas** | The multi-surface collaborative workspace combining chat, documents, diagrams, and code in one view (Phase 5). |
| **Confidence indicator** | A visible High/Moderate/Low signal attached to any factual claim returned by the Research or Knowledge Engine. |
| **Knowledge Vault** | The user-uploaded document/media store indexed for retrieval-augmented generation (RAG). |
| **Model Router** | The service that abstracts model providers behind one interface and selects which model handles a given request. |
| **Orchestration Engine** | The central request coordinator that loads context, invokes the Model Router and Tool-Calling Framework, and returns a unified response. The architectural "kernel" — see [System Architecture](03-system-architecture.md). |
| **RAG** | Retrieval-Augmented Generation — retrieving relevant content from a vector store to ground a model's response, rather than relying on the model's parametric knowledge alone. |
| **Tool-Calling Framework** | The shared contract every capability engine implements to be invokable by any model through the Orchestration Engine. |
| **Trace ID** | A unique identifier attached to a request at the gateway and propagated through every downstream service call, used for cost/latency attribution and debugging. |
