# Topic — Evaluation & Observability

How you find out whether the thing works — before shipping it, and while it runs.

**In scope:** eval design and dataset construction, LLM-as-judge and its biases, benchmarks and their
limits, regression suites for agents, trace collection and inspection, tracing standards, cost and
latency accounting, guardrails, drift detection, incident triage on agent failures.

**Out of scope:** using scores as a training signal → see [`post-training`](../post-training/);
the serving stack the traces come from → see [`infrastructure`](../infrastructure/).

## Entries

_No entries yet._ See [CONTRIBUTING.md](../../CONTRIBUTING.md) to add the first one.

## Wanted

- Grading multi-step trajectories, not just final answers.
- How LLM judges fail, and what to do about it beyond "use a bigger judge".
- Evals that survive contact with a production distribution that keeps moving.

---

[← All topics](../) · [Repository home](../../)
