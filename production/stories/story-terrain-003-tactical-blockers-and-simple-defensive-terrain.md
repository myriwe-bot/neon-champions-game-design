---
title: STORY-TERRAIN-003 Tactical Blockers and Simple Defensive Terrain
type: story
status: done
phase: production
owner: shared
created: 2026-06-28
updated: 2026-06-28
source_lore: [greenland, white-sky, digital-net]
related:
  [
    production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability,
    production/stories/story-terrain-001-strategic-terrain-tags-and-tactical-layout-family-contract,
    production/stories/story-terrain-002-tactical-layout-definitions-and-deployment-zones,
    design/gdd/tactical-combat,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-TERRAIN-003 Tactical Blockers and Simple Defensive Terrain

## Status

DONE / merged. Unity PR #92 merged on 2026-06-28 as `74badf31fc10a91dbd8723242263be6d39b94711`; exact-head PR CI and post-merge main CI passed.

## Story type

Tactical Rules + UI.

## Parent epic

- [EPIC-VSLICE-MVP-010 Terrain, Tactical Battlefields, and Map-Space Readability](../epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability.md)

## User/player/system value

As a player, I want tactical battlefields to contain a few readable blocked and defensive cells, so layout family differences start affecting movement and positioning without adding full cover/LoS simulation.

## Source requirements

- `STORY-TERRAIN-001` is DONE and provides strategic terrain/context tags plus tactical layout-family selection.
- `STORY-TERRAIN-002` is DONE and provides authored tactical layout definitions plus attacker/defender deployment zones.
- `design/gdd/tactical-combat.md` §§3-6 and §6.2A for flat hex board, tactical movement/attack, and EPIC-010 tactical battlefield contract.
- `design/gdd/strategic-map.md` §9.5 for strategic context feeding tactical battle setup.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, and `docs/architecture/ci-build-automation.md`.

## In scope

- Extend authored tactical layout definitions with prototype terrain cell metadata for:
  - blocked/obstacle cells that cannot be occupied or moved into;
  - simple defensive cells that are visible and can apply a small existing/prototype defensive effect only when explicitly validated by this story.
- Keep terrain data keyed by existing layout family definitions (`server_yard`, `fortified_approach`, `open_route_clash`, `infrastructure_hub`).
- Update movement validation and legal-move affordances so blocked cells are excluded clearly.
- Surface blocked and defensive cells in tactical presentation snapshots and readable UI/debug evidence.
- Add validation for terrain cells that reference non-board coordinates, overlap deployment zones illegally when applicable, duplicate coordinates ambiguously, or use unknown terrain cell types.
- Add tests proving at least two layout families expose distinct blocked/defensive cell patterns and that blocked cells affect legal movement.
- Preserve existing deployment-zone, movement, attack, AP, Defend, retaliation, command, CombatAI, battle result, and strategic result-return behavior except for the explicitly scoped blocker/defensive-cell behavior.

## Out of scope

- No elevation, line-of-sight rewrite, overwatch, destructible terrain, hazards, weather, fog, supply, strategic terrain movement costs, strategic topology changes, or strategic AI terrain valuation.
- No full cover system, facing rules, ranged accuracy, damage formulas beyond the narrow approved defensive-cell effect.
- No new units, abilities, Champion Operations, resources, sites, objectives, base/facility rules, AI strategy, or balance pass.
- No final art/icons/VFX/audio/localization.
- No map editor UI.

## Allowed stubs, mocks, placeholders, or temporary data

- Prototype blocked/defensive coordinates and labels are allowed.
- Crude colors/text markers are allowed.
- Defensive-cell behavior may be mechanically minimal; if the existing Defend damage-reduction model is reused, document it as a prototype terrain effect and keep it test-covered.
- Debug/evidence-only visualization is allowed if production UI is not ready.

## Dependencies

- Required prior story: `STORY-TERRAIN-002` DONE / merged.
- Required Unity CI: post-merge main CI for `STORY-TERRAIN-002` passed.
- Required data: authored tactical layout definitions and deployment zones.

## Acceptance criteria

- [x] Authored layout definitions can express blocked and simple defensive terrain cells per layout family.
- [x] Blocked cells are present in board state or presentation snapshots and are not legal movement destinations.
- [x] Defensive cells are present in board state or presentation snapshots and have either a narrow tested prototype effect or a clearly documented inert/readability-only behavior.
- [x] At least two layout families produce visibly/testably distinct terrain-cell patterns.
- [x] Invalid terrain cell definitions fail validation clearly.
- [x] Existing tactical loop behavior remains intact outside the scoped blocker/defensive-cell behavior.
- [x] Evidence shows selected layout family plus blocked/defensive cells for at least two contexts.
- [x] The implementation leaves a clean extension point for `STORY-TERRAIN-004` range, threat, and terrain readability.

## Verification requirements

- Unit/EditMode tests for terrain-cell validation and layout-family terrain-cell selection.
- EditMode tests proving blocked cells are excluded from legal movement/placement as scoped.
- PlayMode smoke or equivalent presentation evidence showing at least two selected layout families with blocked/defensive terrain output.
- PNG or text evidence under `production/evidence/STORY-TERRAIN-003/`.
- Exact-head Unity Foundation CI before merge and post-merge main CI before marking DONE.

## Ambiguity Check

Status: PASS.

Open questions:

- Should defensive cells be inert/readability-only in this story, or should they apply a tiny prototype defensive effect? Default recommendation: use a tiny tested prototype effect only if it can reuse existing Defend-style damage reduction without changing broader combat formulas.

Assumptions:

- Use existing flat tactical board architecture.
- Keep terrain cell data authored and deterministic, not procedural.
- Prefer narrow movement/placement blockers before broader combat terrain effects.

Out of scope:

- Cover/LoS/elevation/hazards/weather/fog/supply/strategic movement terrain rules/final art.

Allowed stubs/mocks:

- Prototype coordinates, labels, colors, and debug/evidence markers.

Human-approved answers:

- Approved 2026-06-28 via user instruction: "Approved next story".
- Use the story's listed assumptions, exclusions, allowed placeholders, branch/PR requirements, and verification requirements as the implementation contract.
- Defensive cells may use the story's default recommendation: a tiny tested prototype effect only if it can reuse existing Defend-style damage reduction without broader combat formula changes; otherwise document inert/readability-only behavior clearly.

## Branch / PR requirements

- Branch name: `story/STORY-TERRAIN-003-tactical-blockers-simple-defensive-terrain`
- PR title: `STORY-TERRAIN-003 Tactical blockers and simple defensive terrain`
- Required linked story ID: `STORY-TERRAIN-003`.
- Required evidence summary: tests run, at least two layout-family contexts, blocked/defensive-cell output, evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked.
- [x] Exact ADR/architecture/control-manifest source is linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [x] Ambiguity Check status is PASS for candidate review.
- [x] Human implementation approval has been given and recorded.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes or human-approved exceptions are documented.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged via Unity PR #92. Exact-head PR CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28325537773. Post-merge main CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28326050382.


## Merge evidence

- Unity PR: https://github.com/myriwe-bot/neon-champions-unity/pull/92
- Merge commit: `74badf31fc10a91dbd8723242263be6d39b94711`
- Exact-head PR CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28325537773
- Post-merge main CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28326050382
- Evidence: `production/evidence/STORY-TERRAIN-003/README.md` in the Unity repo.
