# Adding to this knowledge base

Everything here follows one shape, deliberately: once you have read one entry, the next one is faster
to read. This document is the recipe. It takes about ten minutes to follow and saves the reader an
hour.

---

## Before you start: is it worth an entry?

Not every good link deserves one. An entry costs real effort, and a library of half-digested material
is worse than a short one. Add it if you can answer **yes** to at least two:

- It changed how you think about building agents, not just what you know about them.
- It contains something concrete — a real failure, real numbers, a mechanism explained properly —
  rather than a survey of what everyone already says.
- You would send it to a colleague and want them to actually finish it.
- The original is hard to consume as-is: a dense 40-minute talk, a paper with the good part buried in
  section 5.

If it is a good link but not entry-material, add it to the **Wanted** or **Threads worth following**
section of the relevant topic README instead.

---

## The seven steps

### 1. Pick the topic

Exactly one of the folders in [`topics/`](topics/). Choose by what the material is *fundamentally*
about, not what it mentions. A talk about evaluating a multi-agent system belongs in
`evaluation-and-observability`, however much architecture it contains.

Read the target topic's `README.md` — each states its own scope and what it explicitly excludes.

### 2. Choose a slug

The folder name, and permanently part of the URL. So:

- kebab-case, lowercase, ASCII only
- two to four words — the memorable part of the title, not the whole thing
- no dates, no author names, no language suffix, no `-v2`

```
✅  learning-on-the-job          ✅  reward-hacking-in-practice
❌  learning_on_the_job_2026     ❌  feng-post-training-talk-en-final
```

### 3. Create the folder

```bash
mkdir -p topics/<topic>/<slug>
cp templates/explainer-template.html topics/<topic>/<slug>/index.html
cp templates/entry-readme-template.md topics/<topic>/<slug>/README.md
```

The explainer **must** be named `index.html`. That is what gives it a clean URL on GitHub Pages
(`…/topics/<topic>/<slug>/` with no `.html` and no filename showing).

### 4. Write the explainer

Fill in `index.html`. The template carries the shared design system and a commented block for every
component. Two hard rules:

- **Self-contained.** No external CSS, JS, fonts, or images — inline everything. An entry has to open
  correctly from a local file, from GitHub Pages, and from an email attachment, offline, in five years.
- **Diagrams are hand-written inline `<svg>`, never screenshots.** They stay sharp at any size, remain
  text-searchable, and avoid redistributing someone else's slide artwork. Label them as
  reconstructions in the caption.

Do not edit the `:root` palette. Add new component classes if you need them; don't redefine the colours.

### 5. Write the entry README

Fill in `README.md`. The YAML front matter is the machine-readable record of the entry — a generated
catalog will eventually read it, so keep it valid. Field-by-field reference:
[README.md → Front-matter reference](README.md#front-matter-reference).

The prose below the front matter is a **briefing**, not a duplicate summary. Its job is to let someone
decide in ninety seconds whether to spend twenty minutes on the explainer.

Set `status: draft` while you work; flip to `published` when it is ready.

### 6. Wire up the three indexes

A new entry has to be linked from four places or nobody will find it:

| File | What to add |
| --- | --- |
| `topics/<topic>/README.md` | A row in that topic's **Entries** table |
| `topics/README.md` | Increment the topic's entry count |
| `README.md` (root) | A row in the **Catalog** table, the topic's count in the **Topics** table, and the `entries` / `updated` badges at the top |
| `index.html` (root) | An `<article class="entry">` card, a filter button if the topic is new, the topic card's count, and the header chips |

### 7. Check it before committing

```bash
python -m http.server 8000
```

Then open <http://localhost:8000/> and walk the checklist below. Opening the file directly with
`file://` also works, but the local server matches how GitHub Pages will serve it, so relative links
behave the same.

---

## Pre-commit checklist

**The explainer**

- [ ] Named `index.html`, inside `topics/<topic>/<slug>/`
- [ ] No external requests — search the file for `http` and confirm every hit is a *content* link, not
      an asset (`<link>`, `<script src>`, `<img src>`, `@font-face`, `url(`)
- [ ] Every diagram is inline SVG and captioned as a reconstruction
- [ ] TL;DR present, and complete enough to stand alone
- [ ] Source box present, with author, venue, date and canonical URL
- [ ] Provenance note explains how the summary was produced
- [ ] Readable at 375px wide (open your browser's device toolbar and check the tables and SVGs)

**The entry README**

- [ ] Front matter is valid YAML, `title` is quoted, `tags` is a list
- [ ] `topic` matches the folder it sits in
- [ ] `slug` matches the folder name
- [ ] `source_published` is the original's date; `added` is today
- [ ] `status: published`
- [ ] Tags reuse existing vocabulary where one already fits

**The indexes**

- [ ] Row added to the topic README
- [ ] Count bumped in `topics/README.md`
- [ ] Root `README.md`: catalog row added, topic count bumped, `entries` and `updated` badges refreshed
- [ ] Root `index.html`: entry card added, filter button present for the topic, topic-card count and
      header chips refreshed

---

## Conventions worth knowing

**Tags.** Four to eight, kebab-case. Reuse before you invent — grep the existing entries first. Tags
are for cross-cutting themes that don't deserve their own topic (`grpo`, `reward-hacking`, `mcp`,
`cost`); the topic folder already carries the primary categorisation.

**Translations.** The default `index.html` is English. An Indonesian version goes next to it as
`index.id.html`, linked from both the explainer header and the entry README. The folder slug never
changes, and never carries a language suffix.

**Sources you cannot link publicly.** Don't add the entry. This repository is public and every claim in
it has to be checkable against something a reader can open.

**Quoting.** Verbatim quotes go in `.quote` blocks with attribution and a timestamp or page number.
Anything reconstructed or paraphrased must say so — the existing entry uses
`— paraphrase of …'s argument, around 9:24`. Keep quotes short; the value here is the synthesis, not
the excerpt.

**Being wrong.** If you later find an entry misrepresents its source, fix it and note the correction in
the entry's Provenance section. A knowledge base that quietly rewrites itself is not trustworthy.

---

## Attribution

The summaries, prose and diagrams in this repository are original work. **The ideas belong to the
original authors**, who must be credited by name, organisation, venue and link on every entry — in the
explainer's source box *and* in the entry README's front matter. This is not optional politeness; it is
the thing that makes the repository legitimate.
