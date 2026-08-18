---
title: "Memory Layers for AI Agents — what a memory is, how the agent finds it, how you keep it true"
slug: memory-layers
topic: agent-architecture
type: talk-explainer
language: en
status: published
added: 2026-08-18
source_type: conference-talk
source_title: "You Can Learn AI Agent Memory Layers | Graph RAG, Vector DB, SQLite, Hermes, Waku"
source_url: https://www.youtube.com/watch?v=072eNztI06k
source_author: Shen Sean Chen
source_org: "Sean's AI Stories"
source_published: 2026-08-16
source_duration: 30m26s
tags:
  - agent-memory
  - procedural-memory
  - semantic-memory
  - graph-rag
  - vector-stores
  - sqlite
  - agent-harness
---

# Memory Layers for AI Agents

**[▶ Open the explainer](index.html)** · [Baca dalam Bahasa Indonesia](index.id.html) · [Watch the source video ↗](https://www.youtube.com/watch?v=072eNztI06k)

> Reading online? → <https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/memory-layers/>

---

## Why this is in the knowledge base

This topic's **Wanted** list asks for "memory architectures compared on something other than vibes". This
is the closest thing yet: four contenders seeded with the same four facts, asked the same three questions,
timed, and run against a **control group with no memory at all** — a control that passes by correctly
reporting that it has no record, which is the baseline that stops you crediting a memory layer for the
model's guesswork.

The framework matters more than the race. The subject is **state** — what an agent knows between calls —
which is why it sits here rather than in [`context-engineering`](../../context-engineering/), where only
pillar 2 would belong. What it is not: an informal n=1 race, run by the author of the harness it runs
inside, timing local disk against network calls.

## In one paragraph

A model remembers nothing, so anything that looks like recall is a memory system somebody built around it
— and that system answers three questions. **What a memory is:** plain text, rows in a table, or a graph of
nodes and edges; embeddings are not a fourth kind, they live inside one of the three. **How the agent finds
it:** do nothing and preload the file into context, keyword search, RAG, or Graph RAG, which embeds edges as
well as nodes so retrieval returns relationships rather than isolated facts. **How you maintain it:** add,
delete, overwrite, noop, retire, attribute, reflect — *retire* meaning you bound an obsolete fact with a
validity window instead of deleting it, so last week's answer stays explainable. He surveys five layers
— plain text, SQLite, vector stores, mem0, Zep — plus LangMem, which is a package rather than a store. He
then races four entries on a dinner party against a no-memory control: SQLite, mem0 and Zep from that list,
plus LangMem. Plain text is not entered and the vector store is never tested. Of the four, the least
sophisticated is the fastest; the temporal graph spends most of the demo seeding,
yet yields the test's one genuinely valuable artifact — an edge reading *"revealed ending of"*. His
conclusion: the harness is replaceable, so the memories are the asset, provided you maintain them.

## Key takeaways

1. **"Does the model remember me?" is the wrong question.** Someone chose where the facts live, how they
   are fetched, and what happens when they go stale — three separable decisions, which is why the framing
   outlives any product comparison.
2. **The first retrieval strategy is no retrieval.** A short memory file is simply preloaded into context;
   Hermes and Waku Agent use no embeddings at all. The cost: it does not scale, and everything preloaded
   competes for the same window.
3. **Retire beats delete because of tracing.** 1,000 stars on day 25, 1.3k on day 26 — overwrite the old
   number and the 30%-in-a-day jump goes with it, along with any way to explain an answer that used it.
4. **Graph RAG's payoff is in the edge.** Tom Holland to his next film reads **"revealed ending of"**: a
   summarised relationship, not a bare link. Other edges are thinner — one carries the chili-oil stain but
   no guest.
5. **The unglamorous option wins, with an asterisk.** SQLite answers in 4.6s while the hosted graph is still
   seeding — but SQLite is local and the rest are network calls, so part of that gap is latency, not
   retrieval quality.
6. **Keyword search has a language boundary.** Asked in Chinese, SQLite retrieved the right fact and replied
   in English (10.3s); mem0 replied in Chinese. His explanation is hedged, and worth keeping hedged.

## Concepts you will pick up

| Term | Why it matters here |
| --- | --- |
| **The three questions** | What a memory *is* / how the agent *finds* it / how you *maintain* it — a checklist for placing any memory product. |
| **Do nothing (as retrieval)** | Preloading a short memory file into context: the baseline most RAG discussion skips. |
| **Retire / supersede** | Invalidating a fact with a time range instead of deleting it. Transfers to every store; it is Zep's whole model. |
| **Attribute** | Recording a fact's origin. "The agent believes X" versus "believes X because the user said so on Tuesday". |
| **Graph RAG** | Embedding nodes *and* edges, so a search returns a relationship subgraph rather than a ranked list. |
| **Control group** | An agent with no memory, entered in the race. It passes by correctly saying it has no record. |

## Worth noting for our own context

Pillar 3 is what matters in a regulated or audited setting, and almost no product leads with it. **Retire
plus attribute** makes an answer reconstructible months later: the fact, its window of validity, and where
it came from. A store that only overwrites cannot give you that at any price.

## Still open

- **The benchmark is not a benchmark, and he does not claim otherwise** — one run per question, wall-clock
  only, no repetitions, no statistics.
- **Latency is not separated from retrieval quality.** *My assessment, not his:* timing a local file against
  hosted services confounds the interesting question with the easy one.
- **The language result is unexplained** — "found nothing useful" and "found it and answered in the wrong
  language" are never separated.
- **One store and one mode were never tested.** Supabase PGVector by choice ("we're not testing embeddings
  here"), mem0's graph mode behind a paywall. That row of the comparison is theory.
- **"Dreaming" is not citable as presented** — attributed to Anthropic with no paper, author or link.
- **Consolidation policy is asserted, not justified.** He consolidates "after every, you know, say five or
  10 conversations using some cheaper auxiliary models" (11:33) — with no account of what distillation
  loses, or how you would know.

## Also referenced in the source

- **Waku Agent** — the author's own open-source harness, `pip install waku-agent`, 1.3k+ GitHub stars at
  recording; the arena and dashboard are part of it.
- **Hermes** — another harness, cited for its plain-text `.hermes/memory/memory.md` and `state.db`.
- **mem0** (row and graph memory, both vectors; graph mode paywalled) · **Zep** (temporal graph: nodes,
  edges, validity windows) · **LangMem** — LangChain's library; "There's no stores. It's basically a
  package" (17:27) · **Supabase PGVector**, **Weaviate**, **Pinecone**, described but not tested.
- **Anthropic's "dreaming"** — reflection scheduled while the agent is idle. No paper, author or link given.

## Related entries

- [**Loop Engineering vs Graph Engineering**](../loop-vs-graph/) — same author, same Waku Agent harness,
  same series, and the direct predecessor: it named the retrieval gate and the procedural / semantic /
  episodic split in one line, and this is that line as a whole video. It also answers this topic's
  **Wanted** item on comparing memory architectures on something other than vibes — with the caveat that
  what arrives is one informal n=1 race, not a measured study.
- [**From Signal to PR**](../../evaluation-and-observability/signal-to-pr/) — the same conclusion from the
  opposite direction: there, what works is writing production traces into the repo *as files*, because
  coding harnesses are magical with files and hopeless with a dashboard; here, it is keeping memory as
  plain text preloaded into context, with no retrieval and no embeddings at all.

## Provenance

Compiled from the video's **auto-generated caption track** (393 segments, 0:00–30:25) and the video's own
**24 chapters**, which supply every section boundary and the titles in the explainer's chapter index. No
product documentation was consulted. The 24 chapter titles are the creator's own strings from the video record rather than transcriptions of his speech — two of them are tidier than anything he says aloud, the "1,300 stars" figure and "a package, not a store".

**Not re-checked against the live page.** At verification time the source could not be reached from this
environment — the metadata tool timed out repeatedly, a page fetch returned nothing, browser access was
blocked by policy — so every `source_*` field rests on the original harvest, checked for internal
consistency only and not against YouTube as it stands today.

**Figures.** Seven inline SVG figures, no screenshots. **Figure 1 is redrawn from a single frame captured
at 4:56** and the written record of what it showed; the original also carries a hand-drawn stick figure,
the speaker's live inset and a burnt-in caption, not reproduced. **Figures 2–7 are reconstructions from
the spoken description** — illustrations of what the video explains verbally, not reproductions of screens.
Six of seven planned captures failed (the tab could not be kept in the foreground), so the results
dashboard, the seeding screen and the graph UI were rebuilt from narration; Figure 6's grid is our
arrangement of numbers he reads aloud, and Figure 7 is a fragment of a larger graph. Nothing that existed
only on screen is quoted: where he reads a record aloud, the entry says so and paraphrases.

**Quotes and spellings.** Block quotes are verbatim from the caption track with timestamps; short quoted
phrases in prose and figures are verbatim too but do not all carry one. Because the track is
machine-generated, a quote is its rendering of the speech, one step removed from the audio. The captions
garble product names throughout — Zep as "Zap"/"Zeb", mem0 as "Memzer"/"Mem Zero", LangMem as "Lam Mem",
Supabase as "Superbase", `SOUL.md` as "so.md" — so corrected spellings are used in prose and no product
name is asserted on the transcript's authority alone.

**Metadata.** `source_published` is exact from the video record (16 August 2026); there is no separate
delivery date to confuse it with, this being a channel video rather than a recorded talk. For that reason
`source_type: conference-talk` is a poor fit — it is the closest value in the repository's closed enum, and
matches the sibling entry from the same channel. **The title is not stable at source:** two different
titles were observed within two hours, one from the API and one from the live watch page, with an unchanged
upload date — most likely a creator-side title test. `source_title` records the API form because it is
reproducible from the video record; the other observed form was *"You Can Learn To Store, Retrieve &
Maintain AI Agent Memory | Graph RAG, SQLite, Hermes, Waku"*. Neither is asserted as *the* title.

**Disclosures carried in the explainer.** The author wrote Waku Agent, the harness the arena runs inside,
and the plain-text approach he favours is his own project's. The comparison is n=1, wall-clock, mixing a
local SQLite file with network calls; one store and one mode were never run. mem0's first result has no
number — he says only "very fast" and "a slightly longer time than SQLite", and none has been invented.
"The memory is the asset" is a compression of 12:13–12:24 rather than a sentence he speaks, and his actual
words make it conditional on maintaining the memories. Late in the video he names the wrong guest for the
chili-oil spill (the seeded fact attributes it to Jensen Huang); that line is neither quoted nor repeated,
and the one place it undermines his reading of the graph is flagged in section 8.

Note on presentation: this explainer carries its own accent palette (teal on a cool paper) while keeping
the house component vocabulary and layout rules. See
[Design system](../../../README.md#design-system).
