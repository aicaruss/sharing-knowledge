# Topic — Agent Architecture

How an agent is put together above the model: the loop that drives it, what it remembers, how it
decomposes work, and what happens when you run more than one of them.

**In scope:** the agent loop and control flow, planning and task decomposition, memory (working,
episodic, long-term), reflection and self-critique, multi-agent topologies (supervisor/worker, swarm,
debate), delegation and hand-off, human-in-the-loop checkpoints, failure recovery and retries.

**Out of scope:** how tools are declared and invoked → see [`tool-use-and-protocols`](../tool-use-and-protocols/);
what goes into the prompt → see [`context-engineering`](../context-engineering/); training the model
that sits inside the loop → see [`post-training`](../post-training/).

## Entries

| Entry | Source | Format | Added |
| --- | --- | --- | --- |
| [**Loop Engineering vs Graph Engineering**](loop-vs-graph/) — the five-rung ladder from prompts to graphs, why loops and graphs are not competitors, and the three things that make an agent graph more than a 2023 DAG. [_read_](https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/loop-vs-graph/) | Shen Sean Chen · Sean's AI Stories | Talk explainer · 21m31s | 2026-08-11 |

## Wanted

- A clear account of when multi-agent actually beats a single well-equipped agent — and when it just
  multiplies cost and failure surface.
- Memory architectures compared on something other than vibes.
- What "planning" concretely buys over letting a strong model improvise inside a good loop.
- **What guardrails on a non-deterministic graph actually look like.** The loop-vs-graph entry
  establishes that they become mandatory once nodes and routing stop being deterministic, but stops
  short of designing them.
- **A threshold for "the pattern has settled."** "Consolidate a repeating loop into a graph" is good
  advice without a number attached.

---

[← All topics](../) · [Repository home](../../)
