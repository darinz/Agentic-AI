## Agentic Frameworks

Numerous frameworks exist for developing autonomous agents. They typically address skills/tool integration, memory, planning/orchestration, experiential learning, and multi‑agent coordination. This overview highlights common options, their trade‑offs, and when to choose each—plus guidance for teams that prefer to build directly against model/provider APIs.

### Quick comparison

| Framework | Primary focus | Orchestration model | Multi‑agent support | Learning/memory | Maturity | Best for |
|---|---|---|---|---|---|---|
| LangGraph | Inspectable, robust flows | Directed graphs with cycles, async, retries | Light/explicit | Externalized; pluggable | High | Production, complex single‑agent or light multi‑agent systems |
| AutoGen | Multi‑agent dialogues | Message/role based | Strong (manager/worker, self‑reflect) | Via prompts/tools; extensible | High | Research/production with multi‑agent collaboration |
| CrewAI | Speed and simplicity | Task/crew abstractions | Moderate | Basic | Medium | Rapid prototyping, assistants/support agents |
| OpenAI Agents SDK | Secure tool use, routing | Provider‑managed function/tools | Moderate (provider features) | Provider primitives | High | Teams standardized on OpenAI stack |

### How to choose

- If you need explicit, auditable control flow with robust retries and async steps, prefer LangGraph.
- If your problem is inherently multi‑agent (role negotiation, manager/worker, debate), try AutoGen.
- If you want to ship a prototype fast with minimal scaffolding, start with CrewAI.
- If you are all‑in on OpenAI’s ecosystem and want secure tool calling and routing out‑of‑the‑box, use OpenAI Agents SDK.
- If none of the above fit or you need extreme control/portability, build directly on model/provider APIs.

---

### LangGraph

- Strengths
  - Modular orchestration with directed graphs; nodes encapsulate logic (often model or tool calls); edges govern dataflow, loops, and error handling.
  - Strong developer ergonomics; native async, retries, and state passing; inspectable execution traces.
- Trade‑offs
  - Advanced planning/memory patterns require additional design; multi‑agent is possible but not the central abstraction.
- Best for
  - Robust single‑agent or light multi‑agent systems where explicit flow control, observability, and reliability matter.

### AutoGen

- Strengths
  - Powerful multi‑agent orchestration; dynamic role assignment; rich messaging between agents (manager/worker, self‑reflection, debate).
- Trade‑offs
  - Can be heavyweight for simple use cases; more opinionated interaction patterns to learn and govern.
- Best for
  - Research and production scenarios involving dialogue among agents, complex coordination, or reflective loops.

### CrewAI

- Strengths
  - Easy to learn; quick setup for prototyping with helpful abstractions like “crew” and “tasks.”
- Trade‑offs
  - Limited orchestration internals and customization compared to LangGraph/AutoGen for complex workflows.
- Best for
  - Fast prototyping of human‑centric assistants (support agents, copilots) where time‑to‑first‑value is key.

### OpenAI Agents SDK

- Strengths
  - Deep integration with OpenAI tool ecosystem; secure function calling; built‑in memory/tool routing primitives.
- Trade‑offs
  - Tight coupling to OpenAI infrastructure; reduced portability for custom or open‑source stacks.
- Best for
  - Teams already standardized on OpenAI APIs seeking the fastest path to secure tool‑using agents.

---

### Evaluation criteria (use this before you commit)

- Orchestration clarity: Can you inspect/trace decisions, retries, and tool calls?
- Reliability primitives: Timeouts, retries with backoff, circuit breakers, idempotency.
- Multi‑agent fit: Are roles, negotiations, and inter‑agent messaging first‑class?
- Memory and grounding: Retrieval hooks, episodic/semantic memory, knowledge attribution.
- Testing and evals: Support for offline evals, golden sets, scenario tests, red‑teaming.
- Observability: Structured logs for prompts, tools, outcomes, latencies, and costs.
- Governance: Policy enforcement (PII, jailbreak), rate limits, guardrails, audit trails.
- Portability: Cloud/vendor neutrality, open schemas (OpenAPI/JSON Schema), escape hatches.
- DX and ecosystem: Docs, community, adapters, and upgrade cadence.

### When to roll your own

- You need extreme performance constraints or nonstandard runtimes (edge/embedded).
- Compliance requires bespoke governance/observability beyond framework primitives.
- Your orchestration is simple, but integration depth with internal systems is high.

In practice, many teams prototype with CrewAI or OpenAI Agents SDK and migrate to LangGraph or AutoGen as requirements harden. This book emphasizes LangGraph for its balance of simplicity, inspectability, and production‑grade orchestration, while acknowledging that direct integration with provider APIs remains a perfectly valid approach when ultimate control or portability is required.