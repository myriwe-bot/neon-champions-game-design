---
title: STORY-TERRAIN-005 Strategic Context to Tactical Battlefield Smoke
type: story
status: done
phase: production
owner: shared
created: 2026-06-28
updated: 2026-06-29
source_lore: [greenland, white-sky, digital-net]
related:
  [
    production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability,
    production/stories/story-terrain-001-strategic-terrain-tags-and-tactical-layout-family-contract,
    production/stories/story-terrain-002-tactical-layout-definitions-and-deployment-zones,
    production/stories/story-terrain-003-tactical-blockers-and-simple-defensive-terrain,
    production/stories/story-terrain-004-range-threat-and-terrain-readability-pass,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-TERRAIN-005 Strategic Context to Tactical Battlefield Smoke

## Status

DONE / merged. Unity PR #99 merged on 2026-06-29 as `08d7c66fffe4ad902a4e0a9c6f180765ad3dbdcf`. Merge-gate verdict: PASS. Exact-head PR Unity Foundation CI passed on `61f92d26d44427d0bd64e9cd847e82830c023c32` at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28351445229. Post-merge `main` Unity Foundation CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28352578645. Unity README current-task pointer cleanup merged in PR #100 with PR CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28353097517 and post-merge main CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28353377725.

## Story type

Integration Smoke + Readability.

## Parent epic

- [EPIC-VSLICE-MVP-010 Terrain, Tactical Battlefields, and Map-Space Readability](../epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability.md)

## User/player/system value

As a player, I want the strategic place I choose to attack to visibly carry through into the tactical battlefield layout and readability summary, so the strategic map and tactical board feel like one connected terrain system instead of isolated demos.

## Source requirements

- `STORY-TERRAIN-001` through `STORY-TERRAIN-004` are DONE and provide strategic terrain/context tags, tactical layout-family selection, deployment zones, blocked/defensive terrain cells, and range/threat/terrain readability output.
- `design/gdd/strategic-map.md` §§1-10 for graph-backed strategic map/site context and terrain identity.
- `design/gdd/tactical-combat.md` §§3-6 and §6.2A for tactical battlefields, deployment, terrain cells, movement/attack affordances, and readability.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, and `docs/architecture/ci-build-automation.md`.

## In scope

- Add or tighten a connected smoke path proving strategic site/terrain context selects the expected tactical layout family and carries the expected terrain context tags into the tactical snapshot.
- Show at least two strategic contexts/sites that launch into distinct tactical layout-family/readability outputs.
- Verify tactical presentation/evidence includes layout family, terrain context, deployment zones, blocked terrain, defensive terrain, legal moves, legal attack targets, and non-attackable/out-of-range enemies after the strategic-to-tactical handoff.
- Add focused regression tests that the strategic BattleSetup/handoff source data and tactical presentation snapshot stay aligned for those contexts.
- Add PlayMode/evidence screenshots or text evidence under `production/evidence/STORY-TERRAIN-005/`.

## Out of scope

- No new strategic map topology, nodes, routes, sites, factions, resources, facilities, recruitment offers, objectives, win/loss rules, battle-result rules, or strategic AI.
- No new tactical movement, attack, damage, AP, Defend, retaliation, Sensor Lock, CombatAI, battle-end, result-return, or objective mechanics.
- No elevation, line-of-sight rewrite, overwatch, destructible terrain, hazards, weather, fog, supply, strategic terrain movement costs, strategic topology rewrite, strategic AI terrain valuation, cover system, facing, ranged accuracy, broad balance changes, final art/icons/VFX/audio/localization, or map editor UI.

## Allowed stubs, mocks, placeholders, or temporary data

- Existing prototype strategic sites/context tags and tactical layout families may be reused.
- Prototype labels, colors, debug markers, and screenshot/evidence-only text are allowed if they are generated from real strategic handoff and tactical presentation state.
- No final UI polish is required.

## Dependencies

- Required prior stories: `STORY-TERRAIN-001`, `STORY-TERRAIN-002`, `STORY-TERRAIN-003`, and `STORY-TERRAIN-004` DONE / merged.
- Required Unity CI: post-merge main CI for `STORY-TERRAIN-004` passed.
- Required data: strategic terrain/context tags, tactical layout-family IDs, authored tactical layout definitions, deployment zones, blocked/defensive terrain cells, and range/threat/terrain readability summaries.

## Acceptance criteria

- [x] At least two strategic site/context paths launch tactical battles with distinct tactical layout-family IDs.
- [x] Each covered handoff carries expected strategic terrain context tags into `BattleSetup` and tactical presentation snapshots.
- [x] Each covered tactical snapshot/evidence shows layout family, terrain context, deployment zones, blocked terrain, defensive terrain, movement range/legal moves, attack range/legal targets, and out-of-range/non-attackable enemies.
- [x] Strategic-to-tactical handoff tests use real runtime state/projection paths rather than hardcoded presentation-only demo strings.
- [x] Existing terrain stories remain intact; no new mechanics are introduced outside integration smoke/readability evidence.
- [x] Evidence distinguishes this integration smoke from future strategic terrain movement costs, supply, weather, fog, LoS/cover, hazard, objective, and AI systems.

## Verification requirements

- EditMode tests for strategic handoff/BattleSetup context and tactical snapshot alignment across at least two contexts.
- PlayMode smoke or equivalent evidence proving visible strategic-to-tactical transition/readability for at least two contexts.
- PNG or text evidence under `production/evidence/STORY-TERRAIN-005/`.
- Exact-head Unity Foundation CI before merge and post-merge main CI before marking DONE.

## Ambiguity Check

Status: PASS.

Open questions:

- None blocking for candidate drafting. The intended default is connected smoke/readability only, not new mechanics or map content.

Assumptions:

- Reuse existing scenario-authored sites/context tags where possible.
- Prefer asserting existing handoff data and presentation outputs over adding new content.
- The smoke should prove the terrain pipeline is connected, not introduce final terrain design/balance.

Out of scope:

- New mechanics, content expansion, cover/LoS/elevation/hazards/weather/fog/supply/strategic terrain movement rules/final art.

Allowed stubs/mocks:

- Prototype labels, colors, debug/evidence markers generated from real runtime state.

Human-approved answers:

- Approved 2026-06-28 via user instruction: "aPPROVED".
- Use the story's listed assumptions, exclusions, allowed placeholders, branch/PR requirements, and verification requirements as the implementation contract.
- Keep this story integration-smoke/readability-only; do not add new strategic or tactical mechanics.

## Branch / PR requirements

- Branch name: `story/STORY-TERRAIN-005-strategic-context-tactical-battlefield-smoke`
- PR title: `STORY-TERRAIN-005 Strategic context to tactical battlefield smoke`
- Required linked story ID: `STORY-TERRAIN-005`.
- Required evidence summary: tests run, at least two strategic contexts/sites, layout-family/context alignment, range/threat/terrain readability output, evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest source is linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied once TERRAIN-004 merge evidence is recorded.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [x] Ambiguity Check status is PASS for candidate review.
- [x] Human implementation approval has been given and recorded.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists under Unity `production/evidence/STORY-TERRAIN-005/`.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass. Exact-head PR CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28351445229. Post-merge main CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28352578645.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete: Unity PR #99.
- [x] CI passes.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged. Unity PR #99: https://github.com/myriwe-bot/neon-champions-unity/pull/99. Merge commit: `08d7c66fffe4ad902a4e0a9c6f180765ad3dbdcf`. Exact-head CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28351445229. Post-merge main CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28352578645. Unity README current-task pointer cleanup: PR #100, PR CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28353097517, post-merge CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28353377725. No known implementation blocker remains; EPIC-010 should move to QA/playtest closeout review.
