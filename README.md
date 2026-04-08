<p align="center">
  <img src="static/aexor-logo-cropped-tight.png" alt="Aexor Logo" width="200">
</p>

<h1 align="center">Aexor</h1>

<p align="center">
  <strong>Preview-first personal assistant with deterministic planning and adaptive execution</strong>
</p>

**Status:** Backend complete — currently designing and refining the UI
**Deployment:** Self-hosted, single-tenant, multi-user

Aexor is a personal AI assistant that produces immutable plan DAGs where LLM Reasoner steps can spawn bounded new steps at runtime, creating versioned revisions with policy attestations. All execution runs through a pure Python/FastAPI runtime with MCP tool invocations.

---

## Demo

<p align="center">
  <a href="https://www.loom.com/share/8bfadf98c7634be29dba70eae6e4a512">
    <img src="https://img.shields.io/badge/▶_Watch_Demo-Schedule_Meeting_+_Gmail-blue?style=for-the-badge&logo=loom&logoColor=white" alt="Watch Demo on Loom">
  </a>
</p>

> *"Schedule a meeting and send a Gmail notification"* — watch Aexor plan, preview, and execute an end-to-end use case.

---

## How It Works

```
User Request → Understand → Plan → Preview → Approve → Execute → Learn
     ↓            ↓          ↓        ↓          ↓         ↓        ↓
  [Message]   [Intent]   [Plan    [Show    [Confirm]  [Do It]  [Remember]
                          DAG]     Me]
```

**Core flow:**
1. **Understand** — collect user intent across multiple messages
2. **Plan** — generate a deterministic plan DAG (same inputs → same graph)
3. **Preview** — show what will happen (no side effects)
4. **Approve** — wait for user confirmation
5. **Execute** — dispatch steps via MCP (APIs) and Anthropic API (reasoning)
6. **Learn** — persist outcomes for future context

---

## Architectural Principles

1. **Preview-first safety** — never execute without showing the user first
2. **Deterministic planning with adaptive execution** — initial plan is immutable; Reasoner steps may spawn bounded new steps at runtime, creating new revisions with policy attestations
3. **Pure agentic runtime** — all steps dispatched via MCP (APIs) and Anthropic API (reasoning)
4. **Two-tier LLM execution** — sandboxed Tier 1 (untrusted external data, no tools) + capable Tier 2 (agent reasoning, MCP tools)
5. **Default-untrusted rule** — all external API data must pass through Tier 1 sanitization before reaching Tier 2 Reasoners
6. **Policy governance** — actions are only allowed when an explicit policy rule matches

---

## Security & Reliability

- **Prompt injection defence** — two-tier LLM architecture ensures untrusted external data is sanitized in a sandboxed tier before it ever reaches agent reasoning
- **Append-only audit trail** — every plan, execution, and approval event is recorded for full traceability
- **Observability** — structured logging and execution monitoring with stuck-detection and timeout enforcement
- **Credential isolation** — AES-256-GCM encrypted vault; LLM never sees plaintext secrets
- **Human-in-the-loop** — critical actions always require explicit user approval before execution

---

## Tech Stack

| Category | Technology |
|----------|-----------|
| Backend | Python 3.11+, FastAPI, Pydantic v2 |
| Database | PostgreSQL 16 |
| Vector DB | pgvector (hybrid BM25 + semantic search) |
| Cache | Redis 7 with hiredis |
| AI/LLM | Anthropic Claude (local model support in progress) |
| RAG | Context engineering with tiered evidence gathering |
| Prompt Engineering | Structured prompts, two-tier trust model |
| Embeddings | ONNX Runtime (local CPU inference) |
| Tools | MCP protocol via Composio |

