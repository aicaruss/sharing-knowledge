# Topic — Evaluation & Observability

How you find out whether the thing works — before shipping it, and while it runs.

**In scope:** eval design and dataset construction, LLM-as-judge and its biases, benchmarks and their
limits, regression suites for agents, trace collection and inspection, tracing standards, cost and
latency accounting, guardrails, drift detection, incident triage on agent failures.

**Out of scope:** using scores as a training signal → see [`post-training`](../post-training/);
the serving stack the traces come from → see [`infrastructure`](../infrastructure/).

## Entries

| Entry | Source | Format | Added |
| --- | --- | --- | --- |
| [**From Signal to PR: Anatomy of a Self-Improving Agent**](signal-to-pr/) — observability stops being a dashboard and becomes machine input. Traces written to the repo as files, an agent that investigates before you wake up, and why you should now log ten times more. [_read_](https://aicaruss.github.io/sharing-knowledge/topics/evaluation-and-observability/signal-to-pr/) | Jason Lopatecki · Arize AI | Talk explainer · 20m35s | 2026-08-11 |
| [**Verification Debt: Guide, Verify, Solve**](verification-debt/) — the productivity spike expires in about three months; the static-analysis warnings and complexity do not. Why the quality gap scales with criticality, why human review is a leaky backstop (people follow confidently wrong AI advice 79.8% of the time), and the one criterion worth taking away: verify with a *different* methodology than the one that generated the code. A vendor talk, read with that disclosed. [_read_](https://aicaruss.github.io/sharing-knowledge/topics/evaluation-and-observability/verification-debt/) | Anirban Chatterjee · Sonar | Talk explainer · 22m31s | 2026-08-11 |

## Wanted

- Grading multi-step trajectories, not just final answers.
- How LLM judges fail, and what to do about it beyond "use a bigger judge".
- Evals that survive contact with a production distribution that keeps moving.
- **The bill for "trace 10× more."** The signal-to-pr entry recommends an order-of-magnitude increase in
  telemetry without costing the storage, ingestion, or continuous-eval inference.
- **Trace selection as a craft.** Facets, cohorting by customer, picking the right group of traces for
  one session — named as the hard part, nowhere explained in depth.

---

[← All topics](../) · [Repository home](../../)
