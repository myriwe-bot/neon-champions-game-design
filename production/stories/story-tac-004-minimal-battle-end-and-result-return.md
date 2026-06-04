---
title: STORY-TAC-004 Minimal Battle End and BattleResult Return
type: story
status: draft
phase: production
owner: shared
created: 2026-06-04
updated: 2026-06-04
source_lore: []
related:
  [
    design/gdd/tactical-combat,
    design/gdd/strategic-map,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-tac-001-battle-setup-result-dto-contracts,
    production/stories/story-tac-003-minimal-tactical-movement-and-attack-resolution,
  ]
approval: pending
---

# Story: STORY-TAC-004 Minimal Battle End and BattleResult Return

## Status

Draft. Depends on STORY-TAC-003.

## Story type

Logic + Integration.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player/system, I want the minimal tactical battle to end and return a real `BattleResult`, so that strategic guarded-site capture is based on tactical outcome rather than a stub.

## Source requirements

- `design/gdd/strategic-map.md` §14 Strategy-to-Tactical DTOs.
- `design/gdd/tactical-combat.md` §5 Core Combat Loop and §7 acceptance/result expectations where applicable.
- `production/stories/story-tac-001-battle-setup-result-dto-contracts.md`.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.

## In scope

- Detect battle end when attacker or defender stack is defeated.
- Create a valid `BattleResult` matching the input `BattleSetup.battleId`.
- Include attacker/defender survivor/loss snapshots and defeated flags.
- Return attacker-win/defender-win outcome for guarded-site use.
- Minimal result summary facts/keys.

## Out of scope

- Full tactical event stream, replay, morale/rout, retreat, draw/cancel nuance, rewards/control mutation, strategic result application, final UI/copy.

## Acceptance criteria

- [ ] Given defender stack defeated, when battle end evaluates, then attacker-win `BattleResult` is produced with matching battle ID and valid side results.
- [ ] Given attacker stack defeated, when battle end evaluates, then defender-win `BattleResult` is produced with matching battle ID and valid side results.
- [ ] Given no defeated side, when battle end evaluates, then no final result is produced.
- [ ] Result DTO validates using the STORY-TAC-001 contract.
- [ ] Tactical layer does not mutate strategic site/resource/control state.
- [ ] CI passes.

## Verification requirements

- Unity edit-mode tests: required for end conditions, result creation, DTO validation, no strategic mutation.
- Unity play-mode/manual evidence: required if connected to visible smoke.
- Screenshot/video evidence: required if visible scene is touched.
- TDD evidence required? Yes.
- CI evidence: required.

## Ambiguity Check

Status: NEEDS FINAL APPROVAL.

Open questions:

- Approve attacker-win/defender-win only for this first slice, with retreat/draw/cancel deferred?

## Branch / PR requirements

- Branch name: `story/STORY-TAC-004-minimal-battle-end-result-return`
- PR title: `STORY-TAC-004 Minimal battle end and BattleResult return`
- Required evidence summary: result tests, DTO validation, CI, omissions.

## Verdict

Draft.
