---
title: STORY-CHAMP-OPS-002 Operation Targeting and Forecast Readability Pass
type: story
status: ready
phase: production
owner: shared
created: 2026-06-29
updated: 2026-06-29
source_lore: [champions, digital-net, greenland, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-011-champion-assets-and-operations-depth,
    production/stories/story-champ-ops-001-champion-asset-slot-and-prototype-operation-on-ramp,
    design/gdd/strategic-map,
    design/gdd/intel-resource,
    design/gdd/tactical-combat/champion-operations-and-progression,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-CHAMP-OPS-002 Operation Targeting and Forecast Readability Pass

## Status

READY / approved for Unity implementation. Human approval recorded 2026-06-29: "Approved". This approves `STORY-CHAMP-OPS-002` as the next narrow EPIC-011 implementation packet after `STORY-CHAMP-OPS-001` merged.

## Story type

Strategic UX + domain/presentation refinement with PlayMode evidence.

## Parent / context

Parent: `EPIC-VSLICE-MVP-011 Champion Assets and Operations Depth`.

`STORY-CHAMP-OPS-001` proved the first prototype Champion Asset/Operation surface and a one-site forecast effect. The next safe step is not a new operation or deeper economy; it is making the existing forecast operation more understandable and controllable when several guarded sites could be valid targets.

## Player/design value

As a player, I need to understand which site my Champion Operation will forecast, why that target is legal or illegal, and what visible map marker will change before I spend Intel.

## Source authority

Required sources:

- `production/epics/epic-vslice-mvp-011-champion-assets-and-operations-depth.md`.
- `production/stories/story-champ-ops-001-champion-asset-slot-and-prototype-operation-on-ramp.md` and merged Unity evidence for the implemented baseline.
- `design/gdd/tactical-combat/champion-operations-and-progression.md` §§29-80 and §§98-198, under the same narrow human-approved source-authority exception recorded in EPIC-011.
- `design/gdd/intel-resource.md` for existing Intel language.
- `design/gdd/strategic-map.md` for site/route/map presentation boundaries.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, `docs/architecture/ci-build-automation.md`.

## In scope

- Replace or supplement the current automatic first-adjacent-guarded-site forecast target with a clearer target-preview contract.
- Allow the prototype forecast operation to target a selected adjacent guarded site, or otherwise expose the current automatically selected target with explicit legal-target reasoning.
- Show target availability/denial reasons in player-facing language, including at least:
  - no active/selected Champion;
  - no adjacent guarded site;
  - selected site is not adjacent;
  - selected site is not guarded;
  - selected site is already forecasted;
  - insufficient Intel.
- Make forecasted sites visibly identifiable in node/card/HUD text after application.
- Preserve the existing `prototype_operation_site_forecast` operation ID and 1 Intel cost unless a test requires only defensive refactoring.
- Add focused domain/application tests for target selection and denial/no-partial-mutation behavior.
- Add PlayMode evidence for available selected target, denied selected target, and applied forecast marker.

## Out of scope

- New Operations, multiple operation choices, cooldowns, loadouts, reaction windows, or counter-operations.
- Full Champion inventory/assets, progression, skill trees, asset tiers, loss/transfer, or loot.
- New resources, Intel subtypes, economy/income changes, dirty-information/fog, misinformation, PR, legitimacy, or feed systems.
- New sites/routes/map topology, tactical combat rules, AI, victory rules, final art/audio/VFX/icons/localization/accessibility framework.
- Canon/final operation naming. Prototype labels remain acceptable.

## Acceptance criteria

- [ ] The selected/previewed forecast target is explicit in the active Champion operation UI/status.
- [ ] Selecting or inspecting an adjacent guarded site can make it the forecast target, or the implementation clearly explains why the default target is used.
- [ ] Illegal/unavailable targets produce readable denial reasons and do not spend Intel or mutate site markers.
- [ ] Applying the forecast operation marks exactly one legal target and spends exactly 1 Intel.
- [ ] A forecasted target is visible in strategic node/card/HUD text after application.
- [ ] Existing `STORY-CHAMP-OPS-001` operation surface, resource HUD, strategic movement, site interaction, objective, and tactical handoff smokes continue to pass.
- [ ] Evidence under Unity `production/evidence/STORY-CHAMP-OPS-002/` includes available-target, denied-target, applied-marker, and omissions/deferred-work notes/screenshots.
- [ ] Exact-head Unity Foundation CI passes before merge.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- Focused EditMode tests for target selection/denial/no-partial-mutation behavior.
- PlayMode smoke test or generated PNG/text evidence for selected target, denied target, and applied marker.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge, and post-merge main CI after merge.

## Ambiguity Check

Status: PASS. Human approval recorded 2026-06-29: "Approved".

Candidate assumptions:

- The next safest EPIC-011 step is target readability/control for the existing prototype forecast operation, not adding a second operation.
- The story may support either explicit selected-site targeting or a clearer default-target explanation, but implementation must prove the player can understand target legality before spending Intel.
- The operation ID and cost remain unchanged.
- Prototype/non-final labels remain acceptable.

## Branch / PR requirements

- Branch name: `story/STORY-CHAMP-OPS-002-operation-targeting-forecast-readability`.
- PR title: `STORY-CHAMP-OPS-002 operation targeting forecast readability`.
- Required linked story ID: `STORY-CHAMP-OPS-002`.
- Required evidence path: `production/evidence/STORY-CHAMP-OPS-002/` in Unity.
- Required omissions section: explicitly list deferred Operations/Assets systems or state `No known omissions`.

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

READY / approved for Unity implementation. Runnable Codex prompt prepared at `production/sprints/codex-story-champ-ops-002.prompt.txt`.
