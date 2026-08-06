# Topic — Tool Use & Protocols

How a model reaches outside itself, and the wire formats that make that portable across vendors.

**In scope:** function/tool calling, tool schema design and naming, Model Context Protocol (MCP),
computer use and browser control, code execution and sandboxes, agent-to-agent protocols, permissioning
and approval gates, error handling and tool-failure semantics, streaming and partial results.

**Out of scope:** deciding *which* tool to call and when → see [`agent-architecture`](../agent-architecture/);
how tool results are packed into the prompt → see [`context-engineering`](../context-engineering/);
serving and scaling the tool backends → see [`infrastructure`](../infrastructure/).

## Entries

_No entries yet._ See [CONTRIBUTING.md](../../CONTRIBUTING.md) to add the first one.

## Wanted

- Tool schema design as a craft: how naming, granularity, and description wording change behaviour.
- MCP in practice — what it solves, where it is still rough.
- What models actually do when a tool fails, and how the harness should respond.

---

[← All topics](../) · [Repository home](../../)
