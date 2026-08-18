<div align="center">

# sharing-knowledge

**A working library on AI agentic systems.**

Talks, papers and engineering write-ups — read properly, then rebuilt as
self-contained HTML explainers you can actually finish.

[![Entries](https://img.shields.io/badge/entries-5-E8511F?style=flat-square)](#catalog)
[![Topics](https://img.shields.io/badge/topics-7-2B2622?style=flat-square)](#topics)
[![Format](https://img.shields.io/badge/format-self--contained%20HTML-5A5049?style=flat-square)](#anatomy-of-an-entry)
[![Updated](https://img.shields.io/badge/updated-2026--08--18-1B8A54?style=flat-square)](#catalog)

**📖 [Read online → aicaruss.github.io/sharing-knowledge](https://aicaruss.github.io/sharing-knowledge/)**

<sub>_(the live site needs GitHub Pages switched on once — see [Publishing](#publishing-with-github-pages))_</sub>

</div>

---

## Contents

- [Why this exists](#why-this-exists)
- [Anatomy of an entry](#anatomy-of-an-entry)
- [Catalog](#catalog)
- [Topics](#topics)
- [Repository structure](#repository-structure)
- [Reading the material](#reading-the-material)
- [Adding an entry](#adding-an-entry)
- [Conventions](#conventions)
  - [Naming](#naming)
  - [Front-matter reference](#front-matter-reference)
  - [Tags](#tags)
  - [Translations](#translations)
  - [Design system](#design-system)
- [Editorial principles](#editorial-principles)
- [Publishing with GitHub Pages](#publishing-with-github-pages)
- [Roadmap](#roadmap)
- [Attribution & reuse](#attribution--reuse)

---

## Why this exists

The material on agentic AI is good and there is far too much of it. A 40-minute conference talk holds
maybe six ideas worth keeping; a paper often hides the interesting part in section five. Bookmarking it
does nothing — three months later you remember that something important was said, but not what.

So this repository does the expensive part once. Each source gets read end to end, and the argument is
rewritten as **one self-contained HTML page**: a TL;DR that stands on its own, the vocabulary you need
before you need it, diagrams redrawn as inline SVG, and deep links back to the original so you can
verify anything.

Three consequences of that choice, all deliberate:

- **One file, no dependencies.** An entry opens from a local disk, from the web, or from an email
  attachment — offline, on a phone, in five years. No build step, no framework, no CDN that can vanish.
- **A summary, never a replacement.** Every entry names its source loudly and is built to send you
  there better prepared. Where the source says "we don't know yet", the explainer says so too.
- **Structure over volume.** Seven topics, one obvious home per entry, and a fixed shape for every
  page. Reading the second entry is faster than reading the first.

---

## Anatomy of an entry

An entry is a folder. It always contains exactly two files:

```
topics/post-training/learning-on-the-job/
├── index.html     the explainer — self-contained, opens in any browser
└── README.md      YAML metadata + a briefing that helps you decide whether to read it
```

**`index.html`** is the artifact. It follows a fixed shape:

| Part | What it does |
| --- | --- |
| **Header** | Title, author, venue, runtime, a prominent link to the source, topic chips |
| **TL;DR** | The whole argument in 5–7 numbered points. Stop here and you still have the thesis |
| **Vocabulary** | The handful of terms the source leans on, defined in *its* sense, before it uses them |
| **Body** | Section by section, with the reasoning attached — not just the conclusions |
| **Figures** | Hand-written inline SVG reconstructions of the source's diagrams. Never screenshots |
| **Callouts** | Key point, failure mode, analogy, verbatim quote — each with its own visual treatment |
| **Synthesis table** | One table that lets you compare everything at a glance. Usually the most re-read part |
| **Navigation index** | Deep-linked timestamps for talks, section references for papers |
| **Source box** | Full attribution, canonical URL, and related work the source cites |
| **Provenance note** | How the summary was produced, and which parts are reconstructed |

**`README.md`** is the briefing: front matter that machines can read, then *why this is in the
knowledge base*, the argument in one paragraph, key takeaways, concepts introduced, what remains
unresolved, and provenance. Its job is to let you decide in ninety seconds whether the explainer earns
twenty minutes.

Named `index.html` on purpose: GitHub Pages then serves the entry at a clean
`…/topics/<topic>/<slug>/` — no `.html`, no filename.

---

## Catalog

| # | Entry | Topic | Source | Format | Added |
| :--: | --- | --- | --- | --- | --- |
| 01 | **[Learning on the Job: The Future of Post-Training](topics/post-training/learning-on-the-job/)**<br><sub>Post-training as a school ladder — single-turn Q&A → simulated environments → an "internship" inside the customer's real harness → self-improvement. Why simulated environments breed reward hacking (two candid failures from their own runs), and what "Bring Your Own Harness" costs once data stops being replayable and GRPO no longer applies.</sub><br><sub>[📄 notes](topics/post-training/learning-on-the-job/README.md) · [📖 read](https://aicaruss.github.io/sharing-knowledge/topics/post-training/learning-on-the-job/) · [↗ source](https://www.youtube.com/watch?v=k35LeKZEhiE)</sub> | `post-training` | Raymond Feng<br><sub>Applied Compute · AI Engineer World's Fair 2026</sub> | Talk explainer<br><sub>18m20s</sub> | 2026-08-06 |
| 02 | **[Loop Engineering vs Graph Engineering](topics/agent-architecture/loop-vs-graph/)**<br><sub>Two buzzwords, taken slowly. The five-rung ladder — prompt → context → skills → loop → graph — where each rung exists because the one below ran out of road. Loops and graphs aren't competitors: a graph wraps loops, buys speed and predictability rather than intelligence, and needs guardrails precisely because its nodes and routing stopped being deterministic.</sub><br><sub>[📄 notes](topics/agent-architecture/loop-vs-graph/README.md) · [📖 read](https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/loop-vs-graph/) · [↗ source](https://www.youtube.com/watch?v=IMLwvK08JVc)</sub> | `agent-architecture` | Shen Sean Chen<br><sub>Sean's AI Stories</sub> | Talk explainer<br><sub>21m31s</sub> | 2026-08-11 |
| 03 | **[From Signal to PR: Anatomy of a Self-Improving Agent](topics/evaluation-and-observability/signal-to-pr/)**<br><sub>Observability stops being a dashboard you click and becomes machine input. The unlock is deliberately unglamorous — production traces written into the repo as files, because harnesses are magical with files and hopeless with a dashboard. The loop inverts (agent digs, you review), and so you should now log ten times more, not less.</sub><br><sub>[📄 notes](topics/evaluation-and-observability/signal-to-pr/README.md) · [📖 read](https://aicaruss.github.io/sharing-knowledge/topics/evaluation-and-observability/signal-to-pr/) · [↗ source](https://www.youtube.com/watch?v=9HbzAWnKbo4)</sub> | `evaluation-and-observability` | Jason Lopatecki<br><sub>Arize AI</sub> | Talk explainer<br><sub>20m35s</sub> | 2026-08-11 |
| 04 | **[Verification Debt: Guide, Verify, Solve](topics/evaluation-and-observability/verification-debt/)**<br><sub>The productivity spike from AI coding tools expires in about three months; the static-analysis warnings and complexity it leaves behind do not. That residue is verification debt, and it scales with criticality — an agent's default quality is flat while the quality a project needs rises. Human review is a leaky backstop: people follow confidently wrong AI advice 79.8% of the time. The criterion worth keeping: verify with a *different* methodology than the one that generated the code, because a model grading its own output inherits its own blind spots. A vendor talk, and the entry says so.</sub><br><sub>[📄 notes](topics/evaluation-and-observability/verification-debt/README.md) · [📖 read](https://aicaruss.github.io/sharing-knowledge/topics/evaluation-and-observability/verification-debt/) · [↗ source](https://www.youtube.com/watch?v=03l29gJXpCE)</sub> | `evaluation-and-observability` | Anirban Chatterjee<br><sub>Sonar · AI Engineer World's Fair 2026</sub> | Talk explainer<br><sub>22m31s</sub> | 2026-08-11 |
| 05 | **[Memory Layers for AI Agents](topics/agent-architecture/memory-layers/)**<br><sub>Every LLM call starts with amnesia — what makes ChatGPT or Claude seem to remember you is a memory system somebody built around the model, not the model. Three pillars: what a memory *is* (text, table, graph), how the agent *finds* it (do nothing, keyword, RAG, Graph RAG), and how you *keep it true* (retire rather than delete, attribute, reflect). Then four real stores raced on identical facts against a no-memory control that passes by correctly reporting ignorance. An n=1 benchmark by the author of the harness it runs in — the entry says so.</sub><br><sub>[📄 notes](topics/agent-architecture/memory-layers/README.md) · [📖 read](https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/memory-layers/) · [🇮🇩 versi Indonesia](https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/memory-layers/index.id.html) · [↗ source](https://www.youtube.com/watch?v=072eNztI06k)</sub> | `agent-architecture` | Shen Sean Chen<br><sub>Sean's AI Stories</sub> | Talk explainer<br><sub>30m26s</sub> | 2026-08-18 |

---

## Topics

Seven topics, chosen so that every entry has exactly one obvious home. Each folder documents its own
scope — including what it deliberately excludes — and keeps a list of open threads worth researching.

| Topic | What lands here | Entries |
| --- | --- | :--: |
| [**post-training**](topics/post-training/) | RL, fine-tuning, reward design, training environments, custom models | 1 |
| [**agent-architecture**](topics/agent-architecture/) | The agent loop, planning, memory, multi-agent topologies | 2 |
| [**tool-use-and-protocols**](topics/tool-use-and-protocols/) | Function calling, MCP, computer use, agent-to-agent protocols | 0 |
| [**context-engineering**](topics/context-engineering/) | Prompting, RAG, retrieval, context-window budgeting | 0 |
| [**evaluation-and-observability**](topics/evaluation-and-observability/) | Evals, benchmarks, tracing, guardrails, cost accounting | 2 |
| [**infrastructure**](topics/infrastructure/) | Serving, inference, sandboxes, latency and cost | 0 |
| [**applied-and-case-studies**](topics/applied-and-case-studies/) | Real deployments, post-mortems, enterprise patterns | 0 |

Pick by what the material is *fundamentally* about, not what it mentions in passing. A talk about
evaluating a multi-agent system is `evaluation-and-observability`, however much architecture it
contains. If two topics genuinely fit, file it where a reader would look first and cross-link from the
other. An eighth topic is allowed but should be rare — prefer a [tag](#tags).

---

## Repository structure

```
sharing-knowledge/
│
├── index.html                            catalog landing page — the GitHub Pages entry point
├── README.md                             you are here
├── CONTRIBUTING.md                       how to add an entry, with a pre-commit checklist
├── .nojekyll                             tells GitHub Pages to serve files verbatim
│
├── templates/
│   ├── explainer-template.html           skeleton carrying the shared design system
│   └── entry-readme-template.md          skeleton for front matter + briefing
│
└── topics/
    ├── README.md                         the taxonomy, and how to choose between topics
    │
    ├── post-training/
    │   ├── README.md                     topic scope · entry table · open threads
    │   └── learning-on-the-job/
    │       ├── index.html                ← the explainer
    │       └── README.md                 ← metadata + briefing
    │
    ├── agent-architecture/
    │   ├── README.md
    │   └── loop-vs-graph/
    │       ├── index.html
    │       └── README.md
    │
    ├── evaluation-and-observability/
    │   ├── README.md
    │   └── signal-to-pr/
    │       ├── index.html
    │       └── README.md
    │
    ├── tool-use-and-protocols/
    │   └── README.md
    ├── context-engineering/
    │   └── README.md
    ├── infrastructure/
    │   └── README.md
    └── applied-and-case-studies/
        └── README.md
```

Three levels, and that is the ceiling: `topics/` → topic → entry. Nothing nests deeper. If an entry
ever needs supporting files, they go in an `assets/` folder inside that entry — never shared across
entries, because shared assets are how self-contained pages stop being self-contained.

---

## Reading the material

**Online** — the published site is the nicest way:

<https://aicaruss.github.io/sharing-knowledge/>

**Locally** — clone, then serve the folder:

```bash
git clone https://github.com/aicaruss/sharing-knowledge.git
```

```bash
cd sharing-knowledge && python -m http.server 8000
```

Open <http://localhost:8000/>. A local server is worth the extra step because it resolves relative
links exactly the way GitHub Pages will.

**Straight from disk** — double-clicking any `index.html` works too. The pages have no external
dependencies, so they render identically over `file://`.

> **Note:** viewing an entry through GitHub's own file browser shows you HTML *source*, not the page.
> Use the published site, or clone the repository.

---

## Adding an entry

The short version:

```bash
mkdir -p topics/<topic>/<slug>
cp templates/explainer-template.html topics/<topic>/<slug>/index.html
cp templates/entry-readme-template.md topics/<topic>/<slug>/README.md
```

Write the explainer, fill in the front matter, then link it from the four indexes (topic README, topics
README count, root README catalog, root `index.html` card).

**The full recipe, including a pre-commit checklist, is in [CONTRIBUTING.md](CONTRIBUTING.md)** — start
there. It also covers the question worth asking first: whether the source deserves an entry at all, or
just a line in a topic's "wanted" list.

---

## Conventions

### Naming

| Thing | Rule | Example |
| --- | --- | --- |
| Topic folder | kebab-case, plural or compound noun, from the fixed set of seven | `tool-use-and-protocols` |
| Entry folder (slug) | kebab-case, 2–4 words, the memorable part of the title | `learning-on-the-job` |
| Explainer file | always `index.html` | `index.html` |
| Translation | `index.<lang>.html` beside it | `index.id.html` |
| Entry metadata | always `README.md` | `README.md` |

Slugs are permanent — they are part of every URL that gets shared. No dates, no author names, no
language suffix, no `-v2`, no `-final`.

### Front-matter reference

Every entry `README.md` opens with YAML front matter. It is the machine-readable record of the entry;
a generated catalog will eventually read it, so keep it valid.

| Field | Required | Description |
| --- | :--: | --- |
| `title` | ✔ | Full title, quoted. Matches the `<h1>` of `index.html` |
| `slug` | ✔ | Folder name. Must match the directory it sits in |
| `topic` | ✔ | Exactly one of the seven topic folder names |
| `type` | ✔ | `talk-explainer` · `paper-explainer` · `article-explainer` · `primer` · `case-study` · `notes` |
| `language` | ✔ | Language of `index.html`. `en` unless stated otherwise |
| `status` | ✔ | `draft` while in progress, `published` when ready |
| `added` | ✔ | ISO date the entry landed in this repository |
| `source_type` | ✔ | `conference-talk` · `paper` · `blog-post` · `documentation` · `podcast` · `book-chapter` |
| `source_title` |  | Original title, if it differs from `title` |
| `source_url` | ✔ | Canonical link. Prefer permanent identifiers (DOI, arXiv abs) over mirrors |
| `source_author` |  | Person or people. Omit the field entirely if genuinely unattributed |
| `source_org` |  | Their affiliation |
| `source_event` |  | Conference, journal or publication |
| `source_published` | ✔* | ISO date the *original* came out — not when you read it. *\*Omit the field entirely if the source material genuinely doesn't state one, and say so in Provenance. Never guess a date.* |
| `source_duration` |  | `18m20s` for talks, `14 pages` for papers. Omit if meaningless |
| `tags` | ✔ | 4–8 kebab-case tags, as a YAML list |

### Tags

Four to eight per entry, kebab-case, and **reuse before you invent** — grep the existing entries first.
Tags carry cross-cutting themes that don't deserve their own topic; the topic folder already handles
primary categorisation.

In use so far — `agent-harness` · `agent-memory` · `agent-skills` · `agentic-harness` · `byoh` ·
`ci-cd` · `code-review` · `dag` · `evals` · `graph-engineering` · `graph-rag` · `grpo` ·
`incident-response` · `llm-as-judge` · `loop-engineering` · `observability` · `orchestration` ·
`parallelism` · `post-training` · `procedural-memory` · `quality-gates` ·
`reinforcement-learning` · `reward-hacking` · `rl-environments` · `sandboxes` ·
`self-improvement` · `self-improving-agents` · `semantic-memory` · `sqlite` ·
`static-analysis` · `traces` · `vector-stores`

> **Cleanup owed.** That list already contains two near-duplicate pairs — `agent-harness` /
> `agentic-harness`, and `self-improvement` / `self-improving-agents`. They came in from different
> entries. Worth consolidating to one of each before the vocabulary grows further.

### Translations

`index.html` is English by default. An Indonesian version lives beside it as `index.id.html`, linked
from both the explainer header and the entry README. The folder slug never changes and never carries a
language suffix — the URL identifies the *entry*, not the language.

### Design system

What is shared across entries is the **structure and the component vocabulary**, not one fixed palette.
[`templates/explainer-template.html`](templates/explainer-template.html) is the house style — a 900px
column, a dark header band, then a predictable set of components:

`.tldr` · `.card` · `.note` · `.note.warn` · `.analogy` · `.quote` · `.tag` · `.chip` ·
`figure > svg` · `.srcbox` · `.dots`

Each entry then carries its **own accent palette**, declared in its own `:root`. That keeps a page
recognisable as part of this library while letting a topic have its own identity:

| Entry | Paper | Accent |
| --- | --- | --- |
| [learning-on-the-job](topics/post-training/learning-on-the-job/) | warm cream `#FDF3E7` | orange `#E8511F` |
| [signal-to-pr](topics/evaluation-and-observability/signal-to-pr/) | cool lilac `#F3F2F9` | violet `#6D4AE0` |
| [loop-vs-graph](topics/agent-architecture/loop-vs-graph/) | off-white `#f9f9f7` | blue `#2a78d6` |
| [verification-debt](topics/evaluation-and-observability/verification-debt/) | pale teal `#F1F5F5` | teal `#0E7C74` |
| [memory-layers](topics/agent-architecture/memory-layers/) | pale teal `#F1F5F4` | teal `#0E7C6B` |

> **This table is a fifth index surface.** It was missed when `verification-debt` shipped and had to be
> backfilled. If you add an entry, it belongs here too — `CONTRIBUTING.md`'s wiring checklist names it.

Two of the three follow the component vocabulary above. **`loop-vs-graph` is the exception** — adapted
from a differently-structured source, it brings its own components (`.hero`, `.ladder`, `.rung`) and is
so far the only entry that supports dark mode via `prefers-color-scheme`. That is allowed: the template
is a starting point, not a cage.

The rules that are **not** negotiable, because the repository's promises depend on them:

1. **Self-contained.** No external CSS, JS, fonts, or images — inline everything.
2. **Diagrams are inline `<svg>`, hand-written.** Never screenshots.
3. **No horizontal overflow at 375px.** Tables and wide figures scroll inside their own container.

Semantic colours stay consistent in diagrams regardless of palette: blue for requests, green for
responses, red for failures and warnings, violet or purple for specs and skills.

---

## Editorial principles

What separates an entry here from a summary you could have generated in one pass:

**Explain the reasoning, not just the conclusion.** "Reward hacking happened" is a fact. "~10% of tool
calls failed from network issues, so the model shortened its responses even though the reward function
had no length penalty — potholes in the sidewalk, so take fewer steps" is understanding.

**Define jargon before it is used.** A vocabulary section costs 200 words and makes the following 3,000
readable. If a term appears in the TL;DR, it should already be defined.

**Redraw the diagrams.** A screenshot of a slide is unsearchable, blurs on a phone, and redistributes
someone else's artwork. Rebuilding it as SVG forces you to actually understand the diagram, which is
the point.

**Keep the source's uncertainty.** When a slide literally reads `OPSD??` with the question marks, that
belongs in the summary. Smoothing away the unresolved parts makes a field report read like a product
pitch, and destroys exactly the information a practitioner needs.

**Separate their words from yours.** Verbatim quotes get quote blocks and timestamps. Paraphrases say
they are paraphrases. Reconstructions say they are reconstructions.

**Be honest when it's thin.** If a source turns out to have less in it than expected, say so in the
entry rather than padding it. A short honest entry is worth more than a long generous one.

---

## Publishing with GitHub Pages

The site is plain static files — no build step, no Actions workflow. Enable it once:

1. Open **Settings → Pages** in the repository.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Set the branch to **`main`** and the folder to **`/ (root)`**, then **Save**.
4. Wait about a minute. The site appears at
   **`https://aicaruss.github.io/sharing-knowledge/`**.

Every push to `main` republishes automatically. The `.nojekyll` file at the root tells Pages to serve
the files verbatim instead of running them through Jekyll — faster, and it removes a whole class of
surprises around underscores and front matter.

---

## Roadmap

Not a promise, just the direction:

- **Fill the empty topics.** Each topic README lists specific gaps under **Wanted** — those are the
  research queue.
- **Follow the open threads.** `post-training` already tracks the biggest one: what replaces GRPO when
  training data isn't replayable.
- **Generate the catalog.** The front matter exists so that the three index tables can eventually be
  produced from the entries rather than hand-maintained.
- **Indonesian translations** for the entries that get shared most.

---

## Attribution & reuse

The summaries, prose, diagrams and page design in this repository are original work.

**All credit for the underlying ideas belongs to the original authors.** Every entry names its source —
author, organisation, venue, date — in the explainer's source box *and* in the entry's front matter,
with a link to the original. No slide imagery or copyrighted figures are redistributed; every diagram
is redrawn from scratch.

If you are the author of a source and want an entry corrected or removed,
[open an issue](https://github.com/aicaruss/sharing-knowledge/issues) — it will be handled quickly.

> **No licence file yet.** Without one, default copyright applies and others cannot reuse this material.
> If you want the summaries to be freely shareable, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
> fits prose and diagrams well; MIT fits the templates. Worth deciding before the repository gets shared
> widely.

---

<div align="center">
<sub>Maintained by <a href="https://github.com/aicaruss">aicaruss</a> · Contributions and corrections welcome via <a href="https://github.com/aicaruss/sharing-knowledge/issues">issues</a></sub>
</div>
