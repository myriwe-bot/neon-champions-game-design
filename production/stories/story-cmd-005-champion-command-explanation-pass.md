---
title: STORY-CMD-005 Champion Command Explanation Pass
type: story
status: ready
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-14
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp,
    production/sprints/epic-005-playability-repair-train,
    production/stories/story-cmd-004-tactical-command-usability-and-targeting-pass,
    production/stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass,
    production/stories/story-qa-007-champion-encounter-initiation-clarity,
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/champion-operations-and-progression,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-CMD-005 Champion Command Explanation Pass

## Status

READY / approved for Codex implementation. `STORY-QA-007` is DONE / merged in Unity PR #45, and the user request to merge QA-007 and prepare the next implementation packet is recorded as delegated approval for this immediate repair-train follow-up.

This story remains a narrow explanation/readability pass for the already-implemented prototype Champion commands. It is not approval to add new command mechanics or broaden EPIC-005.

## Story type

Tactical UI/UX + Explanation Copy + PlayMode Evidence.

## Parent epic / train

- Parent epic: `production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp.md`.
- Repair train: `production/sprints/epic-005-playability-repair-train.md`.

## Human playtest source

The player reported:

- Rally Order availability is visible, but what it does is unclear.
- Rally Order denial/result is not understood.
- Drone Strike availability is visible, but what it does and target meaning are unclear.
- Second-use denial is not understood.
- Rally Order and Drone Strike do not yet feel differentiated.
- Marshal vs Operator identity is not yet clear.

Preserve this complaint as first-class acceptance authority. Do not dilute it into generic UI polish.

## Player/design value

Make the two existing prototype commands read as Champion command identities rather than unexplained buttons: Marshal as army reliability / rallying discipline, Operator as battle-level remote intervention / fire-support control.

## Source requirements

- GDD path + section/rule:
  - `design/gdd/tactical-combat.md` §§1-3 for fast, readable tactical battle goals and limited Champion support.
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§29-80 for Marshal/Operator poles and Command/Operations/Doctrine definitions.
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§93-155 for first command/operation examples, finite Command, no default regeneration, and cadence direction.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Prior stories:
  - `STORY-CMD-001` DONE / merged.
  - `STORY-CMD-002` DONE / merged.
  - `STORY-CMD-003` DONE / merged.
  - `STORY-CMD-004` DONE / merged.
  - `STORY-QA-006` DONE / merged.
  - `STORY-QA-007` DONE / merged.

Source-authority decision: the same narrow implementation-source exception from EPIC-005 applies. The Champion Operations split article has draft/pending front matter, but this story may use the cited sections only to explain and label the already-approved `rally_order` and `drone_strike` prototype mechanics and Marshal/Operator poles. It does not approve new command effects, broader Operations systems, final balance, Bio/Echo channels, progression, lore names, or faction-locked suites.

## In scope

- Add concise player-facing command explanations for existing commands only:
  - Marshal: `rally_order` / `Rally Order`.
  - Operator: `drone_strike` / `Drone Strike`.
- Explain what each command does, when it works, what it costs, and why it may be denied.
- Make Marshal vs Operator prototype identity legible in the current tactical HUD/panels.
- Differentiate Rally Order from Drone Strike in text: recovery/reliability vs targeted remote strike/intervention.
- Show current Command state, cost, one-use/major-slot limits, and relevant target/result summary in compact prototype-safe text.
- Improve command result/denial wording where needed without changing domain mechanics.
- Add/update PlayMode smoke evidence under `production/evidence/STORY-CMD-005/` proving the explanations are visible in valid and denied states.

## Out of scope

- No new Champion command effects beyond the existing `rally_order` and `drone_strike`.
- No balance changes to costs, damage, healing, command pools, one-use limits, or profile stats.
- No new Command economy, cooldowns, regeneration, round cadence, reactions, interrupts, initiative, or action economy redesign.
- No full Operations/spellbook UI.
- No new Champion classes, skills, Doctrine/passives, levels, progression, loadouts, perks, equipment, or strategic AI command usage.
- No Intel integration, operation upgrades, dirty information, fog/hidden information, save/load, campaign persistence, or final faction/canon changes.
- No final art, icons, portraits, VFX, audio, animation, final command names, or lore copy.
- No objective/capture redesign or EPIC-005 closeout decision by the implementation agent.

## Allowed stubs, mocks, placeholders, or temporary data

- Existing placeholder command/profile IDs and labels only:
  - `marshal_alpha`, `operator_alpha`.
  - `rally_order` / `Rally Order`.
  - `drone_strike` / `Drone Strike`.
- Minimal text/button/panel UI is sufficient if player-legible and covered by tests/evidence.
- Existing placeholder tactical board/stack IDs may be used in tests and evidence.

## Dependencies

- `STORY-CMD-004`, `STORY-QA-006`, and `STORY-QA-007` are DONE / merged.
- Existing Unity Foundation CI remains available.
- Existing placeholder scenario/champion/faction/command data remains valid.

## Acceptance criteria

- [ ] Given a Marshal tactical battle, the UI explains Rally Order as a Marshal-style command, what it does, its Command cost, and the damaged-friendly-stack condition for useful application.
- [ ] Given Rally Order is invalid, denial feedback explains the reason in player-facing terms and no board/Command state mutation occurs.
- [ ] Given an Operator tactical battle, the UI explains Drone Strike as an Operator-style operation/intervention, what it does, its Command cost, the enemy target meaning, and the one-Major-Operation-per-battle limit.
- [ ] Given Drone Strike was already used or otherwise invalid, denial feedback explains the reason in player-facing terms and no board/Command state mutation occurs.
- [ ] Given command state changes after valid command use, the tactical HUD command explanation/summary updates immediately.
- [ ] Given Marshal and Operator profiles are shown, their prototype identities are textually distinct enough that a player can describe the difference without reading external docs.
- [ ] Given this is an explanation pass, no new command mechanics, progression, final content, objective rules, or broader Operations systems are added.
- [ ] Existing QA-006 and QA-007 readability/encounter clarity feedback remains visible and is not regressed.

## Verification requirements

- Unity edit-mode tests: add/update no-mutation and explanation-state tests if application/domain helpers change.
- Unity play-mode tests: command explanation smoke with PNG evidence under `production/evidence/STORY-CMD-005/`.
- Screenshot/video evidence: PNG evidence for Marshal Rally explanation, Rally denial explanation, Operator Drone Strike explanation/target meaning, and second-use/invalid Drone Strike explanation.
- CI evidence: Unity Foundation CI exact-head required before merge.
- Performance budget or N/A: N/A; UI/UX explanation story only.
- Playtest evidence, if applicable: N/A; evidence informs later human closeout/playtest review.
- TDD evidence required? Yes for any production logic changed; pure presentation changes still require PlayMode coverage.
- Automation deferred? No for in-scope explanation smoke; final polish/art/audio remain out of scope.

## Ambiguity Check

Status: PASS.

Open questions:

- None for this implementation packet.

Assumptions:

- Implementation improves wording, labels, panels, snapshots, and evidence for the existing two commands only.
- Minimal prototype text is acceptable if it is readable and testable.
- Marshal/Operator identity may be explained as prototype archetype poles, not final fixed classes.

Out of scope:

- New mechanics, full Operations UI, economy/cooldown/regeneration systems, Intel integration, progression, final content, and EPIC-005 closeout decision.

Allowed stubs/mocks:

- Existing placeholder scenario data, placeholder command IDs/labels, placeholder stack IDs, minimal text/button presentation.

Human-approved exceptions:

- Narrow source-authority exception applies for cited Champion Operations sections despite draft/pending front matter.
- Human request on 2026-06-14 to merge QA-007 and prepare the next implementation packet authorizes this immediate repair-train follow-up.

## Branch / PR requirements

- Branch name: `story/STORY-CMD-005-champion-command-explanation-pass`.
- PR title: `STORY-CMD-005 Champion command explanation pass`.
- Required linked story ID: `STORY-CMD-005`.
- Required linked GDD/ADR/control docs: tactical combat Champion Operations sections, tactical combat readability goals, control manifest, testing strategy, CI automation.
- Required root/scoped AGENTS.md instructions: Unity root plus scoped files touched.
- Required evidence summary: tests, PlayMode PNG evidence, CI run URLs, omissions.
- Required omissions section: must state known omissions or `No known omissions`.

## Story readiness gate

- [x] Status and approval marker: READY / approved.
- [x] Source documents named.
- [x] Acceptance criteria are testable/inspectable.
- [x] Out-of-scope boundaries are explicit.
- [x] Dependencies and sequencing are explicit.
- [x] Estimate/size: Small UI/UX explanation pass.
- [x] Test/evidence expectations are explicit.
- [x] Branch/PR scope guidance is explicit.

## Story DONE gate

- [ ] Implementation PR merged.
- [ ] Required tests and Unity Foundation CI exact-head pass.
- [ ] PlayMode evidence exists under `production/evidence/STORY-CMD-005/`.
- [ ] No unauthorized command mechanics or broader Operations scope added.
- [ ] Omissions/deferred work documented.
- [ ] Post-merge `main` CI passes.
