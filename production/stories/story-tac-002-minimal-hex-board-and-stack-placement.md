---
title: STORY-TAC-002 Minimal Hex Board and Stack Placement
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
    design/gdd/strategic-map,
    docs/architecture/unity-technical-scheme,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-tac-001-battle-setup-result-dto-contracts,
  ]
approval: pending
---

# Story: STORY-TAC-002 Minimal Hex Board and Stack Placement

## Status

READY-candidate. User approved minimal real tactical combat on a hex grid on 2026-06-04. This is the first tactical implementation packet for the current epic closeout and should remain deliberately tiny.

## Story type

Logic + Visual/Feel foundation.

## Estimate

- Size: M.
- Basis: introduces the tactical board foundation and placement validation, but excludes movement, attacks, and battle result generation.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player/system, I want a tiny real hex tactical board that can place attacker and guard stacks from `BattleSetup`, so guarded-site capture can use real tactical combat instead of a fake result stub.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/tactical-combat.md` §3 Design Principles.
  - `design/gdd/tactical-combat.md` §4 MVP Scope.
  - `design/gdd/tactical-combat.md` §5 Core Combat Loop, steps 1-4.
  - `design/gdd/tactical-combat.md` §6.0 Grid Decision.
  - `design/gdd/tactical-combat.md` §6.1 Tactical Entities.
  - `design/gdd/tactical-combat.md` §6.2 Active Army and Deployment.
  - `design/gdd/strategic-map.md` §14 Strategy-to-Tactical DTOs.
  - `production/stories/story-tac-001-battle-setup-result-dto-contracts.md`.
- ADR / architecture / control:
  - `docs/architecture/unity-technical-scheme.md` — domain logic separated from Unity presentation.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` — TDD and story evidence requirements.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - No final tactical art, unit names, faction content, animation, audio, or final copy. Placeholder/localization keys only.

## In scope

Concrete implementation tasks authorized by this story:

- Add a minimal pure-domain flat hex coordinate model.
- Add deterministic neighbor lookup for the chosen hex coordinate representation.
- Add a tiny authored/test tactical board definition sufficient for one guarded-site battle.
- Add tactical stack placement from `BattleSetup` attacker/defender army snapshots.
- Support exactly the closeout-slice minimum by default:
  - one attacker-side stack;
  - one neutral-guard defender stack;
  - legal spawn/placement hexes for both sides.
- Add occupancy validation and invalid-placement diagnostics.
- Add a minimal visual board/stack marker representation only if needed to prove the board exists in Unity; otherwise keep this story domain/test-focused.

## Out of scope

- Movement, pathfinding beyond neighbor/range basics, attacks, damage, tactical AI, battle end, `BattleResult` return.
- AP economy, initiative, abilities, morale, LOS, cover, objectives, operations, status effects.
- Tactical scene polish, final UI/art/icons/animation/audio, balance, roster design.
- Strategic site control, rewards, result application, recruitment, larger map content.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder tactical board ID, hex coordinates, stack IDs, guard-side IDs, and localization keys.
- Test-local `BattleSetup` fixtures matching STORY-TAC-001.
- Minimal stack stat fields required only for placement/identity.

Not allowed:

- Fabricated combat result or deterministic auto-win path.
- Tactical mutation of strategic state.
- Final unit/faction/site content decisions.

## Dependencies

- Required prior stories:
  - STORY-TAC-001 battle setup/result DTO contracts.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required Unity/package setup:
  - Existing Unity project and CI from SPIKE-001.

## Acceptance criteria

- [ ] Given a valid `BattleSetup`, when the tactical board initializes, then attacker and defender stack snapshots are converted into tactical stack entities and placed on legal unoccupied hexes.
- [ ] Given occupied, missing, or invalid hex coordinates, when placement validates, then validation fails with clear diagnostics and no partial board state is accepted.
- [ ] Given the hex coordinate model, when neighbor lookup runs from representative coordinates, then it returns the expected deterministic six-neighbor set.
- [ ] Given attacker/defender army snapshots mutate after board creation in a test, then tactical placed-stack snapshots remain stable.
- [ ] Domain logic compiles without UnityEngine, scene, prefab, camera, input, or final UI dependencies unless isolated in presentation adapters.
- [ ] CI passes.

## Verification requirements

- Unity edit-mode tests: Required for hex coordinate equality, neighbor lookup, board creation, placement, occupancy, snapshot stability, invalid diagnostics.
- Unity play-mode tests: N/A unless scene/presentation is touched.
- Integration/data validation tests: Required if serialized board fixtures or validators are added.
- Manual Unity scene/prefab checks: Required only if scene/presentation is touched.
- Screenshot/video evidence: Required only if scene/presentation is touched.
- Performance budget or N/A: N/A for tiny board/domain validation.
- CI evidence: Required on implementation PR.
- TDD evidence required? Yes.
- Automation deferred? No.

If a verification type is N/A, the PR must say why.

## Ambiguity Check

Status: PASS-candidate.

Resolved by user on 2026-06-04:

- Minimal real tactical combat should be built for the current closeout slice.
- Tactical combat should use a hex grid.

Assumptions for human approval:

- A tiny fixed board and exactly one attacker stack + one guard stack are acceptable for this story.
- No final tactical scene is required unless implementer can add a safe placeholder view without scope drift.

If these assumptions are rejected, revise before marking READY.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-002-minimal-hex-board-stack-placement`
- PR title: `STORY-TAC-002 Minimal hex board and stack placement`
- Required linked story ID: `STORY-TAC-002`
- Required evidence summary: RED/GREEN TDD summary, hex/placement tests, CI link/status, omissions section.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest sources are linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [x] Ambiguity Check is PASS-candidate.
- [x] Branch / PR / CI traceability requirements are stated.
- [ ] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests/validators/PlayMode evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY-candidate pending human approval.
