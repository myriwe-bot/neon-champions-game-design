---
title: STORY-TERRAIN-004 Range, Threat, and Terrain Readability Pass
type: story
status: draft
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
    production/stories/story-terrain-003-tactical-blockers-and-simple-defensive-terrain,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-TERRAIN-004 Range, Threat, and Terrain Readability Pass

## Status

READY-candidate / approval pending. This is the proposed next EPIC-010 Unity implementation packet after `STORY-TERRAIN-003`; no Unity implementation is authorized until a human explicitly promotes this story to READY / approved.

## Story type

Tactical UI + Playability.

## Parent epic

- [EPIC-VSLICE-MVP-010 Terrain, Tactical Battlefields, and Map-Space Readability](../epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability.md)

## User/player/system value

As a player, I want the tactical board to clearly show movement range, attack range/threat, terrain context, and why a hex or target is/not actionable, so blocked and defensive terrain become readable play spaces rather than debug labels.

## Source requirements

- `STORY-TERRAIN-001` through `STORY-TERRAIN-003` are DONE and provide terrain/context tags, selected layout families, deployment zones, blocked cells, defensive cells, and terrain-cell presentation hooks.
- `design/gdd/tactical-combat.md` §§3-6 and §6.2A for flat tactical boards, movement/attack affordances, and tactical battlefield readability.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, and `docs/architecture/ci-build-automation.md`.

## In scope

- Improve existing tactical presentation snapshots/UI/debug text so the active stack's legal movement, attack targets, attack range, and non-attackable enemies are readable together with terrain cells.
- Surface blocked cells as explicitly non-movable / non-occupiable in player-facing labels or summaries.
- Surface defensive cells as readability-only prototype terrain cells, not combat cover, unless a later approved story changes that.
- Add concise terrain/range/threat summaries that connect selected layout family, deployment zones, blocked terrain, defensive terrain, current stack, legal moves, legal targets, and out-of-range enemies.
- Add regression tests for presentation snapshot consistency and UI-visible text for at least two layout-family contexts.
- Add PlayMode/evidence screenshots or text evidence under `production/evidence/STORY-TERRAIN-004/` showing range/threat/readability output with terrain cells.

## Out of scope

- No new movement, attack, damage, AP, Defend, retaliation, Sensor Lock, CombatAI, battle-end, strategic result, or objective mechanics.
- No elevation, line-of-sight rewrite, overwatch, destructible terrain, hazards, weather, fog, supply, strategic terrain movement costs, strategic topology changes, or strategic AI terrain valuation.
- No full cover system, facing rules, ranged accuracy rules, broad damage formula changes, or terrain-based balance pass.
- No final art/icons/VFX/audio/localization.
- No map editor UI.

## Allowed stubs, mocks, placeholders, or temporary data

- Prototype text, colors, simple markers, and debug labels are allowed.
- Screenshot/evidence-only UI labels are allowed if they are generated from real presentation snapshot state.
- No final UI polish is required.

## Dependencies

- Required prior story: `STORY-TERRAIN-003` DONE / merged.
- Required Unity CI: post-merge main CI for `STORY-TERRAIN-003` passed.
- Required data: tactical layout families, deployment zones, blocked/defensive terrain cells, existing legal-move and legal-attack calculations.

## Acceptance criteria

- [ ] Active-stack movement range and legal movement destinations are visible/readable in presentation snapshots and UI/evidence.
- [ ] Active-stack attack range, legal attack targets, and out-of-range/non-attackable enemies are visible/readable in presentation snapshots and UI/evidence.
- [ ] Blocked terrain is clearly presented as not movable/occupiable and does not appear as a legal movement destination.
- [ ] Defensive terrain is clearly presented as readability-only prototype terrain, with no implied cover/damage effect.
- [ ] At least two layout-family contexts produce evidence showing terrain plus range/threat/readability output.
- [ ] Existing tactical mechanics remain unchanged outside presentation/readability and evidence surfaces.
- [ ] Evidence and tests distinguish this readability pass from future LoS/cover/hazard systems.

## Verification requirements

- EditMode tests for presentation snapshot summaries/markers in at least two terrain layout-family contexts.
- PlayMode smoke or equivalent evidence proving UI-visible range/threat/readability text/markers with blocked and defensive terrain.
- PNG or text evidence under `production/evidence/STORY-TERRAIN-004/`.
- Exact-head Unity Foundation CI before merge and post-merge main CI before marking DONE.

## Ambiguity Check

Status: PASS for READY-candidate review; implementation remains blocked until human approval.

Open questions:

- None blocking for candidate drafting. The intended default is presentation/readability-only, not new mechanics.

Assumptions:

- Use existing tactical board, movement, attack, terrain-cell, and presentation snapshot data.
- Prefer adding/clarifying labels and summaries over adding new interaction modes.
- Existing legal-move/legal-attack calculations remain authoritative.

Out of scope:

- Cover/LoS/elevation/hazards/weather/fog/supply/strategic movement terrain rules/final art.

Allowed stubs/mocks:

- Prototype labels, colors, and debug/evidence markers.

## Branch / PR requirements

- Branch name: `story/STORY-TERRAIN-004-range-threat-terrain-readability-pass`
- PR title: `STORY-TERRAIN-004 Range threat and terrain readability pass`
- Required linked story ID: `STORY-TERRAIN-004`.
- Required evidence summary: tests run, at least two layout-family contexts, range/threat/readability output, evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked.
- [x] Exact ADR/architecture/control-manifest source is linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied once TERRAIN-003 merge evidence is recorded.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [x] Ambiguity Check status is PASS for candidate review.
- [ ] Human implementation approval has been given and recorded.

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

READY-candidate / approval pending. Guarded Codex prompt prepared at `production/sprints/codex-story-terrain-004.prompt.txt`; it must self-block until human approval promotes this story to READY / approved.
