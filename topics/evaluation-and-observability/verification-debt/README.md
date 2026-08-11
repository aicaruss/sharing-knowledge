---
title: "Verification Debt: Guide, Verify, Solve"
slug: verification-debt
topic: evaluation-and-observability
type: talk-explainer
language: en
status: published
added: 2026-08-11
source_type: conference-talk
source_title: "Guide, Verify, Solve"
source_url: https://www.youtube.com/watch?v=03l29gJXpCE
source_author: Anirban Chatterjee
source_org: Sonar
source_event: "AI Engineer World's Fair 2026 — Track 8: Agentic Engineering (delivered 2026-07-02)"
source_published: 2026-08-09
source_duration: 22m31s
tags:
  - evals
  - llm-as-judge
  - static-analysis
  - code-review
  - quality-gates
  - ci-cd
---

# Verification Debt: Guide, Verify, Solve

**[▶ Open the explainer](index.html)** · [Watch the source talk ↗](https://www.youtube.com/watch?v=03l29gJXpCE)

> Reading online? → <https://aicaruss.github.io/sharing-knowledge/topics/evaluation-and-observability/verification-debt/>

---

## Why this is in the knowledge base

Most of the material in this collection is about making agents produce more. This one is about deciding
whether what they produced is good enough to ship — and it carries the one criterion that reframes the
question: **verify with a different methodology than the one that generated the code**. That single
line rules out the reflex most teams reach for first ("have the model review its own PR") and it
generalises well beyond code.

It also brings two citable studies. The Carnegie Mellon difference-in-differences result — the
productivity spike fades in about three months while static-analysis warnings and complexity persist —
is the closest thing here to a measured account of what AI-assisted coding costs later. The Wharton
figure (people follow confidently wrong AI advice 79.8% of the time) puts a number on the assumption
that a human reviewer is an adequate backstop.

**Read it with the disclosure in view.** This is a vendor talk: the speaker is in product marketing at
Sonar, and about six of the twenty-two minutes are a catalogue of Sonar products. The explainer says so
once, covers the fourteen or so minutes of transferable argument, and does not reproduce the catalogue.

## In one paragraph

AI coding tools buy you a productivity spike that expires while the static-analysis warnings and
complexity they introduce do not, which leaves a standing shortfall the speaker calls *verification
debt*. That debt is not the same size for every project: an agent's default quality is roughly flat
while the quality a project *needs* rises with its criticality, so the gap — and the amount of
verification worth buying — is set by where the software sits on that axis. Human review does not close
the gap reliably, because people follow confidently wrong AI advice about four times in five, and
because software, unlike code, is not provable in the first place. The proposed answer is automated
verification that is *zero trust* (works the same regardless of who wrote the code, and uses a different
methodology than the one that generated it) and *multilayered* (computational plus reasoning-based
review, each layer required to have very low false positives). Structurally, that check runs **twice** —
inside the generation loop so defects do not propagate into later loops, and again in CI, where a
failing quality gate routes to a fix agent rather than to a person.

## Key takeaways

1. **The productivity gain and the quality cost run on different clocks.** The CMU study found commits
   and lines-added flat while warnings, duplication and complexity climbed persistently after adoption.
   A three-month spike against a permanent overhead is a bad trade nobody measured at the time.
2. **Size verification by criticality, not by policy.** The gap between default and needed quality is
   small for a short-lived internal tool with friendly users and large for a long-lived large codebase
   with adversarial ones. One gate for both wastes money at one end and gives false comfort at the other.
3. **Zero trust means a different instrument, not a stricter one.** A check is only evidence to the
   extent that the checker can fail in ways the writer cannot. This is the criterion worth stealing, and
   it quietly indicts "second agent reviews the first agent".
4. **Layering is bounded by its noisiest layer.** The slide — never spoken aloud — requires every
   approach to have very low false positives and high true positives. Without that, stacking checks just
   manufactures alerts people learn to click past, which recreates the rubber-stamping problem.
5. **Human review is a filter that lets roughly four wrong answers in five through.** 92.7% compliance
   when the AI was right, 79.8% when it was deliberately wrong. Thirteen points of scepticism.
6. **Verification appears twice in the architecture, for two different reasons.** In-loop, so a defect
   generated in loop three does not become context for loops four through twenty. In CI, as the
   pass/fail that stands between the loop and production.
7. **A failing gate routes to a fix agent, not a person.** That keeps the loop closed — and removes the
   human whose review the Wharton result just discredited. Elegant or circular depending on how much you
   trust the gate.

## Concepts you will pick up

| Term | Why it matters here |
| --- | --- |
| **Verification debt** | The distance between an agent's default quality and the quality the application needs. Work somebody does before shipping, whether or not it was budgeted. |
| **Zero trust verification** | Check the code identically regardless of provenance, using a *different methodology* than the one that generated it. The load-bearing idea in the talk. |
| **Multilayered verification** | Independent techniques stacked, each required to have very low false positives. Computational review plus reasoning-based review, plus *runtime* on one slide. |
| **In-loop verification** | The check running while the agent generates, so defects are contained before they become context for the next loop. |
| **Quality gate** | The pass/fail against written-down acceptance criteria in CI. The only thing between the loop and production. |
| **ACDC** | Sonar's label for the loop shape — Agent Centric Development Cycle: Guide, Verify, Solve around Generate. Report the shape, discount the name. |

## Why it lands in `evaluation-and-observability`

The subject is how you decide whether machine-written output is good enough: acceptance criteria,
layered checking, pass/fail gates. That is evaluation. It touches
[`agent-architecture`](../../agent-architecture/) (the loop shape) and infrastructure (CI/CD placement),
but the load-bearing question is *how do you know this output is good enough*.

## Still open, and where to be sceptical

- **Cost is never mentioned.** *My objection.* Computational plus reasoning-based verification on every
  inner-loop iteration has a token bill and a latency cost; neither is quantified. This is the same
  silence [signal-to-pr](../signal-to-pr/) has around "trace 10× more".
- **"Different methodology" is under-defined.** *My objection.* Static analysis versus an LLM is clearly
  a different methodology. Model A reviewing model B's code is much less clearly so — two frontier
  models trained on overlapping data are not independent instruments. The best idea in the talk needs a
  sharper test than the talk gives it.
- **The leap from Wharton to code review is his, not the study's.** The study measured following AI
  advice in general. Applying 79.8% to pull-request review is an analogy, presented with more confidence
  than the evidence carries. His supporting claim — *"there's a lot of rubber stamping that I'm sure is
  happening in all of your organizations"* — is asserted, not measured.
- **Who writes the acceptance criteria, and how do you know they are right?** *My objection.* The gate
  depends entirely on criteria fixed in advance. The talk says define them, and that defaults ship with
  the product. It never asks what happens when yours are wrong in the permissive direction.
- **The CMU study's instrument is the speaker's own product.** Stated openly on the slide and aloud, but
  worth carrying forward: the metric that shows the damage is the metric his employer sells.
- **He runs out of time three times**, each time with substantive material left uncovered — *"I'm going
  to move past this cuz I'm out of time now"* (20:10).
- **The closing ask is a purchase.** The final takeaway is to *"standardize on a single independent
  multi-layered verification platform ... across all projects, across all teams, across all developers,
  and all AI coding tools"* (21:47). Consistency is a real engineering argument and it is also, exactly,
  a request to buy one vendor's product. Both are true at once.

## Also referenced in the source

Both papers are fully citable from the slides even though the speaker never reads the citations aloud.

- **"Does AI-Assisted Coding Deliver? A Difference-in-Differences Study of Cursor's Impact on Software
  Projects"** — Carnegie Mellon. Five outcomes measured −6 to +6 months around Cursor adoption; code
  quality data collected with **SonarQube**, the speaker's own company's product.
- **Shaw & Nave (2026), Wharton — "Thinking Fast, Slow, and Artificial."** Participants followed AI
  advice 92.7% of the time when it was correct and 79.8% when it was wrong. The slide's pull quote
  distinguishes *cognitive offloading* from *cognitive surrender*; the quotation's own source is not
  visible in the captured frame.

Not from a slide, but worth recording:

- **Sonar's own leaderboard** — 4,000+ coding tasks per model, scored on correctness, unsolved tasks,
  security, reliability, maintainability and complexity. The slide is titled "Models have diverse
  quality issues" and its footer carries only the bare URL `sonar.com/leaderboard`; aloud he calls it
  "the LLM leaderboard" (4:59). The report title **"The Coding Personalities of Leading LLMs"** comes
  from the page linked in the video description, not from any slide.

## Related entries

- [**From Signal to PR: Anatomy of a Self-Improving Agent**](../signal-to-pr/) — same topic, opposite
  ends of the lifecycle: this one gates code *before* it ships, that one repairs it *after*, from
  production traces. Both are talks by people with a commercial interest in the conclusion, which is
  worth noticing as a pattern rather than a coincidence.
- [**Loop Engineering vs Graph Engineering**](../../agent-architecture/loop-vs-graph/) — a **partial
  answer to its open question**. That entry establishes that a non-deterministic flow needs guardrails
  and then stops short of designing them. This talk supplies a concrete shape: verify with a different
  method than the one that generated, layer computational review with reasoning review, and run the
  check inside the inner loop so defects do not propagate.
- [**Learning on the Job: The Future of Post-Training**](../../post-training/learning-on-the-job/) —
  the same fair, one day earlier (Track 9; this one is Track 8, 2 July 2026). A clean contrast
  in how each closes the improvement loop: that talk updates *model weights* from graded production
  traces; this one leaves the weights alone and puts a *deterministic gate* in front of the output.

## Provenance

Compiled from the **yt-dlp auto-generated (ASR) English transcript** — 340 merged segments spanning
0:01–22:29 — plus factual descriptions of **8 slide frames** captured from the video for reference. No
screenshot is stored or redistributed. **All three figures in the explainer are hand-drawn inline SVG
reconstructions** built from those frame descriptions, and each caption states what was changed.
Figure 3 in particular removes the vendor product names the original printed against individual nodes,
and re-lays the two loops from side-by-side to stacked; the node wording is unchanged, and the one
inferred piece of topology — where the in-loop **Fail** edge returns to — is disclosed in its caption.

Four sourcing caveats. **(1)** The transcript is machine-generated and garbles proper nouns — SonarQube
as "SonarCube", Antigravity as "Any Gravity" (19:50), the acquired company inconsistently — so **no
proper noun is quoted on the strength of the transcript alone**. Every product, model and paper name
used is corroborated by a slide, with two exceptions, both named as such: the leaderboard report's
title, attributed above to the video description, and **Antigravity** in this sentence, which rests on
the transcript alone. The acquired company is left unnamed because the transcript and the frame
descriptions disagree on its spelling. **(2)** Quoted timestamps are the start of the transcript segment
containing the quote and are accurate to a few seconds. **(3)** `source_event` is inferred from the
on-slide track branding ("TRACK 8 • JULY 2, 2026 / Agentic Engineering") plus the speaker's references
to a keynote "yesterday"; the video metadata does not state it. Note the two dates: `source_published`
is the **video** date, 2026-08-09, while the talk itself was delivered 2026-07-02. **(4)** Two things in
the source could not be reported fully — the leaderboard radar shows a pair of numbers per axis that
cannot be assigned to a model at the captured resolution, and on the quality-gap slide the enterprise
anchor's line count reads as roughly 500K LOCs but its comparison operator is not legible, so the figure
is described rather than quoted. Both gaps are marked in the explainer where they occur rather than
filled in.
