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
| [**Memory Layers for AI Agents**](memory-layers/) — every LLM call starts with amnesia, so what makes an agent seem to remember is a memory system built around it. Three pillars: what a memory *is* (text, table, graph), how the agent *finds* it (do nothing, keyword, RAG, Graph RAG), and how you *keep it true* (retire rather than delete, attribute, reflect). Then four real stores raced on identical facts against a no-memory control. Same author and harness as the entry above. [_read_](https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/memory-layers/) · [_ID_](https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/memory-layers/index.id.html) | Shen Sean Chen · Sean's AI Stories | Talk explainer · 30m26s | 2026-08-18 |
| [**Rethinking Claude Code Best Practices**](rethinking-claude-code/) — when Claude Code sessions run for hours unattended, the five in-loop jobs (steer, approve, say no, check, start) move to the model, the harness or the environment. The sharpest line is judgement versus guarantee: auto mode's classifier blocked 89% of planted dangerous commands, so about one in ten got through, while a deny rule is checked before the classifier ever sees the call. Then sandboxes, cloud sessions, hooks, CI and an orchestrator session. A vendor talk, and the entry says so. [_read_](https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/rethinking-claude-code/) · [_ID_](https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/rethinking-claude-code/?lang=id) | Lydia Hallie · Anthropic | Talk explainer · 17m31s | 2026-11-17 |

## Wanted

- A clear account of when multi-agent actually beats a single well-equipped agent — and when it just
  multiplies cost and failure surface.
- ~~Memory architectures compared on something other than vibes.~~ **Answered** by
  [memory-layers](memory-layers/): four real stores raced on identical facts, with a no-memory control
  group. Still open underneath it, though — that benchmark is n=1 with wall-clock timings and compares a
  local store against network calls, so *ranked* memory architectures on repeatable measurements remain
  wanted.
- What "planning" concretely buys over letting a strong model improvise inside a good loop.
- **What guardrails on a non-deterministic graph actually look like.** The loop-vs-graph entry
  establishes that they become mandatory once nodes and routing stop being deterministic, but stops
  short of designing them.
- **A threshold for "the pattern has settled."** "Consolidate a repeating loop into a graph" is good
  advice without a number attached.

---

[← All topics](../) · [Repository home](../../)
