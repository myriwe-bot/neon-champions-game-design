---
title: STORY-STRAT-INPUT-001 Select Champion and Route Move
type: story
status: approved
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-02
source_lore: []
related: [design/gdd/strategic-map, docs/architecture/unity-technical-scheme, docs/architecture/control-manifest, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, production/epics/epic-strat-mvp-001-strategic-mvp-core-loop, production/stories/story-strat-001-scenario-map-graph-state, production/stories/story-strat-002-hotseat-turn-ownership, production/stories/story-strat-003-champion-route-movement, production/stories/story-strat-vis-001-minimal-strategic-map-presentation]
approval: approved
---

# Story: STORY-STRAT-INPUT-001 Select Champion and Route Move

## Status

READY. Human approval recorded; this story may be assigned to Codex under the story train execution contract.

## Story type

Integration + UI/Input.

Primary layer: Unity input/presentation adapter that calls approved strategic-domain movement services.

## Estimate

- Size: M.
- Basis: readiness review on 2026-06-02; estimate covers story-scoped implementation and required evidence only.

## Parent epic

- Epic ID/path: [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].

## User/player/system value

As a local hotseat player, I want to select my active Champion and move it along a visible adjacent route, so that the first strategic player loop can be tested directly in Unity with crude visuals.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §2 Approved MVP Direction, rules 1-8.
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 2-4 and 9-10.
  - `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft, especially active Champion, movement range/reachable sites, expected interaction type before committing where applicable, and whose turn is next.
  - `design/gdd/strategic-map.md` §9 Strategic Map Topology, rules 1-8 and movement contract draft rules 1-6.
  - `design/gdd/strategic-map.md` §12 Champion/Army Strategic State and Movement Allowance, movement and interaction contract rules used by STORY-STRAT-003.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` §Initial Unity Defaults, §Project Layout Standard, §Assembly Boundary Standard.
  - `docs/architecture/control-manifest.md` §§1, 2, 3, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` — Integration/UI/Input and PlayMode/smoke evidence expectations.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - UX readability only. No final art/content/lore decisions.

## In scope

- Add minimal selection/movement input for the crude strategic-map scene:
  - select the active faction's Champion marker;
  - indicate selected Champion;
  - indicate adjacent reachable destination nodes/routes from the selected Champion's current node;
  - choose one reachable adjacent destination by clicking/tapping/selecting its node or route, using the approved Unity input approach already present in the repo.
- Call STORY-STRAT-003's domain movement preview/apply service for validation and mutation.
- Update visual Champion marker position after successful movement.
- Reject/diagnose invalid movement attempts through a crude visible/debug message path.
- Enforce active-faction ownership if STORY-STRAT-002 is available.
- Add PlayMode tests where feasible for selection, valid route move, inactive/invalid move rejection, and visual state update.

## Out of scope

- Multi-step pathfinding, drag routes, route optimization, animation polish, movement tweening, terrain movement, camera polish, or input remapping polish.
- End Turn button/HUD; that belongs to STORY-STRAT-UI-001.
- Site interaction, auto-claim, auto-battle, rewards, recruitment, victory checks, or tactical scene transition.
- Strategic AI, networking, save/load, final UI skin, localization implementation, or final map art.
- New scenario content, new rules, movement modifiers, or balance changes.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder selected/reachable colors or outlines.
- Simple on-screen/debug diagnostic text.
- Existing/test-local scenario fixture.

Not allowed:

- Presentation/input code that mutates Champion position directly without going through the approved movement service.
- Hidden site interaction or turn advancement after movement.
- New movement rules not present in STORY-STRAT-003.

## Dependencies

- Required prior stories:
  - STORY-STRAT-001 scenario/map graph state.
  - STORY-STRAT-002 hotseat turn ownership.
  - STORY-STRAT-003 champion route movement.
  - STORY-STRAT-VIS-001 minimal strategic-map presentation.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required Unity/package setup:
  - Existing Unity Input System setup or approved equivalent from the Unity repo. If absent, Codex must stop rather than introduce a package/settings change without approval.

## Acceptance criteria

- [ ] Given the minimal strategic-map scene is running and Faction 1 is active, when the player selects Faction 1's Champion marker, then the Champion becomes visibly selected.
- [ ] Given a selected Champion with adjacent affordable routes, when selection is active, then reachable adjacent nodes/routes are visibly indicated.
- [ ] Given the player chooses a reachable adjacent destination, when movement is applied, then the domain movement service updates the Champion current node and spends movement points, and the visual marker moves to the destination node.
- [ ] Given movement preview is displayed or logged, when preview runs, then it does not mutate runtime state before the player commits movement.
- [ ] Given the player attempts to move to a disconnected or unaffordable destination, when input is handled, then movement is rejected with a clear crude diagnostic and the visual marker does not move.
- [ ] Given an inactive faction Champion exists, when the player attempts to select/move it during another faction's turn, then the action is blocked or non-selectable with a clear diagnostic.
- [ ] Input/presentation code compiles without adding new domain dependencies on UnityEngine or presentation classes.
- [ ] PlayMode/smoke evidence covers valid select-and-move and at least one invalid move rejection, or records a human-approved automation exception.

## Verification requirements

- Unit tests: N/A unless pure selection/mapping helpers are added.
- Unity edit-mode tests: Required for pure helper logic if added.
- Unity play-mode tests: Required where feasible for select/move/reject smoke.
- Manual Unity scene/prefab checks: Required.
- Screenshot/video evidence: Required, showing select, reachable indication, movement, and rejection or diagnostic.
- Performance budget or N/A: N/A for one Champion and crude MVP map.
- CI evidence: Required on implementation PR.
- Playtest evidence: Optional but recommended once UI story lands.
- TDD evidence required? Yes for helper/application behavior; PlayMode/manual evidence for input wiring.
- Automation deferred? Only if Unity input automation is technically blocked and the PR documents a manual test protocol plus reason.

## Ambiguity Check

Status: PASS.

Open questions:
- None for single-step adjacent-route input.

Assumptions:
- The first playable goal favors crude, testable click/select behavior over polished controls.
- Only one Champion per faction exists in MVP, so selection can remain simple.

Out of scope:
- Same as story Out of scope section.

## Codex implementation notes

- Branch suggestion: `story/strat-input-001-select-route-move`.
- Stop if the task requires final input architecture, package/settings changes, camera overhaul, or new movement rules.

## Branch / PR requirements

- Branch name: `story/strat-input-001-select-route-move`
- PR title: `STORY-STRAT-INPUT-001 Select Champion and route move`
- Required linked story ID: `STORY-STRAT-INPUT-001`
- Required linked GDD/ADR/control docs: use the exact source references listed above.
- Required root/scoped AGENTS.md instructions: Unity repo root `AGENTS.md` and scoped source/test `AGENTS.md` under touched paths.
- Required evidence summary: RED/GREEN TDD summary where applicable, tests added/changed, CI link/status, manual evidence where required, and omissions section.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/art/worldbuilding references are linked if relevant or explicitly N/A.
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
