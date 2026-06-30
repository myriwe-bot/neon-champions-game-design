---
title: STORY-CHAMP-OPS-003 Operation Aftermath and Closeout Readability Smoke
type: story
status: ready
phase: production
owner: shared
created: 2026-06-29
updated: 2026-06-30
source_lore: [champions, digital-net, greenland, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-011-champion-assets-and-operations-depth,
    production/stories/story-champ-ops-001-champion-asset-slot-and-prototype-operation-on-ramp,
    production/stories/story-champ-ops-002-operation-targeting-and-forecast-readability-pass,
    design/gdd/strategic-map,
    design/gdd/intel-resource,
    design/gdd/tactical-combat/champion-operations-and-progression,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-CHAMP-OPS-003 Operation Aftermath and Closeout Readability Smoke

## Status

READY / approved. Human approval recorded 2026-06-30: "Approved STORY-CHAMP-OPS-003". This story is now authorized for one Unity implementation branch.

## Story type

Strategic UX + integration smoke / closeout-readiness pass with PlayMode evidence.

## Parent / context

Parent: `EPIC-VSLICE-MVP-011 Champion Assets and Operations Depth`.

`STORY-CHAMP-OPS-001` created the first prototype Champion Asset / Operation surface. `STORY-CHAMP-OPS-002` made its forecast target readable and selectable. The next safe step is not adding a second operation; it is proving the post-use state stays understandable across the surrounding strategic loop and that EPIC-011 can either close or identify one sharply scoped remaining gap.

## Player/design value

As a player, after spending Intel on a Champion Operation, I need to understand what changed, that I cannot accidentally spend again on the same target, and that ordinary movement/site/tactical interactions still make sense around the forecast marker.

## Source authority

Required sources:

- `production/epics/epic-vslice-mvp-011-champion-assets-and-operations-depth.md`.
- `production/stories/story-champ-ops-001-champion-asset-slot-and-prototype-operation-on-ramp.md` and merged Unity evidence.
- `production/stories/story-champ-ops-002-operation-targeting-and-forecast-readability-pass.md` and merged Unity evidence.
- `design/gdd/tactical-combat/champion-operations-and-progression.md` §§29-80 and §§98-198, under the same narrow human-approved source-authority exception recorded in EPIC-011.
- `design/gdd/intel-resource.md` for existing Intel language.
- `design/gdd/strategic-map.md` for site/route/map presentation boundaries.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, `docs/architecture/ci-build-automation.md`.

## In scope

- Improve or verify the after-application operation surface so the player can read:
  - which site was forecasted;
  - the 1 Intel spend result;
  - that the operation marker is now present;
  - that a repeat attempt on the same target is denied without spending Intel or changing other markers.
- Add a connected strategic smoke path around the operation marker, covering at minimum:
  - select Champion;
  - acquire/use enough Intel through the existing loop;
  - select/apply the forecast operation;
  - inspect the forecasted target after application;
  - prove duplicate/repeat denial;
  - prove a normal strategic interaction or guarded-site tactical handoff remains available/unbroken after the marker exists.
- Add or update focused tests only where needed to cover repeat-denial/no-partial-mutation and surrounding-loop regression.
- Add PlayMode evidence under Unity `production/evidence/STORY-CHAMP-OPS-003/` for after-apply, repeat-denied, and surrounding-loop-unbroken states.
- Update EPIC-011 closeout notes with a concise recommendation: close epic, defer named gaps, or prepare one more candidate.

## Out of scope

- New Operations, multiple operation choices, cooldowns, loadouts, reaction windows, counter-operations, or operation cadence systems.
- Full Champion inventory/assets, progression, skill trees, asset tiers, loss/transfer, or loot.
- New resources, Intel subtypes, income changes, dirty-information/fog, misinformation, PR, legitimacy, feed systems, or strategic AI.
- New sites/routes/map topology, tactical combat rules, victory rules, final art/audio/VFX/icons/localization/accessibility framework.
- Canon/final operation naming. Prototype labels remain acceptable.

## Acceptance criteria

- [ ] After applying `prototype_operation_site_forecast`, the active UI/status clearly shows the forecasted site and spent-result feedback.
- [ ] Inspecting or reselecting the forecasted target clearly reports that it is already forecasted / unavailable for repeat use.
- [ ] Repeat attempts on the same forecasted target spend 0 additional Intel and do not mutate any other site marker.
- [ ] At least one normal strategic path remains visibly usable after the operation marker exists: movement, non-operation site interaction, or guarded-site tactical handoff.
- [ ] Existing `STORY-CHAMP-OPS-001` and `STORY-CHAMP-OPS-002` tests/evidence expectations continue to pass.
- [ ] Evidence under Unity `production/evidence/STORY-CHAMP-OPS-003/` includes after-apply, repeat-denied, surrounding-loop-unbroken screenshots/notes, and omissions/deferred-work notes.
- [ ] Exact-head Unity Foundation CI passes before merge.
- [ ] EPIC-011 closeout recommendation is documented in design-control after review.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- Focused EditMode tests for duplicate/repeat denial and no-partial-mutation if existing coverage is insufficient.
- PlayMode smoke test or generated PNG/text evidence for after-apply, repeat-denied, and surrounding-loop-unbroken states.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge, and post-merge main CI after merge.

## Ambiguity Check

Status: PASS for candidate review; NOT implementation authority.

Candidate assumptions:

- The next safest EPIC-011 step is a connected after-use/readability smoke and closeout recommendation, not adding a second Champion Operation.
- Existing prototype operation ID and 1 Intel cost remain unchanged.
- If the implementation already satisfies part of this story, the work should be mostly tests/evidence/docs rather than inventing new UI scope.
- Prototype/non-final labels remain acceptable.

## Branch / PR requirements

- Branch name: `story/STORY-CHAMP-OPS-003-operation-aftermath-closeout-smoke`.
- PR title: `STORY-CHAMP-OPS-003 operation aftermath closeout smoke`.
- Required linked story ID: `STORY-CHAMP-OPS-003`.
- Required evidence path: `production/evidence/STORY-CHAMP-OPS-003/` in Unity.
- Required omissions section: explicitly list deferred Operations/Assets systems or state `No known omissions`.

## Human approval

Recorded 2026-06-30: "Approved STORY-CHAMP-OPS-003".

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent/context.
- [x] User/player/system value is clear.
- [x] Source authority and narrow source-authority exception are explicit.
- [x] In-scope and out-of-scope are bounded.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Ambiguity Check is PASS for candidate review.
- [x] Human approval has been recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required evidence exists.
- [ ] Required tests/CI pass, or human-approved exceptions are documented.
- [ ] PR/code review is complete if a Unity PR is opened.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY / approved. Activate `production/sprints/codex-story-champ-ops-003.prompt.txt` and update the Unity current-task pointer before Codex implementation.
