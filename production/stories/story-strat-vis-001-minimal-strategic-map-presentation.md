---
title: STORY-STRAT-VIS-001 Minimal Strategic Map Presentation
type: story
status: in-review
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-02
source_lore: []
related: [design/gdd/strategic-map, docs/architecture/unity-technical-scheme, docs/architecture/control-manifest, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, production/epics/epic-strat-mvp-001-strategic-mvp-core-loop, production/stories/story-strat-001-scenario-map-graph-state, production/stories/story-strat-002-hotseat-turn-ownership, production/stories/story-strat-003-champion-route-movement]
approval: pending
---

# Story: STORY-STRAT-VIS-001 Minimal Strategic Map Presentation

## Status

READY-candidate. Requires explicit human approval before Codex implementation.

## Story type

Visual/Feel + Integration.

Primary layer: Unity presentation adapter for the existing strategic-domain scenario graph and runtime state.

## Parent epic

- Epic ID/path: [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].

## User/player/system value

As a player, I want to see the strategic scenario as a crude but readable node-route map with Champions and turn state, so that the team can test the player loop early instead of building invisible domain systems for too long.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §2 Approved MVP Direction, rules 1-8.
  - `design/gdd/strategic-map.md` §3 First Scenario Shape, rules 1-6 and working first-map content budget.
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 1-4 and 9-10 as display context only.
  - `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft, especially active faction, active Champion, reachable sites, site ownership/control/guarded state, whose turn is next.
  - `design/gdd/strategic-map.md` §9 Strategic Map Topology, rules 1-8 and MVP data implications, especially presentation coordinates.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` §Core Technical Principle, §Project Layout Standard, §Assembly Boundary Standard.
  - `docs/architecture/control-manifest.md` §§1, 2, 3, 4, 5, 6, 9, 10.
  - `docs/architecture/testing-strategy.md` — PlayMode/smoke and story-type evidence requirements.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - UX readability only. No final art direction, lore names, or content expansion is authorized.

## In scope

- Create or update one minimal strategic-map Unity scene suitable for local PlayMode/manual smoke testing.
- Add a thin presentation layer that reads an existing scenario definition/runtime state and renders:
  - strategic nodes as crude placeholder shapes;
  - routes as simple lines or equivalent crude connectors;
  - one Champion marker per faction;
  - active faction / active Champion indication;
  - basic site state indication if the current domain data exposes it, using placeholder color/icon/text only.
- Use existing presentation coordinates from scenario graph data if available. If unavailable, add minimal presentation-coordinate support only if compatible with STORY-STRAT-001's data model and validation rules.
- Add a lightweight scene bootstrap that initializes the approved/test-local MVP scenario runtime for visual testing.
- Keep domain rules in existing domain/application services; presentation must not own movement/turn rules.
- Add PlayMode or smoke automation where feasible to prove the scene loads and expected visual adapters/markers exist.
- Provide manual evidence requirement: screenshot or short video showing the crude map, nodes/routes, Champion markers, and active faction display.

## Out of scope

- Player movement input, click handling, drag handling, keyboard controls, or end-turn input.
- Tactical battle scene, site interaction, rewards, recruitment, victory evaluation, or battle result application.
- Final art, final Greenland map, terrain, animations, VFX/audio, camera polish, accessibility polish, localization implementation, or UI skinning.
- New gameplay content, lore names, balance, map expansion, or final data-authoring pipeline.
- Save/load, map editor, package changes, or architecture changes beyond a thin presentation adapter.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder primitive shapes, colors, labels, and scene object names.
- Test-local scenario fixture from STORY-STRAT-001.
- Minimal bootstrap object for the visual smoke scene.

Not allowed:

- Presentation code that mutates domain state except through approved application services.
- Hidden gameplay behavior such as auto-movement, auto-site interaction, rewards, or turn advancement.
- Final-content claims for placeholder visuals.

## Dependencies

- Required prior stories:
  - STORY-STRAT-001 scenario/map graph state implemented and merged or available on the implementation branch.
  - STORY-STRAT-002 hotseat turn ownership recommended before implementation so active faction display is meaningful.
  - STORY-STRAT-003 champion route movement may be implemented before or after this story, but this story must not implement movement input.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required Unity/package setup:
  - Existing Unity project, scene/test assemblies, and CI from SPIKE-001.

## Acceptance criteria

- [ ] Given the minimal strategic-map scene is opened/loaded, when the scene starts, then it initializes a valid two-faction scenario runtime from the approved/test-local scenario definition.
- [ ] Given the scenario graph contains nodes with presentation coordinates, when the scene renders, then each node has a visible placeholder marker at the expected relative position.
- [ ] Given the scenario graph contains authored routes, when the scene renders, then each route is visibly represented between its endpoint nodes.
- [ ] Given each faction has one Champion, when the scene renders, then each Champion marker appears at its current node.
- [ ] Given one faction is active, when the scene renders, then active faction/active Champion state is visibly distinguishable through placeholder label/color/marker.
- [ ] Given site state data is available, when nodes render, then site ownership/guarded/neutral state is represented with crude placeholder indicators; if unavailable, the PR records this as an omission and does not invent site rules.
- [ ] Presentation code depends on application/domain as allowed, but domain code remains free of UnityEngine, MonoBehaviour, scene, prefab, input, camera, and UI dependencies.
- [ ] A PlayMode/smoke test or documented automated substitute proves the scene loads and expected node/route/Champion marker counts exist.

## Verification requirements

- Unit tests: N/A unless pure presentation mapping helpers are added.
- Unity edit-mode tests: Required for any added presentation-coordinate/mapping helpers if practical.
- Unity play-mode tests: Required where feasible for scene load and marker-count smoke coverage.
- Manual Unity scene/prefab checks: Required.
- Screenshot/video evidence: Required.
- Performance budget or N/A: N/A for crude MVP visualization; no performance-sensitive rendering authorized.
- CI evidence: Required on implementation PR.
- Playtest evidence: Not required for this story, but scene must be suitable for upcoming player-loop smoke.
- TDD evidence required? Yes for production logic/helpers; PlayMode/manual evidence for scene wiring.
- Automation deferred? Only manual visual feel evidence may be manual; compile/scene smoke should not be skipped without documented exception.

## Ambiguity Check

Status: PASS.

Open questions:
- None for crude placeholder visualization.

Assumptions:
- The goal is early loop visibility, not final map art.
- Placeholder visual encoding is acceptable if it is readable and documented as temporary.

Out of scope:
- Same as story Out of scope section.

## Codex implementation notes

- Branch suggestion: `story/strat-vis-001-minimal-map-presentation`.
- Stop if implementing this requires changing scenario graph/domain ownership rules, adding packages, inventing final UI architecture, or deciding final map art/data authoring.
