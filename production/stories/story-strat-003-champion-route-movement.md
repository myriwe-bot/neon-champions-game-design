---
title: STORY-STRAT-003 Champion Route Movement
type: story
status: approved
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-02
source_lore: []
related:
  [
    design/gdd/strategic-map,
    docs/architecture/unity-technical-scheme,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-strat-001-scenario-map-graph-state,
    production/stories/story-strat-002-hotseat-turn-ownership,
  ]
approval: approved
---

# Story: STORY-STRAT-003 Champion Route Movement

## Status

READY. Human approval recorded; this story may be assigned to Codex under the story train execution contract.

## Story type

Logic.

Primary layer: pure strategic-domain movement validation and state transition over the authored node-route graph.

## Estimate

- Size: S/M.
- Basis: readiness review on 2026-06-02; estimate covers story-scoped implementation and required evidence only.

## Parent epic

- Epic ID/path: [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].

## User/player/system value

As a system, I want Champions to move deterministically along authored routes by spending movement points, so that the strategic map becomes an actual playable decision surface before site interaction and battles are added.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §9 Strategic Map Topology, rules 1-8 and MVP movement contract draft rules 1-6.
  - `design/gdd/strategic-map.md` §12 Champion/Army Strategic State and Movement Allowance, rules 1-13 and movement/interaction contract rules 2-3.
  - `design/gdd/strategic-map.md` §15 Acceptance Criteria Draft, Champion movement criterion.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` — domain logic separate from Unity presentation.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` — story-type evidence matrix and TDD requirement.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - N/A. Movement preview returns data only; no UI/visual implementation.

## In scope

- Add a pure domain movement command/request model, if not already present.
- Add route-based movement validation:
  - Champion exists;
  - Champion belongs to active faction if turn ownership is available;
  - Champion current node matches movement origin;
  - destination is connected by an authored route;
  - route movement cost is positive and affordable;
  - defeated/locked Champion cannot move.
- Add movement preview that reports validity, route cost, remaining movement, and diagnostics without mutating runtime state.
- Add movement apply that updates `CurrentNodeId` and subtracts movement points only after validation passes.
- Keep movement single-route per command for this story.
- Add EditMode/domain tests for valid movement, preview non-mutation, invalid origin/destination, disconnected nodes, insufficient movement, inactive faction if applicable, and defeated/locked Champion restriction.

## Out of scope

- Multi-step pathfinding, route choice optimization, freeform/tile/hex movement, terrain pathfinding, weather, supply, fatigue, route ownership taxes, logistics attrition, or movement-type differences.
- UI movement range display, player input, camera, map rendering, scene, prefab, or animation.
- Site interaction, auto-claim, auto-battle, recruitment, reward collection, or end-turn automation.
- Strategic AI movement planning.
- New map content, lore, names, or visual Greenland presentation.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Test-local graph fixtures from STORY-STRAT-001.
- A simple movement result/diagnostic object for tests and future UI use.

Not allowed:

- Hidden automatic site interaction after movement.
- New movement modifiers not approved by this story.

## Dependencies

- Required prior stories:
  - STORY-STRAT-001 scenario/map graph state.
  - STORY-STRAT-002 hotseat turn ownership is recommended before implementation if movement is active-faction gated. If not merged, this story must only implement movement in a way that remains compatible with STORY-STRAT-002 and does not invent alternate turn ownership.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.

## Acceptance criteria

- [ ] Given a Champion at node A with enough movement points and an authored route from A to B, when movement apply runs, then the Champion's current node becomes B and movement points decrease by the route cost.
- [ ] Given the same valid movement request, when movement preview runs, then it reports the expected destination/cost/remaining movement and does not mutate runtime state.
- [ ] Given a Champion current node that does not match the requested origin, when validation runs, then it fails with a clear origin/current-node diagnostic.
- [ ] Given no route connects origin and destination, when validation runs, then it fails with a clear disconnected-route diagnostic.
- [ ] Given route cost exceeds remaining movement, when validation runs, then it fails with a clear insufficient-movement diagnostic.
- [ ] Given a route with non-positive movement cost, when validation runs, then it fails with a clear invalid-route-cost diagnostic.
- [ ] Given a defeated or locked Champion, when movement is requested, then validation fails with a clear Champion-status diagnostic.
- [ ] Given active-faction enforcement is available, when an inactive faction Champion attempts movement, then validation fails with a clear active-faction diagnostic.
- [ ] Domain movement code compiles without UnityEngine, MonoBehaviour, ScriptableObject, scene, prefab, input, camera, or UI references.

## Verification requirements

- Unit tests: N/A unless a non-Unity pure C# runner exists.
- Unity edit-mode tests: Required for movement validation, preview non-mutation, apply mutation, and diagnostics.
- Unity play-mode tests: N/A; no scene/prefab/UI behavior is authorized.
- Integration/data validation tests: N/A beyond domain/EditMode tests.
- Manual Unity scene/prefab checks: N/A.
- Screenshot/video evidence: N/A.
- Performance budget or N/A: N/A for single-route movement over the MVP test graph.
- CI evidence: Required on implementation PR.
- Playtest evidence: N/A.
- TDD evidence required? Yes.
- Automation deferred? No.

## Ambiguity Check

Status: PASS.

Open questions:

- None if implementation remains single-route domain movement.

Assumptions:

- Route movement cost is read from `StrategicRouteDefinition.MovementCost`.
- Movement applies one authored route per command; richer pathing is deferred.

Out of scope:

- Same as story Out of scope section.

Allowed stubs/mocks:

- Same as Allowed stubs section.

Human approval:

- Approved by human on 2026-06-02 in response to readiness review.

Human-approved exceptions:

- None.

## Branch / PR requirements

- Branch name: `story/STORY-STRAT-003-champion-route-movement`
- PR title: `STORY-STRAT-003 Champion route movement`
- Required linked story ID: `STORY-STRAT-003`
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md` §§9, 12, 15.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: Unity repo root `AGENTS.md` and scoped source/test `AGENTS.md` under touched paths.
- Required evidence summary: RED/GREEN TDD summary, movement tests added/changed, CI link/status, omissions section.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/art/worldbuilding references are N/A.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are either disallowed or explicitly listed.
- [x] Dependencies are listed.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [x] Required automated tests/validators/PlayMode evidence are listed or N/A.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Estimate is recorded.
- [x] Human approval has been given or delegated gate approval is recorded.
  - Approved by human on 2026-06-02 in response to readiness review.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests and CI pass or approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are documented.
- [ ] PR/code review is complete.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY. Gate blockers: none.
