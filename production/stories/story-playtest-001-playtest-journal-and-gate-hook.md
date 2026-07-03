---
title: STORY-PLAYTEST-001 Playtest Journal and Gate Hook
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-07-03
updated: 2026-07-03
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    production/planning/post-audit-foundation-pivot-2026-07-03,
    production/gates/review-mode,
    production/stories/story-template,
  ]
approval: pending
---

# STORY-PLAYTEST-001 Playtest Journal and Gate Hook

## Status

READY-candidate / approval pending.

## Story type

Playtest + Process.

## User/player/system value

As the project owner, I want playtest feel notes captured as first-class evidence, so future gates can judge fun, readability, fiction-fit, and confusion instead of only correctness.

## In scope

- Create `production/playtests/playtest-journal.md` with a reusable dated-entry template.
- Add gate wording requiring closeout stories to link playtest notes or state why playtest evidence is N/A.
- Preserve exact human complaints as acceptance drivers.
- Add index/log links.

## Out of scope

- External playtester recruitment.
- Analytics tooling.
- Long survey design.
- Changing Unity code.

## Acceptance criteria

- [ ] Playtest journal exists and has a template for: build/commit, scenario, what dragged, what surprised, what confused, what felt off-fiction, fun verdict, next decision.
- [ ] Closeout/gate docs reference the journal as evidence for subjective/fun claims.
- [ ] Index/log discoverability is updated.

## Verification requirements

- `git diff --check`.
- Quartz build.

## Ambiguity Check

Status: PASS.

## Verdict

READY-candidate / approval pending.
