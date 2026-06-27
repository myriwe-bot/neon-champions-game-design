---
title: STORY-TERRAIN-002 Tactical Layout Definitions and Deployment Zones
type: story
status: ready
phase: production
owner: shared
created: 2026-06-27
updated: 2026-06-27
source_lore: [greenland, white-sky, digital-net]
related:
  [
    production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability,
    production/stories/story-terrain-001-strategic-terrain-tags-and-tactical-layout-family-contract,
    design/gdd/tactical-combat,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-TERRAIN-002 Tactical Layout Definitions and Deployment Zones

## Status

READY / approved for Unity implementation. Human approval recorded 2026-06-27: "Approved next story". This approves the listed scope, assumptions, exclusions, allowed placeholders, branch/PR requirements, and verification requirements as written.

Human-approved answers:

- The listed prototype layout families are sufficient for this story: `server_yard`, `fortified_approach`, `open_route_clash`, and `infrastructure_hub`.
- Deployment-zone presentation may be implemented with readable labels/markers where practical; text/debug evidence is acceptable for this packet if the zones are visible/testable and the extension point for later terrain cells remains clean.

## Story type

Tactical Data + Presentation.

## Parent epic

- [EPIC-VSLICE-MVP-010 Terrain, Tactical Battlefields, and Map-Space Readability](../epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability.md)

## User/player/system value

As a player, I want the tactical battle screen to use authored battlefield layout definitions and visible deployment zones selected by the layout family, so fights no longer feel like the same abstract board regardless of strategic context.

## Source requirements

- `production/stories/story-terrain-001-strategic-terrain-tags-and-tactical-layout-family-contract.md` is DONE and provides `TacticalLayoutFamilyId` plus selected terrain/context tags on battle setup.
- `design/gdd/tactical-combat.md` §§3-6 and §6.2A for flat hex board, strategic battle context, and EPIC-010 tactical battlefield/layout family contract.
- `design/gdd/strategic-map.md` §9.5 for strategic terrain/context feeding battle setup.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, and `docs/architecture/ci-build-automation.md`.

## In scope

- Add tactical layout definition data keyed by the existing prototype layout family IDs, at minimum:
  - `server_yard`;
  - `fortified_approach`;
  - `open_route_clash`;
  - `infrastructure_hub`.
- Define authored board dimensions or board template identity per layout family using current tactical board architecture.
- Define attacker and defender deployment zones for each layout family.
- Update tactical board creation so battle setup `TacticalLayoutFamilyId` selects the corresponding authored layout definition.
- Surface the active layout family and deployment-zone identity in tactical presentation/evidence.
- Add validation for missing/unknown layout definition IDs, duplicate layout definitions, and missing/invalid deployment zones.
- Add tests proving at least two layout families create distinct deployment patterns from battle setup.
- Preserve existing tactical movement, attack, AP, Defend, retaliation, command, CombatAI, battle result, and strategic result-return behavior.

## Out of scope

- No blockers, cover/defensive terrain, hazards, elevation, line-of-sight rewrite, overwatch, destructible terrain, weather, fog, supply, strategic terrain movement costs, or strategic topology changes.
- No new units, abilities, Champion Operations, resources, sites, objectives, base/facility rules, AI strategy, or balance changes.
- No final art/icons/VFX/audio/localization.
- No map editor UI.

## Allowed stubs, mocks, placeholders, or temporary data

- Prototype layout templates and deployment-zone labels are allowed.
- Simple deterministic authored coordinates are allowed.
- Debug/evidence-only visualization is allowed if production UI is not ready.
- Existing flat board visuals may remain crude if zones are readable and testable.

## Dependencies

- Required prior story: `STORY-TERRAIN-001` DONE / merged.
- Required Unity CI: post-merge main CI for `STORY-TERRAIN-001` passed.
- Required data: existing battle setup DTO with `TacticalLayoutFamilyId` and selected terrain/context tags.

## Acceptance criteria

- [ ] Battle setup `TacticalLayoutFamilyId` selects an authored tactical layout definition, not a hardcoded one-off presentation switch.
- [ ] At least two current layout families produce visibly/testably distinct deployment-zone patterns.
- [ ] Attacker and defender deployment zones are represented in tactical board state or presentation snapshots.
- [ ] Unknown or missing layout definitions fail validation clearly.
- [ ] Existing tactical loop behavior remains intact.
- [ ] Evidence shows selected layout family plus attacker/defender deployment zones for at least two contexts.
- [ ] The implementation leaves a clean extension point for `STORY-TERRAIN-003` blockers and simple defensive terrain.

## Verification requirements

- Unit/EditMode tests for layout definition validation and layout-family selection.
- EditMode tests for deployment-zone assignment and invalid definitions.
- PlayMode smoke or equivalent presentation evidence showing at least two selected layout families with deployment-zone output.
- PNG or text evidence under `production/evidence/STORY-TERRAIN-002/`.
- Exact-head Unity Foundation CI before merge and post-merge main CI before marking DONE.

## Ambiguity Check

Status: PASS.

Open questions:

- None.

Assumptions:

- Use existing flat tactical board architecture.
- Keep deployment zones mechanically minimal: placement/start-zone authoring only, not terrain rules.
- Prefer deterministic authored definitions over procedural generation.

Out of scope:

- Blockers, cover, hazards, tactical terrain cell effects, strategic movement terrain rules, weather, fog, supply, final art.

Allowed stubs/mocks:

- Prototype coordinates, labels, and crude markers.

Human-approved answers:

- Approved 2026-06-27 via user instruction: "Approved next story".
- Use the four listed prototype layout families unless implementation discovers a concrete blocker; if so, report the blocker rather than silently deferring one.
- Text/debug evidence is acceptable when paired with tests and readable presentation output; do not add full terrain-cell mechanics.

## Branch / PR requirements

- Branch name: `story/STORY-TERRAIN-002-tactical-layout-definitions-deployment-zones`
- PR title: `STORY-TERRAIN-002 Tactical layout definitions and deployment zones`
- Required linked story ID: `STORY-TERRAIN-002`.
- Required evidence summary: tests run, at least two layout-family contexts, deployment-zone output, evidence path, CI URL.
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
- [x] Ambiguity Check status is PASS.
- [x] Human implementation approval has been given and recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY / approved for Unity implementation. Runnable Codex prompt prepared at `production/sprints/codex-story-terrain-002.prompt.txt`.
