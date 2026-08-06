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

_No entries yet._ See [CONTRIBUTING.md](../../CONTRIBUTING.md) to add the first one.

## Wanted

- A clear account of when multi-agent actually beats a single well-equipped agent — and when it just
  multiplies cost and failure surface.
- Memory architectures compared on something other than vibes.
- What "planning" concretely buys over letting a strong model improvise inside a good loop.

---

[← All topics](../) · [Repository home](../../)
