---
title: STORY-MAP-REAL-001 Scenario-Authored Strategic Map Shell
type: story
status: ready
phase: production
owner: shared
created: 2026-06-26
updated: 2026-06-26
source_lore: [greenland, blue-monday, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction,
    production/planning/strategic-map-realism-brief-2026-06-25,
    design/gdd/strategic-map,
    design/research/homm-like-strategic-map-topology-reference,
    design/research/homm-town-building-reference,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-MAP-REAL-001 Scenario-Authored Strategic Map Shell

## Status

READY / approved. Human approval recorded 2026-06-26 from chat: `Approved`. This story is the current Unity implementation packet for EPIC-009.

## Story type

Data + Presentation Foundation + Validation.

## Parent epic

- [EPIC-VSLICE-MVP-009 Strategic Map Geography, Bases, and Facility Construction](../epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction.md)

## User/player/system value

As a designer and player, I want the strategic map to be scenario-authored through explicit map/base/site/node definitions rather than hardcoded prototype labels, so that the current graph-based loop can support clearer geography, future map-editor workflows, and later base-facility stories without rewriting foundations.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §§1-8 for MVP direction, first scenario shape, data/state, and strategic map UX/readability requirements.
  - `design/gdd/strategic-map.md` §9 for approved authored node-route graph topology presented over visual geography.
  - `design/gdd/strategic-map.md` §10 for site categories, infrastructure/theme types, site runtime states, and site mix targets.
  - `design/gdd/strategic-map.md` §12 for base/facility authoring posture: base IDs, node IDs, scenario-authored display/localization keys, and validation-first editor compatibility.
  - `design/gdd/strategic-map.md` §16 acceptance criteria for scenario-authored base/facility data and serialization readiness.
- Research / planning:
  - `design/research/homm-like-strategic-map-topology-reference.md` for graph-backed map presentation and site readability lessons.
  - `design/research/homm-town-building-reference.md` for why base/town definitions must support future facilities/dwellings without importing a full town tree now.
  - `production/planning/strategic-map-realism-brief-2026-06-25.md` EPIC-009 planning decisions: graph rules preserved, scenario-authored names, validation now, no editor UI.
- ADR / architecture / control-manifest:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation tasks authorized by this story:

- Add or formalize scenario-authored strategic map definition fields sufficient for:
  - stable map ID;
  - scenario-authored display/localization key;
  - optional visual/background/theme key;
  - strategic nodes with stable IDs, node type, presentation coordinates, display/localization keys, and optional site/base references;
  - strategic routes with stable IDs, endpoint node IDs, movement cost, route type, and optional presentation/readability metadata;
  - base definitions attached to starting-hub nodes, with stable base IDs, owning faction, display/localization key, visual theme key, and starting/current facility reference placeholders if cheap/inert;
  - site definitions remaining graph-attached and scenario-authored rather than hardcoded.
- Add validation for scenario-authored map/base/site data, including at minimum:
  - duplicate IDs;
  - missing display/localization keys;
  - route endpoint references to missing nodes;
  - base references to missing nodes;
  - site/base collisions that violate current rules;
  - invalid or out-of-range presentation coordinates where current code can validate them.
- Migrate the current prototype strategic map data to the scenario-authored definition shape without changing the approved movement/topology rules.
- Preserve current node-route movement, Champion placement, site interaction, recruitment, tactical handoff, and objective behavior unless a tiny adapter is required to consume the new data definitions.
- Update strategic map labels/presentation to read from scenario-authored display/localization keys where practical.
- Add tests and evidence that authored definitions drive the map shell and that invalid authored data fails clearly.

## Out of scope

Not authorized by this story:

- No base facility construction UI or build action. That belongs to `STORY-BASE-001`.
- No resource-costed buildings yet.
- No income-chain behavior yet.
- No recruitment/dwelling stock refresh changes yet.
- No starting-base capture, siege, or garrison management.
- No full map editor UI.
- No procedural map generation.
- No hex/tile/freeform movement rewrite.
- No full geography art replacement or final map art.
- No strategic AI.
- No new victory condition.
- No broad balance changes.

## Allowed stubs, mocks, placeholders, or temporary data

- Placeholder visual/background/theme keys are allowed if data-driven and documented.
- Prototype coordinates/layout values are allowed.
- Existing scenario labels may be carried forward as localization/display keys, but they must not remain hardcoded in presentation logic if touched by this story.
- Facility references may be added as inert/empty placeholders only to support later `STORY-BASE-001`; no active construction behavior is allowed.
- Final map art and final icon assets are not required.

## Dependencies

- Required prior stories:
  - EPIC-008 is DONE / closed.
  - EPIC-007 is DONE / closed and supplies the previous strategic-map presentation baseline.
- Required data/assets:
  - Existing strategic map scene/data and current two-faction scenario definitions.
- Required architecture decisions:
  - Existing Unity technical scheme, control manifest, testing strategy, and CI build automation.
- Required Unity/package setup:
  - Existing Unity project and Unity Foundation CI.

## Acceptance criteria

- [ ] A scenario-authored strategic map definition exists or is formalized with stable IDs for map, nodes, routes, sites, and starting bases.
- [ ] Base/town/site/node display text is represented through scenario-authored display/localization keys or equivalent data, not hardcoded presentation strings in newly touched code.
- [ ] The current prototype scenario still loads and plays with the same graph movement/topology rules after data migration.
- [ ] Champion movement still uses node-route graph connectivity and route costs; no tile/hex/freeform movement is introduced.
- [ ] Site interaction, recruitment, tactical battle handoff, and objective flow are not intentionally changed by this story.
- [ ] Validation catches duplicate map/node/route/site/base IDs and references to missing nodes/sites/bases.
- [ ] Validation catches missing required display/localization keys for authored map, base, node, and site definitions where those objects are player-visible.
- [ ] Invalid authored data fails clearly in tests or validation output rather than silently falling back to hardcoded prototype data.
- [ ] Starting bases are represented as authored base definitions attached to starting-hub nodes, but cannot be captured and have no active facility construction behavior yet.
- [ ] Evidence shows the strategic map rendering/labels are driven by authored scenario data for at least the current starting bases and several sites/nodes.

## Verification requirements

- Unit tests: Required for map/base/site definition validation and lookup behavior.
- Unity edit-mode tests: Required where current architecture loads strategic map definitions or validates scenario data in Unity.
- Unity play-mode tests: Required if existing PlayMode smoke can verify current strategic loop still loads, moves, and enters tactical handoff after migration.
- Integration/data validation tests: Required for invalid ID/reference/display-key cases.
- Manual Unity scene/prefab checks: Supplemental only; required if labels/visual map shell cannot be fully asserted automatically.
- Screenshot/video evidence: Required PNG or short capture evidence under `production/evidence/STORY-MAP-REAL-001/` in the Unity repo showing authored base/site/node labels or map shell in play.
- Performance budget or N/A: N/A; story is data/presentation foundation, no large map generation.
- CI evidence: Unity Foundation CI exact-head before merge and post-merge main CI.
- Playtest evidence, if applicable: N/A for this first shell story; QA/playtest closeout occurs later in EPIC-009.
- TDD evidence required? Yes for validators/lookups and migration-safe behavior.
- Automation deferred? No broad exception approved; UI-only label evidence may be manual/PNG if not practical to assert automatically.

## Ambiguity Check

Status: PASS. Human approval recorded 2026-06-26.

Human-approved answers:

- Approved this story as the first EPIC-009 implementation packet.
- Approved the listed scope, assumptions, exclusions, and allowed placeholders as written.

Assumptions:

- Existing prototype map content may keep provisional labels as data/localization keys; this story does not make those names hard canon.
- Facility slots/references may be modeled now only if inert and useful for later stories.
- The story should prefer adapting existing data structures over large architecture rewrites.

Out of scope:

- Active base construction, income, recruitment/dwelling refresh, capture/siege, editor UI, topology rewrite, and final art.

Allowed stubs/mocks:

- Placeholder visual/theme keys.
- Prototype coordinates.
- Inert facility placeholders only.

Human-approved exceptions:

- None.

## Branch / PR requirements

- Branch name: `story/STORY-MAP-REAL-001-scenario-authored-strategic-map-shell`
- PR title: `STORY-MAP-REAL-001 Scenario-authored strategic map shell`
- Required linked story ID: `STORY-MAP-REAL-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md` §§1-10, §12, §16.
  - `design/research/homm-like-strategic-map-topology-reference.md`.
  - `design/research/homm-town-building-reference.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Domain/Application/Presentation/Tests/Evidence directories.
- Required evidence summary: tests run, validation cases, PlayMode/smoke result, PNG/manual evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked.
- [x] Exact ADR/architecture/control-manifest source is linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/reference sources are linked.
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

READY / approved for Unity implementation.
