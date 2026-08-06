# Topic — Context Engineering

Everything about deciding what the model sees. The prompt is only part of it; the harder problem is
budgeting a finite context window across instructions, history, retrieved knowledge, and tool output.

**In scope:** prompt design and system prompts, retrieval-augmented generation, chunking, embeddings and
re-ranking, context-window budgeting, compaction and summarisation of long histories, caching, structured
output, few-shot selection, instruction hierarchies and conflict resolution.

**Out of scope:** the retrieval infrastructure itself → see [`infrastructure`](../infrastructure/);
whether the answer was any good → see [`evaluation-and-observability`](../evaluation-and-observability/);
baking behaviour into weights instead of the prompt → see [`post-training`](../post-training/).

## Entries

_No entries yet._ See [CONTRIBUTING.md](../../CONTRIBUTING.md) to add the first one.

## Wanted

- Context compaction strategies for long-running agents, with the failure modes of each.
- When retrieval beats a longer context window, and when it is just added latency.
- Prompt-caching economics for agent loops that replay a growing prefix on every turn.

---

[← All topics](../) · [Repository home](../../)
