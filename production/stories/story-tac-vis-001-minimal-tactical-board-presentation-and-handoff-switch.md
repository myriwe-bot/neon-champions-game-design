---
title: STORY-TAC-VIS-001 Minimal Tactical Board Presentation and Handoff Switch
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-04
updated: 2026-06-04
source_lore: []
related:
  [
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/overview-and-scope,
    docs/architecture/unity-technical-scheme,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger,
    production/stories/story-tac-002-minimal-hex-board-and-stack-placement,
    production/stories/story-tac-003-minimal-tactical-movement-and-attack-resolution,
  ]
approval: pending
---

# Story: STORY-TAC-VIS-001 Minimal Tactical Board Presentation and Handoff Switch

## Status

READY-candidate. Proposed after STORY-TAC-003 because the tactical rules now exist but the player still cannot see a tactical map or clearly switch from strategic guarded-site handoff into a tactical board. This deliberately pulls crude visibility forward before STORY-TAC-004 battle-result plumbing.

## Story type

Visual/Feel + Integration + Smoke.

## Estimate

- Size: M.
- Basis: one crude tactical board view and one visible handoff/switch path using existing domain setup/state; excludes full tactical UI and battle completion.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player/tester, I want the guarded-site battle handoff to show a crude tactical hex board with attacker and defender stacks, so I can verify that the game actually switches into a tactical layer before deeper result plumbing is added.

## Source requirements

Exact source references:

- `design/gdd/tactical-combat.md` §3 Design Principles.
- `design/gdd/tactical-combat.md` §4 MVP Scope.
- `design/gdd/tactical-combat.md` §5 Core Combat Loop, steps 1-5 for setup/deployment visibility only.
- `design/gdd/tactical-combat.md` §6.0 Grid Decision.
- `design/gdd/tactical-combat.md` §6.1 Battlefield Layout and Objectives — only flat placeholder battlefield readability is authorized.
- `design/gdd/tactical-combat.md` §6.2 Deployment — only existing one-attacker/one-neutral-guard placement visibility is authorized.
- `design/gdd/tactical-combat/overview-and-scope.md` MVP Scope Constraints and Tactical Entity Model.
- `docs/architecture/unity-technical-scheme.md`.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 6, 7, 8, 9, 10.
- `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.

## In scope

- Add a minimal tactical-board presentation path using the existing STORY-TAC-002/003 domain board state.
- From the existing guarded-site Attack/Interact handoff path, show/switch to a crude tactical board view or scene/panel suitable for smoke testing.
- Render the tiny placeholder hex board with readable placeholder hex markers.
- Render exactly the existing attacker and neutral guard defender stack positions from `TacticalBoardState`.
- Show enough labels/status to identify:
  - tactical mode is active;
  - attacker stack;
  - neutral guard defender stack;
  - current/active stack or side if available from the domain state.
- Keep presentation as a thin adapter over domain/application state; tactical rules stay in domain.
- Add PlayMode/smoke coverage where feasible for loading/switching and expected board/stack marker counts.
- Capture screenshot/video/manual evidence for the crude tactical board.

## Out of scope

- Battle end, `BattleResult` creation, strategic result application, site control/rewards/resources/recruitment/victory mutation.
- Full tactical input, movement/attack controls, AP/initiative UI, wait/defend, retaliation, ZOC, overwatch, abilities, morale, LOS, cover, objectives, tactical AI.
- Final tactical scene design, final UI/art/icons/animation/audio/copy, camera polish, shader/VFX work, roster/balance/content changes.
- Save/load, new packages, new data-authoring architecture, broad scene framework replacement, event bus/service locator/DI introduction.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder primitive shapes, colors, labels, and layout positions for hexes and stacks.
- A minimal tactical scene/panel/bootstrap object if it uses approved Unity project patterns and is listed in evidence.
- Test-local guarded-site `BattleSetup` fixture matching prior stories.
- A temporary deterministic handoff route from the existing guarded-site interaction into tactical view, if clearly documented and not a fake battle result.

Not allowed:

- Fake tactical victory/result or auto-resolve.
- Direct presentation mutation of canonical tactical state.
- Final UI/art/content claims.

## Dependencies

- Required prior stories:
  - STORY-STRAT-004 site interaction and guarded battle trigger.
  - STORY-TAC-002 minimal hex board and stack placement.
  - STORY-TAC-003 minimal tactical movement and attack resolution.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.

## Acceptance criteria

- [ ] Given the existing guarded-site Attack/Interact path is triggered, when the tactical handoff occurs, then the player/tester sees a tactical board view rather than only logs/domain state.
- [ ] Given the tactical board view is shown, then all placeholder hexes from the minimal board are visibly represented and countable.
- [ ] Given the tactical board view is shown, then the attacker and neutral guard defender stacks appear at their `TacticalBoardState` coordinates with readable labels or distinct placeholder markers.
- [ ] Given tactical mode is active, then visible status text identifies tactical mode and enough active-side/current-stack context to orient the tester.
- [ ] Given the view is presentation-only, then domain tactical logic remains free of UnityEngine/presentation dependencies and presentation does not own canonical rules.
- [ ] PlayMode/smoke or documented automated substitute proves the handoff/switch loads and expected hex/stack markers exist.
- [ ] Manual screenshot/video evidence exists for the crude tactical map.
- [ ] CI passes.

## Verification requirements

- Unity PlayMode/smoke tests: Required where feasible for handoff/switch and marker counts.
- Unity EditMode/domain tests: Required only for new helper/application logic; do not weaken existing tactical tests.
- Manual Unity scene/prefab checks: Required.
- Screenshot/video evidence: Required.
- Performance budget or N/A: N/A for tiny placeholder board.
- CI evidence: Required on implementation PR.
- TDD evidence required? Yes for production helpers/application logic; smoke/manual evidence for scene/presentation wiring.

## Ambiguity Check

Status: PASS-candidate.

Resolved by user on 2026-06-04:

- User does not currently see a way to view the tactical map and wants this to become an early priority.

Assumptions for human approval:

- It is acceptable to insert this visual/switch story before STORY-TAC-004 rather than continuing with invisible battle-result plumbing.
- A crude placeholder board is preferred over final tactical UI/art.
- The first visible tactical board need not support tactical input controls yet; it only needs to make the transition and board/stack state visible.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-VIS-001-minimal-tactical-board-presentation-handoff-switch`
- PR title: `STORY-TAC-VIS-001 Minimal tactical board presentation and handoff switch`
- Required linked story ID: `STORY-TAC-VIS-001`
- Required evidence summary: handoff/switch smoke, marker-count PlayMode evidence or documented substitute, screenshot/video, CI link/status, omissions section.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Stable ID, title, type, status, and parent epic.
- [x] Exact GDD and architecture/control sources are linked.
- [x] Scope, out-of-scope, allowed placeholders, dependencies, acceptance criteria, and evidence are explicit.
- [x] Ambiguity Check is PASS-candidate.
- [ ] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are documented.
- [ ] PR/code review is complete.
- [ ] CI passes.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY-candidate pending human approval.
