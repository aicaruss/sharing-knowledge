<!--
  ENTRY README TEMPLATE — sharing-knowledge
  Copy to  topics/<topic>/<slug>/README.md  and fill in.
  Keep the YAML front matter valid: it is the machine-readable record of the
  entry and a generated catalog will eventually read it. Field reference:
  ../README.md#front-matter-reference
  Delete these comments when you're done.
-->
---
title: ""                     # Full title, in quotes. Matches the <h1> of index.html.
slug: ""                      # Folder name. kebab-case, short, no dates, no language suffix.
topic: ""                     # Exactly one of the seven folder names under topics/.
type: ""                      # talk-explainer | paper-explainer | article-explainer | primer | case-study | notes
language: en                  # Language of index.html. Translations get their own field entry below.
status: draft                 # draft | published
added: YYYY-MM-DD             # Date this entry landed in the repo.
source_type: ""               # conference-talk | paper | blog-post | documentation | podcast | book-chapter
source_title: ""              # Original title, if it differs from `title`.
source_url: ""                # Canonical link. Permanent one where possible (DOI, arXiv abs, not a mirror).
source_author: ""             # Person or people. Omit the field entirely if genuinely unattributed.
source_org: ""                # Their affiliation.
source_event: ""              # Conference, journal, or publication. Omit if not applicable.
source_published: YYYY-MM-DD  # When the original came out — not when you read it.
source_duration: ""           # e.g. 18m20s for talks, "14 pages" for papers. Omit if meaningless.
tags: []                      # 4–8 kebab-case tags. Reuse existing ones before inventing new ones.
---

# {{Title}}

**[▶ Open the explainer](index.html)** · [{{Watch/read the source}} ↗]({{SOURCE_URL}})

> Reading online? → <https://aicaruss.github.io/sharing-knowledge/topics/{{topic}}/{{slug}}/>

---

## Why this is in the knowledge base

{{Two short paragraphs. Not a summary — a justification. What does this source do that the material
already here does not? Why should someone spend twenty minutes on it? If you can't answer that
convincingly, the entry probably shouldn't exist.}}

## In one paragraph

{{The entire argument, compressed to 4–6 sentences. Someone who reads only this should be able to
repeat the thesis correctly in a meeting.}}

## Key takeaways

{{4–7 numbered items. Each one a claim with its reasoning attached, not a topic label. "Replayability
is the hidden load-bearing assumption — GRPO compares rollouts of the same task from the same initial
state, and a real customer conversation cannot be reset" beats "discusses replayability".}}

1. **{{Claim.}}** {{Why it holds.}}
2. **{{Claim.}}** {{Why it holds.}}
3. **{{Claim.}}** {{Why it holds.}}

## Concepts you will pick up

| Term | Why it matters here |
| --- | --- |
| **{{Term}}** | {{Its role in this specific argument.}} |
| **{{Term}}** | {{Its role in this specific argument.}} |

## Still open

{{What the source does not settle. Be specific and fair — distinguish "the author says this is
unsolved" from "I think this is a weak point". Delete the section if the source really is complete.}}

- **{{Open question}}** — {{state of play.}}

## Also referenced in the source

{{Papers, talks, or posts the source builds on, with enough detail to find them. These often become
future entries.}}

- {{Title}} — {{author, venue, identifier, date}}.

## Related entries

{{Links to other entries in this repo, with one line on how they connect. Write `_None yet._` and list
candidate future entries if this is the first of its kind.}}

## Provenance

{{How the explainer was produced: transcript, paper text, slide captures. State explicitly that figures
are redrawn reconstructions rather than screenshots, and note anything you inferred or reconstructed
rather than took verbatim. Readers deserve to know which parts are the source's words and which are
yours.}}
