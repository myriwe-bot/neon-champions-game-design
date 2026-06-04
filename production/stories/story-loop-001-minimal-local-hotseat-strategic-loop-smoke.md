---
title: STORY-LOOP-001 Minimal Local Hotseat Strategic Loop Smoke
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
    production/stories/story-strat-003-champion-route-movement,
    production/stories/story-strat-vis-001-minimal-strategic-map-presentation,
    production/stories/story-strat-input-001-select-champion-and-route-move,
    production/stories/story-strat-ui-001-minimal-hotseat-hud,
  ]
approval: approved
---

# Story: STORY-LOOP-001 Minimal Local Hotseat Strategic Loop Smoke

## Status

READY. Human approval recorded; this story may be assigned to Codex under the story train execution contract.

## Story type

Playtest + Integration + UX/Smoke.

Primary layer: end-to-end Unity smoke path for the earliest crude player-testable strategic loop.

## Estimate

- Size: S/M.
- Basis: readiness review on 2026-06-02; estimate covers story-scoped implementation and required evidence only.

## Parent epic

- Epic ID/path: [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].

## User/player/system value

As the team, we want a tiny local hotseat strategic loop that can be played by a human with crude visuals, selection/movement input, and an End Turn control, so that player-loop testing begins before site interaction and battles are implemented.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §2 Approved MVP Direction, rules 1-8.
  - `design/gdd/strategic-map.md` §3 First Scenario Shape, rules 1-6.
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 1-4 and 9-10 for this smoke; steps 5-8 are explicitly deferred.
  - `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft, limited to active faction/controller, active Champion, movement/reachable sites, whose turn is next, and status feedback.
  - `design/gdd/strategic-map.md` §9 Strategic Map Topology and §12 Champion/Army Strategic State and Movement Allowance as implemented by prior stories.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` §Core Technical Principle, §Project Layout Standard, §Assembly Boundary Standard.
  - `docs/architecture/control-manifest.md` §§1, 2, 3, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` — PlayMode/smoke, manual Unity verification, and evidence package requirements.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - Minimal usability smoke only. No final art/content/lore decisions.

## In scope

- Verify and, if necessary, lightly wire the already-implemented visual/input/HUD pieces into one smoke scene.
- Define a minimal manual smoke protocol for a human tester:
  1. launch the minimal strategic-map scene;
  2. confirm Faction 1 active;
  3. select Faction 1 Champion;
  4. move one route;
  5. observe movement points/status update;
  6. end turn;
  7. confirm Faction 2 active;
  8. select/move Faction 2 Champion;
  9. end turn and confirm round increment.
- Add automated PlayMode/smoke coverage where feasible for the same loop without requiring final art or site/battle systems.
- Add or update an evidence checklist/report location in the Unity repo for this smoke story, following existing repo conventions.
- Record known omissions clearly: no site interaction, no battle trigger, no rewards, no victory condition, no final art.

## Out of scope

- New gameplay mechanics beyond stitching prior stories together.
- Site interaction, guarded battle trigger, tactical battle, battle result application, rewards, recruitment, victory/loss, resource economy, strategic AI, save/load, final art, or polish.
- Refactoring scene/presentation architecture unless a blocking integration defect requires a separately approved fix.
- Expanding map content or changing balance/tuning.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Existing placeholder scene, shapes, labels, test-local scenario data, and debug/status line.
- Manual smoke checklist/report if automation cannot fully drive Unity input.

Not allowed:

- Fake success by bypassing domain services.
- Hidden implementation of deferred site/battle/reward/victory behavior.
- New final content or final player-facing copy.

## Dependencies

- Required prior stories:
  - STORY-STRAT-001 scenario/map graph state.
  - STORY-STRAT-002 hotseat turn ownership.
  - STORY-STRAT-003 champion route movement.
  - STORY-STRAT-VIS-001 minimal strategic-map presentation.
  - STORY-STRAT-INPUT-001 select Champion and route move.
  - STORY-STRAT-UI-001 minimal hotseat HUD.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required Unity/package setup:
  - Existing Unity scene/test/CI setup from SPIKE-001 and prior visual/input/UI stories.

## Acceptance criteria

- [ ] Given the smoke scene starts, when a human tester follows the smoke protocol, then Faction 1 can select its Champion, move one authored adjacent route, see the marker/HUD update, and end turn.
- [ ] Given Faction 1 ends turn, when Faction 2 becomes active, then Faction 2 can select its Champion and move one authored adjacent route while Faction 1 Champion is not active-controllable.
- [ ] Given both factions have ended one turn, when turn order wraps, then the HUD shows the correct active faction and incremented round number.
- [ ] Given the smoke loop runs, when all actions complete, then domain state, visual markers, and HUD state agree for Champion node positions, movement points, active faction, turn, and round.
- [ ] Given site/battle/reward/victory systems are not implemented, when the smoke is run, then the UI/status clearly does not imply those systems are available.
- [ ] Automated PlayMode/smoke coverage exists for the loop where feasible, or a documented human-approved exception explains the manual-only portions.
- [ ] Manual evidence includes a short video or screenshots plus a filled smoke checklist.
- [ ] PR evidence lists omissions and confirms no new gameplay systems were added beyond the smoke wiring.

## Verification requirements

- Unit tests: N/A unless pure helper logic is added.
- Unity edit-mode tests: Required for added helper logic if applicable.
- Unity play-mode tests: Required where feasible for the smoke path.
- Manual Unity scene/prefab checks: Required.
- Screenshot/video evidence: Required.
- Performance budget or N/A: N/A for crude MVP smoke scene.
- CI evidence: Required on implementation PR.
- Playtest evidence: Required as manual smoke protocol evidence, not full design playtest analysis.
- TDD evidence required? Yes for any production helper/application logic; smoke/manual evidence for scene loop.
- Automation deferred? Manual-only gaps require explicit exception and checklist evidence.

## Ambiguity Check

Status: PASS.

Open questions:

- None for the first crude hotseat movement smoke.

Assumptions:

- Testing the player loop early is more valuable than waiting for site/battle systems.
- This story is a smoke/integration gate, not a feature expansion story.

Out of scope:

- Same as story Out of scope section.

## Codex implementation notes

- Branch suggestion: `story/loop-001-hotseat-strategic-smoke`.
- Stop if the smoke requires implementing site interaction, tactical combat, final visuals, new architecture, or unapproved content.

## Branch / PR requirements

- Branch name: `story/loop-001-hotseat-strategic-smoke`
- PR title: `STORY-LOOP-001 Minimal local hotseat strategic loop smoke`
- Required linked story ID: `STORY-LOOP-001`
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
