---
title: STORY-LOOP-002 Visible Guarded Site Capture Smoke
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
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger,
    production/stories/story-strat-005-strategic-battle-result-application,
  ]
approval: pending
---

# Story: STORY-LOOP-002 Visible Guarded Site Capture Smoke

## Status

Draft. This is the recommended vertical-slice closeout packet for the current epic after STORY-STRAT-004 and STORY-STRAT-005.

## Story type

Playtest + Integration + UX/Smoke.

## Estimate

- Size: M.
- Basis: connects existing strategic map UI/input, guarded-site handoff, and result application into one visible smoke path. It should use the smallest acceptable tactical/result stub until real tactical combat exists.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player/designer, I want to see a Champion capture a guarded neutral site on the visible strategic map, so that we can judge whether the strategic MVP loop is becoming understandable and worth expanding into larger maps, bases, recruitment, and tactical combat.

## Source requirements

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 3-9.
  - `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft.
  - `design/gdd/strategic-map.md` §10 Site and Infrastructure States.
  - `design/gdd/strategic-map.md` §14 Strategy-to-Tactical DTOs.
- Story dependencies:
  - STORY-STRAT-004.
  - STORY-STRAT-005.
- ADR / architecture / control:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

- A visible smoke path where the player can:
  - select the active Champion;
  - move to or start near a guarded neutral site;
  - see that the site is guarded and interactable;
  - launch the guarded-site handoff;
  - apply a deterministic test/stub attacker-win result if real tactical combat is not available;
  - see the site become controlled by the attacking faction.
- Clear on-screen feedback for guarded state, interaction type, battle launched/result applied, and new site owner.
- Automated PlayMode smoke if feasible; otherwise documented blocker plus screenshot/video evidence.
- Evidence package documenting omissions and the temporary tactical/result stub.

## Out of scope

- Real tactical combat implementation, unless already available from another story.
- Larger map expansion, cities/bases, recruitment, central objective victory, enemy-site contests, final art/UI/copy, balance, strategic AI, networking.
- Hiding the tactical stub. If a stub is used, the PR must call it out plainly.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- A deterministic attacker-win test/stub result path if real tactical combat is not implemented yet.
- Placeholder guarded site IDs, labels, and guard army fixture data.
- Temporary UI text/keys for smoke evidence.

Not allowed:

- Claiming tactical combat is implemented when only a stub/result injector exists.
- Expanding into recruitment, cities/bases, or larger map content in this story.

## Acceptance criteria

- [ ] Given the visible strategic smoke scene, when the active Champion interacts with a guarded neutral site, then the UI clearly shows a guarded-site battle handoff.
- [ ] Given the smoke applies an attacker-win result, then the guarded site becomes controlled by the attacking faction and the UI visibly reflects the new owner/state.
- [ ] Given the smoke path completes, then evidence includes screenshot/video and a checklist of what was real versus stubbed.
- [ ] Given the story PR, then omissions explicitly state whether tactical combat was real or stubbed.
- [ ] CI passes.

## Verification requirements

- Unity edit-mode tests: Required for underlying command/result behavior via STORY-STRAT-004/005 tests.
- Unity play-mode tests: Required if harness supports the visible smoke path; otherwise document blocker and use manual evidence as a temporary exception.
- Manual Unity scene/prefab checks: Required.
- Screenshot/video evidence: Required.
- CI evidence: Required.
- TDD evidence required? Yes for new logic; smoke wiring may use existing test patterns.

## Ambiguity Check

Status: FAIL.

Open questions:

- Is a deterministic attacker-win result stub acceptable for this smoke, or must minimal tactical combat exist first?
- Should this story close EPIC-STRAT-MVP-001 if it passes, with larger map/cities/recruitment/tactical combat moving to the next epic?

## Branch / PR requirements

- Branch name: `story/STORY-LOOP-002-visible-guarded-site-capture-smoke`
- PR title: `STORY-LOOP-002 Visible guarded site capture smoke`
- Required evidence summary: visible smoke checklist, screenshot/video, tests, CI, omissions/stubs.

## Verdict

Draft.
