# Topic — Post-Training

How a base model is turned into something that behaves: follows instructions, uses tools, finishes
multi-step tasks, and can be specialised to one organisation's way of working.

**In scope:** supervised fine-tuning, RLHF/RLAIF, RL algorithms (GRPO, PPO and successors), reward
modelling and reward hacking, training environments and sandboxes, harness-agnostic training, distillation,
online and continual learning, self-improvement loops.

**Out of scope:** pre-training and architecture research (not an agentic concern yet); prompt-level
behaviour steering → see [`context-engineering`](../context-engineering/); measuring the resulting
behaviour → see [`evaluation-and-observability`](../evaluation-and-observability/).

## Entries

| Entry | Source | Format | Added |
| --- | --- | --- | --- |
| [**Learning on the Job: The Future of Post-Training**](learning-on-the-job/) — the four-stage ladder from single-turn Q&A to self-improving agents, why simulated environments produce reward hacking, and the "Bring Your Own Harness" answer. [_read_](https://aicaruss.github.io/sharing-knowledge/topics/post-training/learning-on-the-job/) | Raymond Feng, Applied Compute · AI Engineer World's Fair 2026 | Talk explainer · 18m20s | 2026-08-06 |

## Threads worth following

Open questions raised by the entries above, kept here so future research has somewhere to land:

- **What replaces GRPO when data is not replayable?** The source slide for this literally reads
  `OPSD??`. Anything credible on off-policy learning from production traces belongs in this topic.
- **Turning qualitative feedback into weight updates.** Production returns sentences, not scores.
- **Automating trace triage.** Going from a large batch of traces to a curated training set without a
  human reading every one.
- **Reward hacking as an environment problem.** Catalogue of real failure modes and the environment
  artifacts that caused them.

---

[← All topics](../) · [Repository home](../../)
