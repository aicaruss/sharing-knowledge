---
title: "Rethinking Claude Code Best Practices — what takes over when you step out of the loop"
slug: rethinking-claude-code
topic: agent-architecture
type: talk-explainer
language: en
translations:
  - id
status: published
added: 2026-11-17
source_type: conference-talk
source_title: "Rethinking Claude Code Best Practices — Lydia Hallie, Anthropic"
source_url: https://www.youtube.com/watch?v=vlfCjWuv4es
source_author: Lydia Hallie
source_org: Anthropic
source_published: 2026-11-12
source_duration: 17m31s
tags:
  - claude-code
  - agent-harness
  - permissions
  - sandboxes
  - quality-gates
  - ci-cd
  - orchestration
  - code-review
---

# Rethinking Claude Code Best Practices

**[▶ Open the explainer](index.html)** · [Baca dalam Bahasa Indonesia](index.html?lang=id) · [Watch the source talk ↗](https://www.youtube.com/watch?v=vlfCjWuv4es)

> Reading online? → <https://aicaruss.github.io/sharing-knowledge/topics/agent-architecture/rethinking-claude-code/>

---

## Why this is in the knowledge base

Most entries here are about what agents can do. This one is about what happens to the developer's job
once agents do it unattended, and it brings a usable frame: list the five things you did in the loop —
steer, approve, say no, check, start — and name what takes each one over: **the model, the harness, or
the environment**. The frame applies to any agent you want to leave running, not only Claude Code. This
topic's scope names human-in-the-loop checkpoints and supervisor/worker topologies; the talk covers both,
ending in an orchestrator session that starts and judges worker sessions.

Its sharpest idea is the line between **judgement and guarantee**. In Anthropic's study a permission
classifier blocked 89% of planted dangerous commands where people caught 14% — and about one in ten still
got through. On her account a guarantee can only be enforced in the harness: a deny rule the classifier
never sees. By the same logic — this entry's extension, not her claim — the OS sandbox, a machine with
nothing to steal and CI are the other deterministic layers. Her test for which actions need a rule,
*"if [Claude] gets this wrong once, can I take it back?"*, is the most portable sentence in the talk.
**Read it with the disclosure in view:** the speaker works on the Claude Code team at Anthropic, in
developer relations, most of the remedies are Anthropic product features, and both pieces of evidence she
cites are Anthropic's own and unlinked; the explainer keeps the transferable principle apart from the
product.

## In one paragraph

As models got better at long tasks, Claude Code sessions at Anthropic went from one run a developer steered
and approved step by step to dozens of parallel sessions running for hours, and the five in-loop jobs moved
to the model, the harness or the environment. Getting out of the loop is easy (a newer model, auto mode, a
CLAUDE.md trimmed to what the code cannot show); making that safe is not. A classifier is judgement, so
anything irreversible goes under a deny rule, which is checked before the classifier sees the call. Rules
gate calls but not what a running command reaches — `npm test` runs your dependencies — so the environment
has to be restricted too: an OS-enforced sandbox on your own machine or, ideally, a cloud session on a
disposable machine with nothing worth stealing, while remembering that pushes and messages still leave it.
Correctness comes from pass/fail verification points enforced by hooks and, across all sessions, by CI —
on her team with a separate Claude reviewing every PR and people added by risk — and where she sees things
going, an orchestrator starts the sessions too, leaving you to start the first and review what comes out.

## Key takeaways

1. **The loop moves; it does not vanish.** Every job a person stops doing needs a named new owner. A job
   with none has not been automated, only left unattended. The closing slide maps all five.
2. **A classifier is a judgement, not a control.** 89% blocked against 14% caught by people is a large
   improvement and still lets about one dangerous command in ten through. Hence deny rules: checked
   before auto mode, so the classifier never sees a matching call.
3. **Reversibility sorts the rules.** Wrong code can be reverted — leave it to the model. Discarded
   uncommitted work or a key read into the transcript cannot — make it a rule. One question keeps the rule
   list short.
4. **Permissions gate calls, not effects.** `npm test` runs code you did not write; neither a rule nor a
   human approver sees what it opens. So contain the environment: a sandbox the OS enforces, child
   processes included; or, ideally, a cloud machine where `.env`, SSH keys and tokens are simply absent. Pushes
   and connector messages still leave that machine, so the gate stays on.
5. **Review verification points, not diffs.** The same prompt yields different reasonable results, so put
   pass/fail checks along the way and review those. Enforce the essential ones with hooks — and, on her
   account, exit with code 2, because exit 1 lets the task be marked complete anyway. Test that claim in
   your own setup before relying on it.
6. **CI is the floor every session meets.** Sessions differ in prompt, hooks and choices; CI runs the same
   checks on all their PRs. On her team, a separate Claude with fresh context reviews each PR first, and
   people are added by risk — the tiers differ between speech and slide.
7. **CLAUDE.md should hold only what the code cannot tell the model.** Emphatic rules written for older
   models are, she says, unnecessary now and can make the model go off track; the one line worth keeping
   on her slide is a fact no model could infer from the repository.

## Concepts you will pick up

| Term | Why it matters here |
| --- | --- |
| **The five in-loop jobs** | Steering, approving, saying no, checking, starting — a checklist for what you are still doing by hand. |
| **Model / harness / environment** | The three places a job can move to. The harness is Claude Code's own enforcement: permissions, deny rules, hooks. |
| **Auto mode** | A permission mode that runs a classifier on nearly every action except reading or editing project files; configured in plain English. Judgement. |
| **Deny rule** | `permissions.deny` in `settings.json`, checked before the classifier. The guarantee. |
| **Sandbox** | OS-enforced limits on files, folders and hosts for shell commands and their children — but not for Claude's own files, MCP servers or hooks. |
| **Cloud session** | Its own disposable machine with a fresh repo copy, restricted network and network secrets. Nothing local to steal; pushes and messages still leave. |
| **Verification point** | Any pass/fail check along the way — test, build, screenshot — reviewed instead of the whole diff. |
| **Hook exit code** | Her claim: exit 2 sends Claude back to fix; exit 1 lets the task close. |
| **Orchestrator and threads** | One session that splits work, starts sessions ("threads") and judges what returns; a deciding model and a doing model, set separately. |

## Worth noting for our own context

In a regulated or audited setting, the talk's line between judgement and guarantee is an auditor's line
between a statistic and a control. Deny rules, an OS sandbox, configuration committed to the repo, CI gates
and written review tiers can be inspected and evidenced; a classifier's catch rate says nothing about any
single action. Her "things that leave [the machine]" — pushes, messages through connectors — are where the
audit trail has to sit.

## Still open

What **she** concedes:

- Auto mode and prompting are each *"not a guarantee"*; about one in ten planted commands got through.
- The sandbox can read most of the machine by default and leaves Claude's own files, MCP servers and hooks
  outside it.
- Merge-when-ready: *"that's not the default"*; and the review tiers are hedged — "maybe", "might need two".

Where **I** would push — my assessment, not hers:

- **Throughput is not quality.** 2,500 → 30,000+ changes a day comes from Anthropic's own blog post; no
  defect, revert or incident rate is shown.
- **Cost is absent.** Dozens of hours-long sessions, a reviewing Claude per PR and agents double-checking
  each bug all carry a token bill the talk never mentions.
- **Who decides a change is risky?** Review tiers need the risk known before review; the talk does not say
  who or what makes that call.
- **Her own example auto-merges a row labelled "dependencies"** (slides at 1:30 and 14:33), while her
  safety section's threat model is a compromised dependency. CI and the sandbox may cover it; the talk does
  not connect the two.
- **`autoMode.hard_deny` versus `permissions.deny`.** By her description the `autoMode` block goes to the
  classifier, and she does not say whether `hard_deny` is treated differently. If not, the name promises
  more than a classifier gives; the guarantee she describes is `permissions.deny`.
- **Hooks run outside the local sandbox, by her account**, so a hook running `npm test` runs the very
  dependency code the sandbox is meant to contain — an argument for her cloud conclusion.
- **A fresh-context reviewer is not a different model.** The talk does not say which model reviews.
- **The CLAUDE.md claim is asserted, not shown**, and **the evidence cannot be checked from the talk**: the
  study and the blog post are named on slides only, with no links and no study title.

## Also referenced in the source

None of these is linked in the source; no URL is given here because none was given there.

- **"Redesigning source control at Anthropic"** — Anthropic blog post, October 2026. Cited on a slide (1:50)
  for **2,500 (May 2026) → 30,000+ (September 2026) code changes merged per day to Anthropic's monorepo**.
  Aloud she says only "our blog post in October"; "merged" and "monorepo" are the slide's words.
- **An Anthropic study, August 2026** — no title shown. Slide footnote (5:57): *"1,053 paid testers, one
  dangerous command swapped in per session. Anthropic, August 2026"*. **14% caught by people, 89% blocked
  by auto mode**; aloud, *"about one in 10 of those commands still went through"*.
- **SWE-bench Pro chart** — slide at 0:22, *"As reported by Anthropic. Test settings vary by model."*, from
  52% (Opus 4.5) to 90% (Opus 5.5) and a final 93% point whose model label is hidden behind the speaker's
  webcam. Never discussed.
- **Anthropic's Claude Code best-practices documentation** — recommended at 17:26, without a title or link.

## Related entries

- [**Verification Debt: Guide, Verify, Solve**](../../evaluation-and-observability/verification-debt/) —
  her PR review by a separate Claude with fresh context, not the session that wrote it, is that entry's
  criterion in practice: verify with a different methodology than the generator — a test her setup only
  half passes, since fresh context is not a different model. It also echoes her 14% figure from an
  unrelated study: people are a weak backstop for confident machine output.
- [**From Signal to PR: Anatomy of a Self-Improving Agent**](../../evaluation-and-observability/signal-to-pr/)
  — the same inversion of the loop: the agent does the digging and the doing, the person starts and reviews.
- [**Loop Engineering vs Graph Engineering**](../loop-vs-graph/) — the orchestrator session spawning worker
  threads is a concrete instance of a coordinating layer wrapping loops, with deciding and judging split
  from doing across two models.
- [**Memory Layers for AI Agents**](../memory-layers/) — CLAUDE.md is preloaded plain-text memory, the "do
  nothing" retrieval strategy; her advice to trim it to what the model cannot see in the code is the
  maintenance half of that entry's third pillar.

## Provenance

Compiled from the video's **auto-generated English caption track** (3,566 words, 0:00–17:30), written
descriptions of **20 frames** captured for reference, the creator's eight chapters, and the video
description (for the speaker's title). No product documentation was consulted: every statement about how
Claude Code behaves is the speaker's claim, reported as hers.

**Quotes** are verbatim from the caption track, slips included ("a worse results", "the Claude"), with
timestamps marking where the cited words begin, to the second. The captions garble names — "Cloud Code"/"Cloud",
"Cloud MD", "Opus 55"/"Opus 45", "doctor prompt audit", "or end file" (`.env`), "automo" — so inside quotes
they are corrected **in square brackets**, and only where the video title or a slide confirms the
spelling; "[you]" (6:05) and "tool [call]" (6:22) are supplied the same way.

**Not corroborated, and so handled.** Fable's version number (heard at 0:20) is omitted — the chart label is
behind the webcam and the orchestrator slide prints only "Fable". "Claude Code projects" is heard twice,
once garbled, and is on no slide: named as heard. The permission-skipping flag (1:09) is on no slide and is
not spelled out. "A Cloud session" (from 9:30) could be "Claude session" or "cloud session"; it is read as
cloud because the slides show a cloud icon and "Edit cloud environment", and she later says "start in the
cloud" (17:18). Speech-versus-slide differences — the review tiers, the fourth "Out of the loop" card, the
2,500 → 30,000 figure — are reported side by side, not merged.

**Figures.** Six hand-drawn inline SVGs, no screenshots. Figures 1, 2, 3 and 5 are redrawn from the frames
at 0:42/1:30, 2:18/16:50, 6:25/8:57 and 12:55/13:10, with slide wording and this entry's layout; Figure 6
is a composite of 16:08 and 14:33 plus two annotations from speech, marked as such; Figure 4 is assembled
from speech (6:19–10:44) and draws the local sandbox and the cloud session side by side, because she
presents them as alternatives and never says whether a cloud session sandboxes commands. Where the webcam hides part of a slide, the caption says how it was completed.

**Metadata.** `source_title` reproduces the video title exactly, including the no-break space after the em
dash. `source_published` is the yt-dlp upload date in UTC; the same instant (2026-11-12T03:26:55Z) is
2026-11-11 in US Pacific time, as YouTube's page shows — the UTC date is kept. **`source_event` is omitted**:
the description names no event, the slides carry no branding, and she says only: "I had some technical
difficulties during my talk this morning, so I ran back home and I'm just going to record it from my
computer instead" (0:00) — so this video was recorded at home, after a live talk whose venue and date are
unstated. **`source_type: conference-talk`** is the closest value in the
repository's closed list for that; AI Engineer is the publishing channel, not a confirmed venue.

**Whose words.** Passages marked "my reading", "my observation" or "my assessment", the second half of
**Still open**, and the explainer table's "Kind of control" column are this entry's judgement.

**Translation.** The Indonesian version lives in the same `index.html`, behind the English / Bahasa Indonesia
toggle in the header ([open it directly](index.html?lang=id)). It translates the English explainer, which stays the
reference: same structure, numbers, figures and disclosures; quotes stay in the speaker's English with
glosses outside the quotation marks; figure labels are translated, product names, code and on-slide UI and
prompts are not.

Note on presentation: this explainer carries its own accent palette (berry `#A12F6A` on a pale rose-grey
paper `#F7F3F4`) while keeping the house component vocabulary and layout rules. See
[Design system](../../../README.md#design-system).
