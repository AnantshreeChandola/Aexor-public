<p align="center">
  <img src="static/aexor-logo-cropped-tight.png" alt="Aexor" width="200">
</p>

<h1 align="center">Aexor</h1>

<p align="center">
  <strong>Preview-first personal agent framework</strong><br>
  <em>Never acts without showing you first.</em>
</p>

---

Aexor is an agentic execution framework built on a simple principle: **show, then do.**

Every action goes through a preview-approve-execute loop so you stay in control while the agent handles the work.

**Key ideas**

- **Preview-first safety** — see exactly what will happen before anything executes
- **Policy-bounded execution** — deny-by-default policy engine keeps the agent within explicit guardrails
- **Deterministic planning, adaptive execution** — plans are fixed DAGs; only designated reasoning steps introduce runtime decisions
- **Pure agentic execution** — Python/FastAPI orchestrator dispatching via MCP tool connectors
- **Two-tier LLM trust model** — untrusted external data is sanitized before any agent reasoning touches it

**Status:** Under active development. Not yet ready for external contributions.

---

*Built with Python 3.11, FastAPI, and the MCP connector ecosystem.*
