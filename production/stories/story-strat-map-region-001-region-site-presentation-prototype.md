---
title: STORY-STRAT-MAP-REGION-001 Region/Site Presentation Prototype
type: story
status: done
phase: production
owner: shared
created: 2026-06-18
updated: 2026-06-18
source_lore: [greenland, white-sky, digital-net]
related:
  [
    production/epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation,
    production/stories/story-strat-read-002-strategic-map-readability-pass,
    production/stories/story-strat-base-001-starting-hub-reinforcement-preview,
    design/gdd/strategic-map,
    design/research/homm-like-strategic-map-topology-reference,
    production/planning/prototype-readability-and-map-next-steps-2026-06-15,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-STRAT-MAP-REGION-001 Region/Site Presentation Prototype

## Status

DONE / merged. Human approval recorded 2026-06-18 from chat: `STORY-STRAT-MAP-REGION-001 approved`. Unity PR #57 merged 2026-06-18 as `ffe1dd68c61faa897f0ae4021b61aa12d77df924`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27759022977

Approved scope was one region/site presentation prototype that makes the current graph-backed strategic map look and read more like a spatial HoMM-like map, while preserving the existing node-route rules and avoiding full tile/hex movement, pathfinding, fog, map editor, procedural generation, final art, or new strategic mechanics.

## Story type

Strategic Presentation + Data / Region-Site Map Prototype.

## Parent epic

- [EPIC-VSLICE-MVP-007 Strategic Map Readability, Bases, and Spatial Presentation](../epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation.md)

## User/player/system value

As a player, I want the strategic layer to read as a map of regions, corridors, bases, guarded sites, and ownership instead of a pure node diagram, so movement and site stakes feel more HoMM-like without forcing a premature tile/hex rewrite.

## Source requirements

Exact source references:

- Parent epic:
  - `production/epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation.md` region/site presentation scope and child target.
- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §§1-8 for MVP direction, core loop, first scenario, and readability goals.
  - `design/gdd/strategic-map.md` §9 for approved node-route topology and future tile/grid/region compatibility.
  - `design/gdd/strategic-map.md` §10 for site categories, ownership/control/guarded state, and site presentation responsibilities.
  - `design/gdd/strategic-map.md` §§11-13 only as read-only context for resources/recruitment, movement, and turn/scenario state already surfaced in map UI.
- References:
  - `design/research/homm-like-strategic-map-topology-reference.md` Option B region map with embedded sites and recommended phased path.
  - `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` Region/site map evolution direction and non-recommendations.
- ADR / architecture / control:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Prior prerequisites:
  - `STORY-STRAT-READ-002` DONE / merged.
  - `STORY-STRAT-BASE-001` DONE / merged.

## In scope

Concrete implementation tasks proposed by this story:

- Add lightweight presentation data or derived presentation fields that let the existing strategic nodes/sites render as named regions/sites/corridors while preserving graph rules internally.
- Make start hubs, recruitment sites, resource/cache sites, guarded sites, central objective, and routes read spatially through clear map labels, markers, ownership color/region tint, guarded markers, and road/corridor presentation.
- Show current active Champion, selected Champion, reachable destinations, path-cost/readability, selected site state, and available interaction in the region/site presentation.
- Keep existing click/select/move/recruit/reinforce/attack/engage/field-upgrade affordances working after the presentation change.
- Add tests that verify graph topology and command semantics are unchanged while presentation fields/markers are present and non-overlapping enough for 1280x720 PlayMode smoke evidence.
- Add PNG evidence under `production/evidence/STORY-STRAT-MAP-REGION-001/` showing initial map, selected/reachable map, and at least one selected site/interaction preview in the region/site presentation.

## Out of scope

Not authorized by this story:

- No square/hex strategic tile movement.
- No freeform movement, terrain pathfinding, diagonal movement, road movement modifiers, weather, logistics, supply, fog, scouting, or strategic AI.
- No procedural map generation or map editor.
- No new economy, recruitment stock rules, base/town-building systems, garrisons, reserves/caravans, unit roster/balance, or tactical rules.
- No final map art, final icons, VFX, audio, animation, localization, or lore/content rewrite.
- No replacement of the existing node-route graph as the rules substrate.

## Allowed stubs, mocks, placeholders, or temporary data

- Prototype region names, region IDs, corridor/road labels, tint colors, and marker shapes are allowed.
- Existing node/site IDs may remain visible in diagnostics/tests, but player-facing labels should be clearer than raw IDs where practical.
- Simple authored/derived presentation coordinates or region groupings are allowed if they are deterministic and future tile/hex compatible.

## Dependencies

- Required prior stories:
  - `STORY-STRAT-READ-002` DONE / merged.
  - `STORY-STRAT-BASE-001` DONE / merged.
- Required data/assets:
  - Existing strategic graph, nodes, routes, sites, runtime state, strategic UI/presentation surfaces.
- Required architecture decisions:
  - Existing Unity technical scheme/control manifest; no new ADR required if graph remains authoritative.
- Required Unity/package setup:
  - Existing Unity project and CI.

## Acceptance criteria

- [ ] The strategic map visibly reads as a region/site/corridor prototype rather than only a node diagram at 1280x720.
- [ ] Start hubs, recruitment site, resource/cache/guarded sites, central objective, and routes/corridors have distinct readable presentation.
- [ ] Ownership/control, guarded state, active Champion, selected Champion, reachable destinations, and selected site interaction are visible without relying only on raw node IDs.
- [ ] Existing graph movement semantics are unchanged: route costs, reachable destinations, movement commit, site selection, recruitment, starting-hub reinforcement, guarded battle launch/return, objective/field-upgrade/champion encounter smoke paths remain green.
- [ ] Pointer/button interaction still works for map markers and command controls.
- [ ] Presentation additions are deterministic and covered by EditMode/PlayMode tests where practical.
- [ ] Evidence PNGs show initial/selected/reachable/site-preview region-site presentation.

## Verification requirements

- Unity edit-mode tests: Required for any new presentation data projection/validation and for graph-semantics no-regression where practical.
- Unity play-mode tests: Required for visible region/site/corridor markers, non-overlap/basic readability at 1280x720, and existing core interaction no-regression.
- Integration/data validation tests: Existing placeholder validator must remain green; add validation only if new authored data files are introduced.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-STRAT-MAP-REGION-001/` in the Unity repo.
- CI evidence: Unity Foundation CI exact-head before merge.
- TDD evidence required? Yes for presentation projection and command no-regression where practical.
- Automation deferred? No broad exception approved.

## Ambiguity Check

Status: PASS. Human approval recorded 2026-06-18.

Human-approved answers:

1. Approved as the next implementation packet.
2. Approved region/site hybrid direction as a presentation/data pass only, not a topology rewrite.

Approved assumptions:

- The graph remains the authoritative strategic rules substrate.
- The story may add lightweight presentation fields/markers/labels/tints/coordinates if deterministic and future-compatible.
- The story should improve map readability through spatial grouping and labels, not introduce new mechanics.

Out of scope:

- Tile/hex movement, terrain pathfinding, procedural/map editor work, fog/logistics/weather/supply, strategic AI, new economy/base/tactical systems, final art/content.

Allowed stubs/mocks:

- Prototype region/corridor names, colors, marker shapes, and presentation coordinates.

Human-approved exceptions:

- None. Story scope remains presentation/data only and does not authorize a topology rewrite.

## Branch / PR requirements

- Branch name: `story/STORY-STRAT-MAP-REGION-001-region-site-presentation-prototype`.
- PR title: `STORY-STRAT-MAP-REGION-001 Region/site presentation prototype`.
- Required linked story ID: `STORY-STRAT-MAP-REGION-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md`.
  - `design/research/homm-like-strategic-map-topology-reference.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Application/Presentation/Tests/Evidence directories.
- Required evidence summary: tests run, PlayMode/PNG evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists: `production/evidence/STORY-STRAT-MAP-REGION-001/` in the Unity repo.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented in Unity PR #57.
- [x] PR/code review is complete: https://github.com/myriwe-bot/neon-champions-unity/pull/57
- [x] CI passes: PR exact-head Unity Foundation CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27758159262 and post-merge main CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27759022977
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged.
