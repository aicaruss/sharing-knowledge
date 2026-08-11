---
title: "Loop Engineering vs Graph Engineering — two AI agent buzzwords, taken slowly"
slug: loop-vs-graph
topic: agent-architecture
type: talk-explainer
language: en
status: published
added: 2026-08-11
source_type: conference-talk
source_title: "You Can Learn AI Agent Graph Engineering In 21 Min | Loop, Harness, System Design, Waku Agent"
source_url: https://www.youtube.com/watch?v=IMLwvK08JVc
source_author: Shen Sean Chen
source_org: "Sean's AI Stories (YouTube channel)"
source_published: 2026-08-01
source_duration: 21m31s
tags:
  - loop-engineering
  - graph-engineering
  - orchestration
  - parallelism
  - dag
  - procedural-memory
  - agent-harness
  - llm-as-judge
---

# Loop Engineering vs Graph Engineering

**[▶ Open the explainer](index.html)** · [Watch the source video ↗](https://www.youtube.com/watch?v=IMLwvK08JVc)

> Reading online? → <https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/loop-vs-graph/>

---

## Why this is in the knowledge base

Two words got loud in mid-2026 and a lot of people started picking sides. This is the entry that says
there is no side to pick, and then earns that claim with a live codebase rather than a whiteboard.

Its real value is not the loop/graph comparison — that resolves in one table. It is the **five-rung
ladder** in section 2: prompt → context → skills → loop → graph, where each rung exists because the one
below it ran out of road. That ladder is the cheapest way to place any new agent buzzword, including
ones that haven't been coined yet, and it gives you a decision rule for which rung a given problem
actually needs.

## In one paragraph

Loops and graphs are not competitors. A **loop** is what you reach for when you know the *goal* but not
the steps — hand the model a goal and a toolbox and let it decide each move, one at a time. A **graph**
is what you reach for when you already know the *shape* of the work — draw the nodes and edges up front
so the steps can run together instead of queueing. Every graph node can itself contain a loop, so a
graph *wraps* loops rather than replacing them. The practical order is: write the skill first, and only
consolidate into a graph once you notice the same pattern coming round again and again. Yes, a graph is
structurally the same DAG we've had since 2023 — but three things are genuinely new: a node can be an
LLM call, the model itself can choose the edge, and because both are uncertain the flow now needs
guardrails.

## Key takeaways

1. **The ladder is the real content.** Prompt engineering (give it a role) → context engineering (give
   it data) → skills (give it an SOP) → loop (give it a goal and a toolbox) → graph (give it a route
   map). Each rung exists because the one below it wasn't enough. Climb only as far as the problem
   requires.
2. **It's a pendulum, not a march.** Skills means "follow a strict procedure". Loop means "go figure it
   out yourself". Graph is the settlement in the middle — a fixed shape with the uncertain parts fenced
   inside specific nodes.
3. **A graph buys speed and predictability, not intelligence.** The intelligence still lives in the
   loops inside the nodes. A loop runs sequentially because each step waits on the model's next
   decision; a graph was told the shape up front, so its branches set off together.
4. **Graphs wrap loops — this is demonstrated, not asserted.** In the author's own `/gather` workflow,
   four branches run in parallel, and the "web search" node is itself a loop that keeps digging until it
   finds something.
5. **Don't reach for a graph too early.** Graphs pay off once a process has stabilised. Applied to a
   workflow that is still shifting, a graph just relocates the complexity into a rigid shape.
6. **Three things make it more than a 2023 DAG.** Nodes are non-deterministic (a node can be an LLM
   call); routing can be handed to the model as a judge; and that uncertainty is exactly why guardrails
   become mandatory where a deterministic pipeline never needed them.
7. **On buzzwords generally.** A term goes viral either because someone with reach said it, or because
   it is genuinely useful — the author's point is that telling those two apart is the job. The whole
   argument here started from a single post that drew roughly three million views.

## Concepts you will pick up

| Term | Why it matters here |
| --- | --- |
| **Loop** | Model picks the next step, one at a time. Sequential, unpredictable in length, right for exploratory work. |
| **Graph** | You draw nodes and edges up front. Parallel, predictable, right for work whose pattern has settled. |
| **Procedural memory** | The harness-language name for "skills" — a rule that fires when a situation comes up, no extra data needed. |
| **Node / edge** | A node is the work (tool call, LLM call, agent, MCP server, router); an edge answers "where next once this finishes". |
| **LLM-as-a-judge routing** | Handing edge selection to a model: cheap model or strong one? Something an old DAG could never do. |
| **Guards** | Guardrails a flow needs *because* its nodes and routing are non-deterministic. |

## Why it lands in `agent-architecture`

The subject is orchestration topology — how control flows between the model, the tools and the steps.
It touches skills and procedural memory, which brush against
[`context-engineering`](../../context-engineering/), and its guardrail argument brushes against
[`evaluation-and-observability`](../../evaluation-and-observability/), but the load-bearing question is
architectural: *who decides the next step, and when is that decision made?*

## Worth noting for our own context

The closing takeaways make an explicit case for graphs in **banking and enterprise settings**: heavy on
SOPs, heavy on audit requirements. The argument is that a graph makes steps traceable and routes
auditable while keeping the non-deterministic parts fenced inside named nodes — which is a different and
more defensible posture than letting a single loop roam across a regulated workflow.

## Still open

- **No measured numbers.** The timeline comparison is explicitly illustrative, not benchmarked. How much
  wall-clock a graph actually saves on a real workload is left unanswered.
- **Where the boundary sits.** "Consolidate into a graph once the pattern repeats" is good advice
  without a threshold. How many repetitions, and how do you tell a settled pattern from a coincidence?
- **Guardrails are named, not designed.** The talk establishes that non-deterministic flows need guards
  but does not say what they look like.

## Also referenced in the source

- **Peter Steinberger's post on X** (18 July 2026) — *"are we still talking about loops, or did we shift
  to graphs yet?"* — the post that started the argument.
- **Waku Agent** — the author's open-source local-first assistant used for the live demo; the graph
  engine lives in `waku/graph/`, with one `.py` file per workflow under `waku/graph/workflows/`.
- **Airflow** and **AWS Step Functions** — the 2023-era deterministic workflow tools the "isn't this
  just a DAG?" objection rests on.
- **Harrison Chase** on harnesses and memory — surfaced by the demo's own web-search branch.

## Related entries

- [**Learning on the Job: The Future of Post-Training**](../../post-training/learning-on-the-job/) —
  useful contrast. Both talks care about the harness, but from opposite ends: this one designs the
  harness, that one trains a model to be good *inside* someone else's.
- [**From Signal to PR**](../../evaluation-and-observability/signal-to-pr/) — the guardrail question
  raised here is the observability question answered there.

## Provenance

Compiled from the video's transcript. **The diagrams are redrawn to clarify what the video explains
verbally — they are not screenshots of the original whiteboard**, and in places they visualise an
argument that was spoken rather than drawn. The timeline figure in section 6 is illustrative: bar
lengths convey relative duration, not measurements.

Note on presentation: this explainer carries its own palette and its own components (`.hero`, `.rung`,
`.ladder`) rather than the house cream-and-orange set, and it is the first entry here that supports
dark mode. See [Design system](../../../README.md#design-system).

> **Correction, 2026-08-11.** Two metadata fields were wrong and have been fixed against the source.
> `source_title` read *"Loop Engineering VS Graph Engineering, Buzzwords Clearly Explained"* — a title
> inherited from the intermediate artifact this entry was written from, and not the video's own. The
> canonical title is now recorded above. `source_published` read **2026-08-02**, derived from a relative
> "9 days ago" reading rather than the exact date; YouTube reports **2026-08-01**. The body of the
> explainer was checked against the transcript and needed no change — the error was confined to
> attribution.
