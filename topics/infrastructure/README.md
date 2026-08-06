# Topic — Infrastructure

The machinery underneath: what actually runs the model, the tools, and the environments — and what it
costs.

**In scope:** inference engines and serving, batching and throughput, KV-cache behaviour, routing and
fallback across providers, sandbox and execution isolation, queueing and concurrency for long-running
agents, state and checkpointing, cost modelling, latency budgets, deployment topologies.

**Out of scope:** the training stack itself → see [`post-training`](../post-training/); what you
measure once it runs → see [`evaluation-and-observability`](../evaluation-and-observability/).

## Entries

_No entries yet._ See [CONTRIBUTING.md](../../CONTRIBUTING.md) to add the first one.

## Wanted

- Sandbox designs for untrusted agent-generated code, compared on isolation vs. start-up cost.
- What a realistic cost model for an agent fleet looks like once retries and long contexts are included.
- Running agent workloads that live for hours without holding a process open the whole time.

---

[← All topics](../) · [Repository home](../../)
