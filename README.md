<p align="center">
  <img src="static/aexor-logo-cropped-tight.png" alt="Aexor Logo" width="200">
</p>

<h1 align="center">Aexor</h1>

<p align="center">
  <strong>Preview-first personal assistant with deterministic planning and adaptive execution</strong>
</p>

**Status:** Under active development
**Deployment:** Self-hosted, single-tenant, multi-user

Aexor is a personal AI assistant that produces immutable plan DAGs where LLM Reasoner steps can spawn bounded new steps at runtime, creating versioned revisions with policy attestations. All execution runs through a pure Python/FastAPI runtime with MCP tool invocations.

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

## Tech Stack

| Category | Technology |
|----------|-----------|
| Backend | Python 3.11+, FastAPI, Pydantic v2 |
| Database | PostgreSQL 16 + pgvector |
| Cache | Redis 7 with hiredis |
| AI/LLM | Anthropic Claude |
| Embeddings | ONNX Runtime (local CPU inference) |
| Tools | MCP protocol |

---

## License

MIT
