---
title: STORY-QA-003 Guarded Site Capture Readability and Evidence Pass
type: story
status: draft
phase: production
owner: shared
created: 2026-06-04
updated: 2026-06-04
source_lore: []
related:
  [
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-loop-002-visible-guarded-site-capture-smoke,
  ]
approval: pending
---

# Story: STORY-QA-003 Guarded Site Capture Readability and Evidence Pass

## Status

Draft optional closeout QA packet. Use only if STORY-LOOP-002 succeeds technically but the visible guarded-site capture path is confusing, ugly, or poorly evidenced.

## Story type

QA + UX Readability + Bugfix.

## Estimate

- Size: S/M.
- Basis: fixes and documents comprehension issues in an already merged guarded-site capture smoke; does not add new systems.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player/designer, I want the guarded-site capture smoke to be legible enough to judge, so the current epic can close on a usable demo rather than a technically correct but unreadable prototype.

## Source requirements

- `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft.
- `design/gdd/strategic-map.md` §10 Site and Infrastructure States.
- `design/gdd/tactical-combat.md` §3 Design Principles and §4 MVP Scope.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.
- Evidence and omissions from STORY-LOOP-002.

## In scope

- Fix readability bugs in the current guarded-site capture smoke path, such as:
  - unclear selected site/champion/acting side;
  - unclear Attack/Interact availability;
  - unclear battle launched/in progress/resolved state;
  - unclear site owner/control after capture;
  - confusing or missing tactical-to-strategic result summary.
- Improve placeholder layout/copy/markers only enough to make the demo understandable.
- Add or update screenshot/video/evidence checklist after fixes.
- Add regression tests for any bugfixable state/readability logic.

## Out of scope

- New gameplay systems, new tactical mechanics, recruitment, larger map content, final UI/art/audio/copy, balance, new lore/site/faction naming, strategic AI, networking.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder labels, colors, icons, localization keys, and screenshot/video evidence.
- Minimal layout adjustments using existing UI patterns.

Not allowed:

- Adding new mechanics to hide readability problems.
- Final asset/content decisions.
- Changing strategic/tactical rules without updating source GDD/story docs.

## Acceptance criteria

- [ ] Given the guarded-site capture smoke, a reviewer can identify the active faction, active Champion, selected guarded site, available Attack/Interact action, battle outcome, and final site owner without developer explanation.
- [ ] Given the smoke path completes, screenshot/video evidence shows before/after site control and tactical/result handoff clearly.
- [ ] Given any state/readability bug is fixed, regression tests or manual reproduction evidence are included.
- [ ] No new gameplay systems, content expansion, final art/UI, or tactical mechanics are introduced.
- [ ] CI passes.

## Verification requirements

- Unity edit-mode tests: Required for any domain/UI-state bugfix logic.
- Unity play-mode tests: Required if feasible for smoke/readability regression; otherwise document blocker and use manual evidence as temporary exception.
- Manual Unity scene/prefab checks: Required.
- Screenshot/video evidence: Required.
- CI evidence: Required on implementation PR.
- TDD evidence required? Yes for bugfixable logic; N/A for screenshot-only evidence, with reason.

## Ambiguity Check

Status: PASS-candidate if invoked after LOOP-002 evidence identifies concrete readability issues.

Assumption:

- This story is optional and should not run before STORY-LOOP-002.

## Branch / PR requirements

- Branch name: `story/STORY-QA-003-guarded-site-capture-readability-evidence-pass`
- PR title: `STORY-QA-003 Guarded site capture readability and evidence pass`
- Required linked story ID: `STORY-QA-003`
- Required evidence summary: issue list, fixes, before/after screenshot/video, tests where applicable, CI, omissions.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Verdict

Draft optional QA packet.
