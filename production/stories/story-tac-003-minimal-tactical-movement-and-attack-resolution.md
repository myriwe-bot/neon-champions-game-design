---
title: STORY-TAC-003 Minimal Tactical Movement and Attack Resolution
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
    docs/architecture/unity-technical-scheme,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-tac-002-minimal-hex-board-and-stack-placement,
  ]
approval: pending
---

# Story: STORY-TAC-003 Minimal Tactical Movement and Attack Resolution

## Status

READY-candidate. Depends on STORY-TAC-002. This packet makes the hex board minimally playable without expanding into the full tactical GDD.

## Story type

Logic + Integration.

## Estimate

- Size: M.
- Basis: adds movement and one deterministic attack/loss path; excludes battle-end/result return and tactical system depth.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player/system, I want stacks on the minimal hex board to move and attack, so that guarded-site capture is resolved by real tactical actions, not a result injector.

## Source requirements

Exact source references:

- `design/gdd/tactical-combat.md` §3 Design Principles.
- `design/gdd/tactical-combat.md` §4 MVP Scope.
- `design/gdd/tactical-combat.md` §5 Core Combat Loop, steps 5-8.
- `design/gdd/tactical-combat.md` §6.0 Grid Decision.
- `design/gdd/tactical-combat.md` §6.3 AP and Actions.
- `design/gdd/tactical-combat.md` §6.4 Movement, ZOC, Retaliation, and Overwatch — only movement basics are authorized here.
- `design/gdd/tactical-combat.md` §6.5 Attacks, Damage, and Defense — only a minimal deterministic attack is authorized here.
- `docs/architecture/unity-technical-scheme.md`.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.

## In scope

- Add minimal tactical activation/action command support for the current side/stack.
- Add simple hex movement validation and application:
  - legal destination;
  - unoccupied destination;
  - within movement range;
  - state mutation only through domain action/command.
- Add one simple attack validation and application:
  - target belongs to opposing side;
  - target is in the minimal allowed range;
  - deterministic damage/loss value sufficient for tests and slice play.
- Add defeated stack state when stack strength reaches zero.
- Add tiny visible controls only if needed and safe; otherwise domain/edit-mode coverage is the core evidence.

## Out of scope

- Battle end and `BattleResult` creation; belongs to STORY-TAC-004.
- Full AP/initiative model, wait/defend, retaliation, ZOC, overwatch, abilities, morale, LOS, cover, objectives, tactical AI sophistication.
- Balance-realistic formulas, final roster/unit design, animation/audio/final UI.
- Strategic control/reward mutation.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder stack stat values such as movement range, attack range, hit points/strength, and deterministic damage.
- Test-local board and `BattleSetup` fixtures from STORY-TAC-002.
- Minimal turn/current-side fixture data.

Not allowed:

- Result auto-win that skips movement/attack.
- Full combat formula invention beyond deterministic slice values.
- Final unit/faction balance claims.

## Dependencies

- Required prior stories:
  - STORY-TAC-002 minimal hex board and stack placement.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.

## Acceptance criteria

- [ ] Given a stack with movement range, when it moves to a legal reachable unoccupied hex, then position updates and occupancy remains valid.
- [ ] Given an illegal move target, occupied hex, or out-of-range destination, when movement validates, then movement is rejected with clear diagnostics and no board mutation occurs.
- [ ] Given an attack target in the minimal allowed range, when attack resolves, then deterministic damage/losses are applied to the target stack.
- [ ] Given damage reduces a stack to zero strength, then the stack is marked defeated and cannot move or attack.
- [ ] Given an invalid attack target, same-side target, defeated attacker, or out-of-range target, when attack validates, then attack is rejected with clear diagnostics and no combat mutation occurs.
- [ ] Domain logic compiles without UnityEngine/presentation dependencies unless isolated in adapters.
- [ ] CI passes.

## Verification requirements

- Unity edit-mode tests: Required for movement validation/application, occupancy, attack validation/application, damage/losses, defeated state, invalid diagnostics, no-mutation cases.
- Unity play-mode tests: Required only if visible controls are touched.
- Manual Unity scene/prefab checks and screenshot/video: Required only if scene/presentation is touched.
- Performance budget or N/A: N/A for tiny board/domain commands.
- CI evidence: Required on implementation PR.
- TDD evidence required? Yes.

## Ambiguity Check

Status: PASS-candidate.

Resolved by user on 2026-06-04:

- Minimal real tactical combat on a hex grid is required for the current closeout slice.

Assumptions for human approval:

- Deterministic minimal damage is acceptable for the first slice; balance-realistic formulas are deferred.
- Only movement and a basic attack are required here; battle result return waits for STORY-TAC-004.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-003-minimal-tactical-movement-attack-resolution`
- PR title: `STORY-TAC-003 Minimal tactical movement and attack resolution`
- Required linked story ID: `STORY-TAC-003`
- Required evidence summary: RED/GREEN TDD summary, movement/attack/defeat tests, CI link/status, omissions section.

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
