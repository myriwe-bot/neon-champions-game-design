---
title: STORY-TAC-003 Minimal Tactical Movement and Attack Resolution
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
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-tac-002-minimal-hex-board-and-stack-placement,
  ]
approval: pending
---

# Story: STORY-TAC-003 Minimal Tactical Movement and Attack Resolution

## Status

Draft. Depends on STORY-TAC-002.

## Story type

Logic + Integration.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player/system, I want the minimal hex-grid tactical battle to support movement and attacks, so that guarded-site capture is resolved by real tactical actions.

## Source requirements

- `design/gdd/tactical-combat.md` §§5-6.
- `design/gdd/tactical-combat/overview-and-scope.md` MVP scope constraints.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.

## In scope

- Minimal tactical turn/activation order for attacker then defender or a deterministic two-side sequence.
- Stack movement over hexes using simple range/cost rules.
- One simple attack action with deterministic damage sufficient to defeat a tiny guard stack after one or more attacks.
- Stack defeated state.
- Minimal controls/UI only if needed for visible playthrough.

## Out of scope

- Full AP economy, initiative, abilities, morale, LOS, cover, ranged complexity, tactical AI sophistication, animation, final UI/art/audio, balance.

## Acceptance criteria

- [ ] Given a stack with movement range, when it moves to a legal reachable hex, then position updates and occupancy remains valid.
- [ ] Given an illegal move, when validation runs, then movement is rejected with clear diagnostics.
- [ ] Given an attack target in range, when attack resolves, then deterministic damage/losses are applied.
- [ ] Given damage reduces a stack to zero, then the stack is marked defeated.
- [ ] CI passes.

## Verification requirements

- Unity edit-mode tests: required for movement validation, occupancy, attack resolution, defeat state, invalid diagnostics.
- Unity play-mode/manual evidence: required if visible controls are touched.
- Screenshot/video evidence: required if visible scene is touched.
- TDD evidence required? Yes.
- CI evidence: required.

## Ambiguity Check

Status: NEEDS FINAL APPROVAL.

Open questions:

- Approve deterministic minimal damage instead of balance-realistic tactical formulas for this slice?

## Branch / PR requirements

- Branch name: `story/STORY-TAC-003-minimal-tactical-movement-attack-resolution`
- PR title: `STORY-TAC-003 Minimal tactical movement and attack resolution`
- Required evidence summary: movement/attack/defeat tests, CI, omissions.

## Verdict

Draft.
