---
title: "From Signal to PR: Anatomy of a Self-Improving Agent"
slug: signal-to-pr
topic: evaluation-and-observability
type: talk-explainer
language: en
status: published
added: 2026-08-11
source_type: conference-talk
source_url: https://www.youtube.com/watch?v=9HbzAWnKbo4
source_author: Jason Lopatecki
source_org: Arize AI
source_event: "AI Engineer (talk)"
source_published: 2026-07-24
source_duration: 20m35s
tags:
  - observability
  - traces
  - evals
  - agent-skills
  - sandboxes
  - self-improving-agents
  - llm-as-judge
  - incident-response
---

# From Signal to PR: Anatomy of a Self-Improving Agent

**[▶ Open the explainer](index.html)** · [Watch the source talk ↗](https://www.youtube.com/watch?v=9HbzAWnKbo4)

> Reading online? → <https://aicaruss.github.io/sharing-knowledge/topics/evaluation-and-observability/signal-to-pr/>

---

## Why this is in the knowledge base

Most observability material is about instrumenting systems for people to look at. This talk argues the
audience has changed: telemetry is becoming **machine input**, and once you accept that, several
long-standing engineering habits invert — including the rule that you should log less to reduce noise.

It also happens to contain the least glamorous good idea in this collection. The mechanism that makes
the whole thing work is not a model or an algorithm: it is **writing production traces to disk as files
inside the repo**, because coding harnesses are excellent with files and useless with a dashboard.
That is a thing you could implement next week.

It earns its place partly by being honest. The speaker's own first agent, in his words, *"frankly
sucked"*, and he is explicit that what is solved here is the **cold start**, not autonomy.

## In one paragraph

Software got dramatically faster to write, but diagnosing and repairing it in production did not — and
that gap is the problem. The fix is to invert who moves first: instead of an alert waking you up so you
can start digging, a trigger wakes an *agent*, which pulls the relevant traces and logs into the repo as
files, reads them alongside the code, and leaves you an issue with evidence attached or a pull request
to review. Traces are the substrate rather than dashboards because a trace records **which path the code
actually took**, and without that the agent is guessing among a million branches. Evals layer on top as
pre-processed judgement attached to traces, not as a replacement for them. The consequence is
counterintuitive: you should now trace and log an order of magnitude *more*, because the reason to log
less was a human reading constraint that no longer applies.

## Key takeaways

1. **Observability stops being a dashboard.** Three eras: built for humans (a UI you click) → coding
   agent plus skills helping *you* debug → a continuous loop where systems throw off far more telemetry
   than any human could read. The axis underneath is telemetry for people to read → telemetry for agents
   to read.
2. **Traces on a filesystem is the actual unlock.** Skills pull the relevant traces and logs down as
   files into the repo, next to the source — sometimes 10 MB of them. *"These harnesses are magical with
   files."* Same data, completely different usefulness.
3. **Why traces and not dashboards.** A trace tells the agent the exact code path one run took. A
   dashboard summarises. Without the path, *"there's a million paths it could have taken."*
4. **The loop inverts, and so does your role.** Before: you dig, then the agent helps fix. After: the
   agent digs, then you review. Responder → reviewer.
5. **Three components, and that's the whole anatomy.** *Event evidence* (traces + evals — what
   happened), *context + skills* (logs, APM, the repo — enough to fix it), *trigger* (periodic or
   on-error — when it runs). Everything else in the talk elaborates one of those three.
6. **Trace ten times more, not less.** The old advice to minimise logging existed because humans can't
   dig through volume and it becomes noise. Remove the human reading constraint and the rule flips.
7. **The bottleneck is confidence, not code generation.** Among people already using coding agents with
   skills, the blocking question is *"is this fix the right one to push?"*
8. **Sandboxes are a deployment decision, not a detail.** To debug your database the agent has to reach
   it. Many large companies won't send those connections outbound but will install into their own VPC —
   which is why the harness, the sandbox, the driving prompt and the skills are all your choice.

## Concepts you will pick up

| Term | Why it matters here |
| --- | --- |
| **Trace** | The structured record of one request through the system. The load-bearing artifact: it reveals which path the code actually took. |
| **Skill** | Packaged instructions plus tooling for a job. Here: skills that talk to observability platforms and land the *right* data in the repo. |
| **Online eval** | LLM-as-a-judge run continuously against production traces; the result attaches to the trace as extra data. |
| **Sandbox** | The isolated environment where the agent investigates — what replaces "the agent runs on my laptop". |
| **Cold start** | The expensive opening phase of debugging: pulling the data, forming a hypothesis. What this system actually removes. |
| **Facets / cohorting** | Skill-level techniques — slicing by dimension, grouping by customer — that let an agent find *which* traces matter. |

## Why it lands in `evaluation-and-observability`

The subject is telemetry and the judgement layered on it: traces, evals, triggers, and what you do with
the signal. It reaches into [`agent-architecture`](../../agent-architecture/) (the investigate-then-review
loop) and [`infrastructure`](../../infrastructure/) (sandboxes, VPC deployment), but the thesis is about
**what you measure and who reads it**.

## Still open, and where to be sceptical

- **The honest limit, stated by the speaker.** *"These are ideal, but a lot of times the fixes are
  bigger."* The worked example resolved to a one- or two-line fix. The bigger the fix, the more likely a
  human has to drive it over the line.
- **Cost is never addressed.** "Trace and log 10× more" has a storage and ingestion bill, and continuous
  online evals have an inference bill. Neither is quantified.
- **10 MB files in a repo** is presented as a virtue. Context limits, repo hygiene and what happens when
  the relevant trace set doesn't fit are left alone.
- **Vendor position.** This is a talk by a co-founder about his company's product. The architectural
  argument stands on its own, but the claim that the hard part is *skill design* — the thing Arize sells
  — is also a commercial claim. Worth reading with that in view.
- **Reproducing it yourself.** The Q&A answer to *"why not just point Claude Code at your data?"* is
  effectively "you can, and here is the work you're signing up for": finding the right traces, landing
  them in a good file format, and composing enough skills to find issues.

## Products and tools named in the talk

**AX** (Arize's SaaS, deployable into a customer VPC) · **Phoenix** (their open-source option) ·
**Signal** (the self-improving agent this talk is about, AX-only) · **Alyx** (Arize's in-product
assistant, and the source of the worked bug) · **Pyroscope** · Google Cloud logging · **Daytona**
(third-party sandboxes) · **Claude Code**.

## Related entries

- [**Loop Engineering vs Graph Engineering**](../../agent-architecture/loop-vs-graph/) — that entry
  establishes that non-deterministic flows need guardrails; this one is about the telemetry those
  guardrails would run on.
- [**Learning on the Job: The Future of Post-Training**](../../post-training/learning-on-the-job/) —
  a strong pairing. Both describe a loop that improves a system from production signal; that one closes
  it by updating *weights*, this one by opening a *pull request*. Both name the same unsolved problem
  from opposite ends: turning qualitative production feedback into a real improvement.

## Provenance

Compiled from the video's full transcript (153 segments, 0:01–20:12) plus the speaker's own chapter
outline. **Figure 3 reproduces the structure and wording of the talk's own "anatomy" slide; the remaining
figures are diagrams built to explain the architecture described in the transcript — illustrations of the
argument, not reproductions of specific slides.**

One gap to be aware of: quotations carry approximate timestamps as given in the talk ("around 3:30",
"around 13:27") rather than exact ones.

> **Correction, 2026-08-11.** This entry originally omitted `source_published`, on the stated grounds
> that "the source material does not state a publication date". That was wrong. The *intermediate
> artifact* this entry was written from did not state one; the **source** does — YouTube reports an
> upload date of **2026-07-24** for this video, now recorded above. The claim has been removed rather
> than softened, because it was not a gap in the source but a gap in how the source was read.
