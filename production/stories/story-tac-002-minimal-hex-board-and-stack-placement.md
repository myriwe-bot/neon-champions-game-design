---
title: STORY-TAC-002 Minimal Hex Board and Stack Placement
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
    production/stories/story-tac-001-battle-setup-result-dto-contracts,
  ]
approval: pending
---

# Story: STORY-TAC-002 Minimal Hex Board and Stack Placement

## Status

Draft. User approved minimal real tactical combat on a hex grid on 2026-06-04. This story is the first tactical implementation packet for the guarded-site vertical slice.

## Story type

Logic + Visual/Feel foundation.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player/system, I want a tiny real hex tactical board that can place attacker and guard stacks from `BattleSetup`, so that guarded-site capture can use real tactical combat instead of a result stub.

## Source requirements

- `design/gdd/tactical-combat.md` §§3-6, especially the 2026-06-04 hex-grid decision.
- `design/gdd/strategic-map.md` §14 Strategy-to-Tactical DTOs.
- `production/stories/story-tac-001-battle-setup-result-dto-contracts.md`.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.

## In scope

- Minimal flat hex coordinate model and neighbor lookup.
- Tiny authored/test board sufficient for one guarded-site battle.
- Placement of one attacking stack and one neutral guard stack from `BattleSetup` snapshots.
- Occupancy validation and invalid-placement diagnostics.
- Minimal scene or visual representation only if needed to prove the board exists.

## Out of scope

- Movement, attack, damage, tactical AI, pathfinding beyond neighbor/range basics, objectives, morale, abilities, LOS, cover, final art/UI, animation, audio.

## Acceptance criteria

- [ ] Given a valid `BattleSetup`, when the tactical board initializes, then attacker and defender stacks are placed on legal hexes.
- [ ] Given occupied or invalid hex coordinates, when placement validates, then it fails with clear diagnostics.
- [ ] Hex neighbor lookup is deterministic and covered by tests.
- [ ] Domain code avoids UnityEngine references unless isolated in presentation adapters.
- [ ] CI passes.

## Verification requirements

- Unity edit-mode tests: required for hex coordinates, neighbors, placement, occupancy, validation diagnostics.
- Unity play-mode/manual evidence: required only if scene/presentation is touched.
- Screenshot/video evidence: required if visible scene is touched.
- TDD evidence required? Yes.
- CI evidence: required.

## Ambiguity Check

Status: NEEDS FINAL APPROVAL.

Open questions:

- Approve a tiny fixed board and exactly one attacker stack + one guard stack for this story?

## Branch / PR requirements

- Branch name: `story/STORY-TAC-002-minimal-hex-board-stack-placement`
- PR title: `STORY-TAC-002 Minimal hex board and stack placement`
- Required evidence summary: hex/placement tests, CI, omissions.

## Verdict

Draft.
