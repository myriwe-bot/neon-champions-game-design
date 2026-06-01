---
title: STORY-STRAT-001 Scenario Map Graph State
type: story
status: approved
phase: production
owner: shared
created: 2026-05-30
updated: 2026-06-01
source_lore: [greenland, blue-monday, white-sky, digital-net]
related: [design/gdd/strategic-map, docs/architecture/unity-technical-scheme, docs/architecture/control-manifest, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, production/epics/epic-strat-mvp-001-strategic-mvp-core-loop, production/stories/story-template]
approval: approved
---

# Story: STORY-STRAT-001 Scenario Map Graph State

## Status

READY.

This story is approved as the first strategic MVP implementation story. It may be assigned once the implementation repo branch/PR plan is confirmed and the implementer has read the Unity repo `AGENTS.md` and relevant source/test assembly layout.

## Story type

Logic + Config/Data.

Primary layer: pure strategic-domain data/state, with validation tests.

## Parent epic

- Epic ID/path: [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].
- Blocking? No. Parent epic exists and is approved.

## User/player/system value

As a system, I want a serializable two-faction strategic scenario definition and runtime state based on an authored node-route graph, so that later stories can implement hotseat turns, Champion movement, site interaction, and strategy-to-tactical battle handoff without inventing map/state structure.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §2 Approved MVP Direction, rules 1-8.
  - `design/gdd/strategic-map.md` §3 First Scenario Shape, rules 1-6 and working first-map content budget.
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 1-11.
  - `design/gdd/strategic-map.md` §7 Data and State Contract Draft, Scenario/Faction/Controller/Champion/Army/Site/Route/Resource rows.
  - `design/gdd/strategic-map.md` §9 Strategic Map Topology, rules 1-8 and MVP data implications.
  - `design/gdd/strategic-map.md` §10 Site and Infrastructure States, rules 1-8 and MVP site runtime states.
  - `design/gdd/strategic-map.md` §11 Resources, Intel, and Recruitment/Reinforcement Minimum, rules 1-7.
  - `design/gdd/strategic-map.md` §12 Champion/Army Strategic State and Movement Allowance, Champion/army state minimum.
  - `design/gdd/strategic-map.md` §13 Turn/Scenario/Victory Structure, scenario state minimum.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` — domain logic must be testable separately from Unity presentation; exact section to be re-read by implementer before coding.
  - `docs/architecture/control-manifest.md` §1 Implementation Authority.
  - `docs/architecture/control-manifest.md` §2 Source Reading Order.
  - `docs/architecture/control-manifest.md` §4 Architecture Boundaries.
  - `docs/architecture/control-manifest.md` §5 Data and Tuning.
  - `docs/architecture/control-manifest.md` §6 Testing and Verification.
  - `docs/architecture/control-manifest.md` §9 Git / GitHub Rules.
  - `docs/architecture/testing-strategy.md` §Required Test and Evidence Layers.
  - `docs/architecture/testing-strategy.md` §Story Type to Required Evidence Matrix.
  - `docs/architecture/testing-strategy.md` §TDD Requirement.
- UX/content/art rule, if applicable:
  - `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft, only as data support for future UI; no UI implementation in this story.
- Worldbuilding or design-bridge source, if lore-facing:
  - N/A for implementation behavior. Placeholder IDs/names may reference Greenland/White Sky flavor only if already present in GDD; no new lore decisions authorized.
- Parent epic:
  - [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].

## In scope

Concrete implementation tasks authorized by this story:

- Create pure domain definitions for MVP strategic scenario graph data:
  - `ScenarioDefinition` or equivalent.
  - `StrategicMapDefinition`.
  - `StrategicNodeDefinition`.
  - `StrategicRouteDefinition`.
  - `FactionDefinition` minimum reference shape.
  - `ControllerAssignment` or equivalent runtime assignment model for `HumanLocal`.
  - `SiteDefinition` minimum reference shape needed by map nodes.
  - `ResourceDefinition` minimum IDs for Credits, Materials, Intel.
  - `ChampionDefinition` minimum reference shape for starting Champions.
  - `ArmyTemplate` / `ArmyStackDefinition` minimum shape if needed for starting armies and guards.
- Create pure runtime state models for an initialized scenario:
  - `ScenarioRuntimeState`.
  - faction runtime state with resource stockpiles.
  - Champion runtime state with current node, movement fields, interaction availability, status flags, attached army.
  - site runtime state with owner/control/guarded/visited/consumed fields.
  - objective hold fields required by Packet G.
- Create an initializer/factory that builds a valid scenario runtime state from a static scenario definition.
- Create validation for static scenario definitions, including:
  - stable non-empty IDs;
  - unique node IDs;
  - unique route IDs;
  - route endpoints exist;
  - starting Champion placements reference existing nodes;
  - exactly two MVP factions for this story;
  - exactly one starting Champion per faction for this story;
  - each starting hub/site references valid node/faction IDs;
  - central objective site exists and is on a valid node;
  - resource definitions include Credits, Materials, Intel;
  - no unsupported active resource stockpiles are required.
- Add one representative hardcoded or test-local sample scenario definition for tests only, unless an approved data-authoring path already exists in the Unity repo.
- Ensure all domain/runtime state models are serializable-friendly plain C# objects/records/classes without Unity scene/prefab dependencies.

## Out of scope

Adjacent behavior not authorized by this story:

- Unity scene, map rendering, camera, input, HUD, or visual Greenland map presentation.
- Champion movement execution/pathfinding beyond storing current node and movement fields.
- Hotseat turn advancement logic beyond initial active faction fields.
- Site interaction behavior, claiming, recruiting, rewards, battle triggering, or tactical handoff.
- Tactical combat implementation.
- `BattleSetup` / `BattleResult` implementation, except references/placeholders needed to avoid circular design.
- Save/load system or final file format.
- Data editor, map editor, ScriptableObject authoring pipeline, custom importers, or external-data pipeline.
- Multiple Champions per faction.
- More than two factions.
- Strategic AI.
- Networking/online multiplayer.
- Full economy, market, upkeep, town trees, logistics, weather, supply, fatigue, or fog/feed misinformation.
- New lore, faction naming, unit roster design, site naming, or map content beyond test placeholders.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Test-local sample scenario definition with placeholder IDs such as `scenario_mvp_greenland_duel_test`, `faction_1`, `faction_2`, `node_start_a`, `node_start_b`, `node_central_objective`.
- Placeholder display/localization keys, if marked as placeholders and covered by validation expectations.
- Minimal enum/string IDs for controller types: `HumanLocal`, `CombatAI`, and reserved future `StrategicAI` only if needed for shape compatibility.
- Minimal site/army/unit references as IDs, provided the story does not implement tactical unit rules.

Not allowed:

- Placeholder behavior that silently decides movement, combat, site rewards, or victory.
- Hardcoded production tuning values outside test data unless explicitly represented as scenario definition fields.
- New player-facing names/lore not already approved.

## Dependencies

- Required prior stories:
  - SPIKE-001 Unity project and CI foundation should exist in the Unity repo.
  - No strategic gameplay story is required before this one.
- Required data/assets:
  - None for production assets.
  - Test-local scenario data allowed as above.
- Required architecture decisions:
  - Approved Unity technical scheme.
  - Approved control manifest.
  - Approved testing strategy.
  - Approved CI/build automation direction.
  - Data-authoring path remains phased hybrid; this story must not finalize the authoring pipeline.
- Required Unity/package setup:
  - Unity project with test assemblies available from SPIKE-001.
  - If exact assembly paths differ, implementer must inspect Unity repo and place domain code/tests according to existing AGENTS.md and assembly scheme.

## Acceptance criteria

Use observable/testable criteria.

- [ ] Given a valid MVP strategic scenario definition with two factions, one Champion per faction, starting hubs, nodes, routes, resource definitions, and a central objective, when the initializer runs, then it creates a serializable runtime state with no validation errors.
- [ ] Given a valid graph with routes between existing nodes, when validation runs, then every route endpoint resolves to an existing node ID.
- [ ] Given duplicate node IDs, when validation runs, then validation fails with a clear duplicate-node diagnostic.
- [ ] Given a route referencing a missing node ID, when validation runs, then validation fails with a clear missing-node diagnostic.
- [ ] Given a scenario with fewer or more than two MVP factions, when validation runs for MVP mode, then validation fails with a clear two-faction diagnostic.
- [ ] Given a faction without exactly one starting Champion in MVP mode, when validation runs, then validation fails with a clear starting-Champion diagnostic.
- [ ] Given a starting Champion whose starting node ID does not exist, when validation runs, then validation fails with a clear missing-start-node diagnostic.
- [ ] Given a scenario missing Credits, Materials, or Intel resource definitions, when validation runs, then validation fails with a clear missing-resource diagnostic.
- [ ] Given a scenario with an unsupported active MVP resource stockpile, when validation runs, then validation fails or ignores it according to a documented validation rule; hidden currencies are not allowed.
- [ ] Given a valid scenario, when runtime initialization completes, then each faction has Credits/Materials/Intel stockpiles initialized to defined starting values or zero.
- [ ] Given a valid scenario, when runtime initialization completes, then each Champion runtime state has faction ID, current node ID, attached army state, movement fields, major interaction availability field, and explicit status flags.
- [ ] Given a valid scenario with central objective settings, when runtime initialization completes, then scenario runtime contains central objective site ID, objective hold required count, objective hold faction/progress state, active faction ID, turn order, turn number, round number, and victory state.
- [ ] Given the runtime state object graph, when serialized through the approved/default Unity-compatible serializer used by tests, then it can round-trip without losing IDs, faction resources, Champion locations, site runtime state, or objective fields. If final serializer is not approved, a plain JSON test serializer may be used as a temporary test-only proxy and documented as such.
- [ ] Domain/state code compiles without requiring MonoBehaviour, scene objects, prefabs, camera, input, UI, or ScriptableObject asset references.

## Verification requirements

Use `docs/architecture/testing-strategy.md` to select required evidence by story type.

- Unit tests:
  - Required if the Unity repo has a non-Unity pure C# test runner; otherwise N/A with reason.
- Unity edit-mode tests:
  - Required.
  - Cover scenario validation, runtime initialization, graph endpoint validation, required resource validation, two-faction/one-Champion constraints, and serialization round-trip proxy.
- Unity play-mode tests:
  - N/A for this story; no scene/prefab/UI behavior is authorized.
- Integration/data validation tests:
  - Required for scenario definition validation and representative test-local scenario load/parse if a data representation is introduced.
- Manual Unity scene/prefab checks:
  - N/A; this story must not touch scenes/prefabs.
- Screenshot/video evidence:
  - N/A; no visual output.
- Performance budget or N/A:
  - N/A for first implementation. Optional sanity: validation/initialization of the small MVP test scenario should complete instantly in EditMode tests; no benchmark required.
- CI evidence:
  - Required once implemented: PR must include relevant test command output and CI status according to `docs/architecture/ci-build-automation.md`.
- Playtest evidence, if applicable:
  - N/A.
- TDD evidence required? Yes.
  - Production domain logic requires failing test first, RED/GREEN evidence, then regression run.
- Automation deferred? No.
  - This story is domain/data logic and should be automated in EditMode tests.

## Ambiguity Check

Status: PASS.

Open questions:
- Exact Unity repo source/test paths must be discovered by the implementer from existing AGENTS.md and assembly definitions before coding. This is implementation discovery, not a design ambiguity.

Assumptions:
- The implementation repo already has SPIKE-001 foundation available.
- Data-authoring pipeline remains phased hybrid; this story may use test-local data and plain domain models without deciding the final authoring route.
- The first production code should prefer pure domain classes/records and EditMode tests.

Out of scope:
- Same as story Out of scope section.

Allowed stubs/mocks:
- Same as Allowed stubs section.

Human approval:
- Approved by human on 2026-06-01 with note: "Story 001 is good".

Human-approved exceptions:
- None.

If status is FAIL, this story is not READY. Current status is PASS and the story is READY after human approval and parent epic handling.

## Branch / PR requirements

- Branch name:
  - `story/STORY-STRAT-001-scenario-map-graph-state`
- PR title:
  - `STORY-STRAT-001 Scenario map graph state`
- Required linked story ID:
  - `STORY-STRAT-001`
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md` §§2, 3, 6, 7, 9, 10, 11, 12, 13.
  - `docs/architecture/unity-technical-scheme.md` relevant domain/assembly/data sections.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 9, 10.
  - `docs/architecture/testing-strategy.md` §§Required Test and Evidence Layers, Story Type to Required Evidence Matrix, TDD Requirement.
  - `docs/architecture/ci-build-automation.md` relevant CI evidence requirements.
- Required root/scoped AGENTS.md instructions:
  - Unity repo root `AGENTS.md` and any scoped AGENTS.md under touched source/test paths must be read and followed.
- Required evidence summary:
  - Tests added/changed.
  - RED/GREEN TDD summary.
  - Validation diagnostics covered.
  - Serialization round-trip proxy result.
  - CI link/status.
- Required omissions section:
  - PR must explicitly list known omissions/stubs/mocks/assumptions/deferred work, or state `No known omissions`.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

A story may be marked READY only when all items are true:

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified or explicitly N/A.
- [x] UX/content/art/worldbuilding references are linked if relevant.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are either disallowed or explicitly listed.
- [x] Dependencies are listed and satisfied or marked blocking.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed, or approved exceptions are documented.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded.
  - Approved by human on 2026-06-01.

## DONE gate

A story may be marked DONE only when all items are true:

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

READY.

Gate assessment:

- Blockers before READY:
  - None.
- Concerns:
  - Exact Unity source/test paths must be discovered in the implementation repo at execution time.
- Required fixes before implementation:
  - None before READY. Implementer must still confirm implementation repo branch/PR plan and source/test paths before coding.
- Optional improvements:
  - Add a tiny scenario fixture name once the Unity repo folder/assembly names are inspected.
