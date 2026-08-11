# Topics

The taxonomy this knowledge base is organised around. Seven topics, chosen so that every entry has
exactly one obvious home. Each topic folder states its own scope and lists its entries.

| Topic | What lands here | Entries |
| --- | --- | --- |
| [**post-training**](post-training/) | RL, fine-tuning, reward design, training environments, custom models | 1 |
| [**agent-architecture**](agent-architecture/) | The agent loop, planning, memory, multi-agent topologies | 1 |
| [**tool-use-and-protocols**](tool-use-and-protocols/) | Function calling, MCP, computer use, agent protocols | 0 |
| [**context-engineering**](context-engineering/) | Prompting, RAG, retrieval, context-window budgeting | 0 |
| [**evaluation-and-observability**](evaluation-and-observability/) | Evals, benchmarks, tracing, guardrails, cost accounting | 1 |
| [**infrastructure**](infrastructure/) | Serving, inference, sandboxes, latency and cost | 0 |
| [**applied-and-case-studies**](applied-and-case-studies/) | Real deployments, post-mortems, enterprise patterns | 0 |

## Choosing a topic for a new entry

Pick by **what the material is fundamentally about**, not by what it mentions in passing. A talk about
evaluating a multi-agent system is `evaluation-and-observability`, even though it is full of
architecture. If two topics genuinely fit, file it under the one a reader would search first and
cross-link from the other topic's README.

Adding an eighth topic is allowed but should be rare — it means something genuinely does not fit the
seven. Prefer a tag over a new folder.

---

[Repository home](../) · [How to add an entry](../CONTRIBUTING.md)
