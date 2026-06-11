---
title: STORY-TAC-008 Champion-vs-Champion Tactical Encounter Path
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-10
updated: 2026-06-11
source_lore: []
related:
  [
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes,
    production/stories/story-tac-007-simple-stack-strength-persistence,
  ]
approval: pending
---

# Story: STORY-TAC-008 Champion-vs-Champion Tactical Encounter Path

## Status

READY-candidate / approval pending. Draft expanded after `STORY-TAC-007` merged. This story is prepared for human review, but it is not READY and does not authorize Unity implementation until approval is changed to `approved` and the Ambiguity Check is changed to PASS.

## Story type

Tactical Integration + Strategic Encounter Routing + Smoke/Regression.

## Estimate

- Size: M.
- Basis: reuses the existing battle setup/result/application path and current placeholder tactical board, but adds a deterministic Champion-vs-Champion encounter trigger/path, side validation, outcome persistence, and visible feedback. It deliberately excludes strategic AI and full encounter systems.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes.md`.

## User/player/system value

As a vertical-slice tester, I need the game to support a controlled Champion-vs-Champion tactical encounter so Champion conflict can be exercised through the same tactical result model as guarded sites without pretending strategic AI or full PvP is done.

## Source requirements

- `design/gdd/strategic-map.md` §§8, 10, 11, 12, 13, 14 for Champion position/state, interaction affordances, tactical handoff, and result application.
- `design/gdd/tactical-combat.md` §§3-7 and post-battle/result sections for side setup, stacks-first combat, battle end, and return to strategic state.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Parent epic: `EPIC-VSLICE-MVP-003`.
- Baseline: Unity `main` after PR #30 / merge commit `d822018fed10715b97263d984d3418eb3da7475c`.

## Problem statement

The prototype can resolve guarded-site battles and persist simple attacker stack losses, but Champion-vs-Champion conflict is still only an epic-level direction. The next smallest useful step is a deterministic, player/test-triggered Champion encounter path that proves the existing battle setup/result/application model can carry Champion-vs-Champion combat without adding strategic AI.

## In scope

- Add a deterministic Champion-vs-Champion encounter path using existing Champion runtime state and tactical setup/result DTOs.
- Support a player/test-triggered encounter only when two active opposing Champions occupy an approved encounter context, such as the same node or a story-approved adjacent/interaction path already available in the current map slice.
- Produce a valid `BattleSetup` with `BattleType.ChampionVsChampion`, attacker side as the active/player Champion, defender side as the opposing Champion, and stable faction/champion/army/stack identity.
- Route the encounter through the existing tactical handoff/board/result path where feasible.
- Apply the resulting `BattleResult` back to strategic Champion state using the existing result application boundaries, including simple attacker stack persistence from TAC-007 where applicable.
- Mark defeated Champion state when the result indicates a Champion/army defeat, without adding healing/recovery/campaign systems.
- Add minimal placeholder visible feedback that a Champion-vs-Champion battle occurred and which side won/lost.
- Add automated tests for valid setup, invalid same-faction/missing/inactive Champion cases, result side/outcome consistency, no partial mutation on invalid result data, and regressions for guarded-site results.
- Add PlayMode smoke and PNG evidence showing a deterministic Champion-vs-Champion encounter and result feedback.

## Out of scope

- Strategic AI, pursuit, autonomous enemy decisions, or enemy-initiated encounters.
- Full encounter system, diplomacy, zone-of-control, ambushes, scouting, or PvP UX.
- New tactical abilities, cover, LOS, morale, healing, ammo, status effects, or final combat balance.
- Full casualty/healing/recovery economy or post-defeat revival rules.
- Save/load, campaign progression, or full loss/victory structure beyond existing placeholder victory hooks.
- Final Champion names, factions, units, lore copy, portraits, animation, VFX, audio, final UI/art/accessibility.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Deterministic test-triggered or debug interaction for Champion-vs-Champion encounter setup.
- Existing placeholder Champion, faction, unit, stack, and localization IDs.
- Minimal placeholder result text such as `Champion battle: attacker won` and stack count deltas already supported by TAC-007.
- Existing crude tactical board/stack visuals.

Not allowed:

- Hidden strategic mutation outside result-application services.
- Treating a failed/invalid Champion result as partially applied state.
- Inventing final strategic AI, combat balance, Champion lore, or casualty systems.
- Broad DTO redesign beyond the minimal Champion-vs-Champion fields/validation needed for this story.

## Dependencies

- Required prior story:
  - `STORY-TAC-007` DONE / merged in Unity PR #30.
- Required architecture decisions:
  - Existing battle setup/result/application boundaries remain binding.
  - Current Unity root/scoped `AGENTS.md` rules remain binding.
- Required data/assets:
  - Existing placeholder Champion armies/stacks are sufficient unless implementation discovers a missing stable ID; if so, stop rather than invent final content.

## Acceptance criteria

- [ ] Given two active opposing Champions in the approved encounter context, the player/test path can create a `ChampionVsChampion` battle setup with correct attacker/defender faction, Champion, controller, army, and stack identity.
- [ ] Given same-faction, missing, inactive, defeated, or armyless Champion inputs, encounter setup fails with diagnostics and does not mutate strategic state.
- [ ] Given invalid side/outcome/result payloads for a Champion-vs-Champion battle, result application fails with diagnostics and no partial mutation.
- [ ] Given a valid Champion-vs-Champion battle result, strategic Champion/army state updates through the approved result application path.
- [ ] Given a defeated Champion/army result, the defeated Champion state is visible in placeholder status/feedback without adding recovery systems.
- [ ] Given a non-defeating result with stack losses, TAC-007 attacker stack persistence still applies for participating attacker stacks where the current result model supports it.
- [ ] Existing guarded-site objective, defender-tier, and stack-persistence flows still pass.
- [ ] Minimal visible feedback communicates that a Champion-vs-Champion encounter occurred and reports the result.
- [ ] PlayMode smoke and PNG evidence show the deterministic Champion encounter and result feedback.
- [ ] CI passes.

## Verification requirements

- Unit/EditMode tests: required for setup validation, result application, invalid/no-partial-mutation cases, and guarded-site regressions.
- Unity PlayMode tests: required for deterministic Champion encounter path and visible feedback.
- Placeholder validator: must remain passing.
- Screenshot/video evidence: PNG evidence required under `production/evidence/STORY-TAC-008/` or equivalent story evidence path.
- CI evidence: required on PR branch and post-merge main if merged.
- TDD evidence required? Yes for validation/result semantics.
- Automation deferred? No, except final visual judgement is supplemental.

## Ambiguity Check

Status: FAIL until human approval.

Open questions for human review:

1. What exact MVP encounter context should trigger Champion-vs-Champion for this story: same node only, selected adjacent enemy Champion, or a deterministic test/debug interaction?
2. Should defeated Champion state reuse the current `ChampionStatusFlags.Defeated` semantics only, or should this story stop before any strategic victory/loss side effect beyond visible status?
3. Is minimal placeholder feedback text enough, or should the existing battle-result panel explicitly name both Champion placeholder IDs?

Assumptions for review:

- The smallest safe implementation is deterministic/player-test-triggered, not strategic AI.
- Same-node encounter is likely the narrowest trigger unless the human chooses adjacent selection.
- Existing placeholder IDs are acceptable; no final Champion identity/content work is authorized.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-008-champion-vs-champion-tactical-encounter-path`
- PR title: `STORY-TAC-008 Champion-vs-Champion tactical encounter path`
- Required linked story ID: `STORY-TAC-008`
- Required evidence summary: setup/result contract, invalid/no-partial-mutation tests, defeated Champion/status feedback, guarded-site regressions, PlayMode/PNG evidence, CI, omissions.
- Required omissions section: no strategic AI, no full encounter system, no healing/recovery/casualty economy, no final content/balance/lore, no final UI/art/accessibility.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest sources are linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [ ] Ambiguity Check status is PASS.
- [ ] Human approval has been given for implementation / READY promotion.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence pass.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY-candidate / approval pending. Next human step: choose the Champion encounter trigger semantics and approve or revise this packet before Codex implementation.
