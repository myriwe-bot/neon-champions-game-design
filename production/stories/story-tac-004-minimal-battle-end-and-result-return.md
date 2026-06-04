---
title: STORY-TAC-004 Minimal Battle End and BattleResult Return
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
    design/gdd/strategic-map,
    docs/architecture/unity-technical-scheme,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-tac-001-battle-setup-result-dto-contracts,
    production/stories/story-tac-003-minimal-tactical-movement-and-attack-resolution,
  ]
approval: pending
---

# Story: STORY-TAC-004 Minimal Battle End and BattleResult Return

## Status

READY-candidate. Depends on STORY-TAC-003. This packet connects minimal tactical combat back to the existing DTO boundary without applying strategic control/rewards.

## Story type

Logic + Integration.

## Estimate

- Size: M.
- Basis: adds end-condition detection and DTO output; excludes strategic mutation and deeper tactical modes.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player/system, I want the minimal tactical battle to end and return a real `BattleResult`, so strategic guarded-site capture can be driven by tactical outcome rather than a stub.

## Source requirements

Exact source references:

- `design/gdd/tactical-combat.md` §5 Core Combat Loop, steps 8-10.
- `design/gdd/tactical-combat.md` §4 MVP Scope, post-battle summary/result boundary.
- `design/gdd/strategic-map.md` §14 Strategy-to-Tactical DTOs, BattleResult minimum and strategic application contract.
- `production/stories/story-tac-001-battle-setup-result-dto-contracts.md`.
- `docs/architecture/unity-technical-scheme.md`.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.

## In scope

- Detect battle end when all stacks on one side are defeated in the minimal two-side battle.
- Return attacker-win when neutral guards are defeated.
- Return defender-win when attacker stack is defeated.
- Produce a valid `BattleResult` matching the input `BattleSetup.battleId`.
- Include side result facts needed by STORY-STRAT-005:
  - side IDs/controllers;
  - surviving/defeated stack snapshots;
  - loss/survivor counts sufficient for strategic army/guard update;
  - outcome.
- Keep tactical result generation separate from strategic site control/reward mutation.

## Out of scope

- Strategic result application, site control, rewards, victory mutation; belongs to STORY-STRAT-005.
- Retreat, surrender, draw, cancellation, rout, morale, rewards, post-battle UI polish, replay/event stream.
- Tactical AI sophistication or automatic playthrough beyond what earlier stories already provide.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder result summary facts/keys.
- Attacker-win/defender-win only for this slice.
- Test-local `BattleSetup`/board fixtures.

Not allowed:

- Strategic state mutation from tactical layer.
- Hidden rewards/control changes inside tactical DTO creation.
- Pretending retreat/draw/cancel modes exist.

## Dependencies

- Required prior stories:
  - STORY-TAC-001 battle setup/result DTO contracts.
  - STORY-TAC-003 minimal tactical movement and attack resolution.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.

## Acceptance criteria

- [ ] Given defender stack defeated, when battle end evaluates, then attacker-win `BattleResult` is produced with matching battle ID and valid side results.
- [ ] Given attacker stack defeated, when battle end evaluates, then defender-win `BattleResult` is produced with matching battle ID and valid side results.
- [ ] Given no defeated side, when battle end evaluates, then no final result is produced and tactical state remains in-progress.
- [ ] Given a produced result, when the STORY-TAC-001 DTO validator runs, then the result passes validation.
- [ ] Given result creation, tactical code does not mutate strategic site, resource, control, Champion strategic state, turn, or victory state.
- [ ] CI passes.

## Verification requirements

- Unity edit-mode tests: Required for end-condition detection, attacker-win/defender-win result creation, DTO validation, in-progress no-result case, no strategic mutation.
- Unity play-mode tests: Required only if connected to visible tactical smoke in this story.
- Manual Unity scene/prefab checks and screenshot/video: Required only if scene/presentation is touched.
- Performance budget or N/A: N/A for tiny result creation.
- CI evidence: Required on implementation PR.
- TDD evidence required? Yes.

## Ambiguity Check

Status: PASS-candidate.

Assumptions for human approval:

- Attacker-win and defender-win are the only required outcomes for this first slice.
- Retreat, draw, cancel, morale rout, and result-screen polish are deferred.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-004-minimal-battle-end-result-return`
- PR title: `STORY-TAC-004 Minimal battle end and BattleResult return`
- Required linked story ID: `STORY-TAC-004`
- Required evidence summary: RED/GREEN TDD summary, battle-end/result tests, DTO validation, no-strategic-mutation evidence, CI link/status, omissions section.

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
