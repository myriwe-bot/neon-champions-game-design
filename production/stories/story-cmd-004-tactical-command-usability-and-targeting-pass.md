---
title: STORY-CMD-004 Tactical Command Usability and Targeting Pass
type: story
status: ready
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-13
source_lore: [champions]
related:
  [
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/champion-operations-and-progression,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp,
    production/stories/story-cmd-001-champion-command-archetype-state-and-tactical-hud,
    production/stories/story-cmd-002-first-marshal-and-operator-command-pair,
    production/stories/story-cmd-003-command-on-ramp-closeout-smoke,
  ]
approval: approved
---

# Story: STORY-CMD-004 Tactical Command Usability and Targeting Pass

## Status

READY / approved for Codex implementation. Human approved continuing EPIC-005 and approved this next story on 2026-06-13 after `STORY-CMD-003` merged.

This story keeps EPIC-005 open for one narrow usability pass: the first Marshal/Operator command pair already exists, but the tactical controls must make those commands intentionally usable and legible to a player before adding more Champion systems.

## Story type

Tactical UI/UX + PlayMode Evidence + Validation Consistency.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp.md`

## User/player/system value

As a player, I can see which Champion command is available, understand whether I can use it, choose/apply it deliberately, and see why it succeeded or failed.

## Source requirements

- GDD path + section/rule:
  - `design/gdd/tactical-combat.md` §§1-3 for fast, readable tactical battle goals and limited Champion support.
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§29-80 for Marshal/Operator poles and Command/Operations/Doctrine definitions.
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§93-155 for first command/operation examples, finite Command, no default regeneration, and cadence direction.
  - `design/gdd/strategic-map.md` §§6, 7, 14 for strategic-to-tactical setup/result boundaries and Champion/army state context.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Prior stories:
  - `production/stories/story-cmd-001-champion-command-archetype-state-and-tactical-hud.md` DONE / merged.
  - `production/stories/story-cmd-002-first-marshal-and-operator-command-pair.md` DONE / merged.
  - `production/stories/story-cmd-003-command-on-ramp-closeout-smoke.md` DONE / merged.
- Parent epic:
  - `production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp.md`.

Source-authority decision: the same narrow implementation-source exception from EPIC-005 applies. The Champion Operations split article has draft/pending front matter, but this story may use the cited sections only to improve player-facing usability and targeting for the already-approved `rally_order` and `drone_strike`. It does not approve new command effects, broader Operations systems, final balance, Bio/Echo channels, or progression.

## In scope

- Tactical command UI affordances for existing commands only:
  - Marshal: `rally_order` / `Rally Order`.
  - Operator: `drone_strike` / `Drone Strike`.
- Clear command availability or disabled/denial state for:
  - enough Command;
  - correct command profile;
  - Major Operation already used;
  - valid target / damaged active stack;
  - battle not complete.
- Explicit target selection or clear target feedback for `Drone Strike`.
- Clear feedback text after valid and invalid command attempts.
- HUD command summary refresh after command state changes.
- PlayMode evidence showing:
  - Marshal Rally usable after damage;
  - Rally disabled/denied when invalid;
  - Operator Drone Strike target selection/use;
  - second Drone Strike denied visibly.
- Regression tests that UI-visible state matches domain validation and no invalid attempt mutates board/Command state.

## Out of scope

- No new Champion command effects beyond `rally_order` and `drone_strike`.
- No full Operations/spellbook UI.
- No new Command economy rules, regeneration, cooldowns, round cadence, reactions, interrupts, initiative changes, or action economy redesign.
- No new Champion classes, skills, Doctrine/passives, levels, progression, loadouts, perks, equipment, or strategic AI command usage.
- No Intel integration, Field Upgrade replacement, operation upgrades, dirty information, fog/hidden information, save/load, campaign persistence, or final faction/canon changes.
- No final art, icons, portraits, VFX, audio, animation, final operation names, or balance claims.
- No EPIC-005 closeout decision by implementation agent.

## Allowed stubs, mocks, placeholders, or temporary data

- Use existing placeholder command/profile IDs and labels only:
  - `marshal_alpha`, `operator_alpha`.
  - `rally_order` / `Rally Order`.
  - `drone_strike` / `Drone Strike`.
- Minimal text/button UI is sufficient, but it must be player-legible and testable.
- Existing placeholder tactical board/stack IDs may be used in tests and evidence.
- Deterministic fallback may remain internally, but the player-facing path should make target choice or selected target feedback explicit enough that the evidence does not depend on a hidden target guess.

## Dependencies

- Required prior stories:
  - `STORY-CMD-001` DONE / merged.
  - `STORY-CMD-002` DONE / merged.
  - `STORY-CMD-003` DONE / merged.
- Required data/assets:
  - Existing placeholder scenario/champion/faction data.
  - Existing command profiles and command pair.
- Required architecture decisions:
  - Existing Unity technical scheme and control manifest.
- Required Unity/package setup:
  - Existing Unity Foundation CI.

## Acceptance criteria

- [ ] Given a Marshal tactical battle, when the active stack is damaged, then Rally Order is visibly available or clearly usable and using it spends Command and restores count.
- [ ] Given Rally Order is invalid, then the UI shows a denial reason and no board/Command state mutation occurs.
- [ ] Given an Operator tactical battle, then Drone Strike requires/communicates a valid enemy target and spends Command on success.
- [ ] Given Drone Strike was already used, then a second attempt is visibly denied and Command does not change.
- [ ] Given command state changes, then the tactical HUD command summary updates immediately.
- [ ] Given domain validation rejects a command, then player-facing availability/denial state matches the domain reason instead of showing a contradictory affordance.
- [ ] Given this is a usability/targeting story, then no new command mechanics, progression, final content, or broader Operations systems are added.

## Verification requirements

- Unity edit-mode tests: add/update validation/no-mutation tests if any command availability or targeting helper changes touch domain/application logic.
- Unity play-mode tests: command usability/targeting smoke with PNG evidence under `production/evidence/STORY-CMD-004/`.
- Screenshot/video evidence: PNG evidence for valid Rally, invalid Rally denial, valid Drone Strike target/use, and second Drone Strike denial.
- CI evidence: Unity Foundation CI exact-head required before merge.
- Performance budget or N/A: N/A; UI/UX affordance story only.
- Playtest evidence, if applicable: N/A; evidence informs later human closeout/playtest review.
- TDD evidence required? Yes for any production logic changed; pure presentation changes still require PlayMode coverage.
- Automation deferred? No for the in-scope command usability smoke; final polish/art/audio remain out of scope.

## Ambiguity Check

Status: PASS

Open questions:

- None for CMD-004 implementation.

Assumptions:

- The story improves usability for the existing two command effects only.
- Minimal text/button presentation remains acceptable if legible and tested.
- Implementation may choose explicit target selection or selected-target feedback for Drone Strike, but must not hide success behind uncommunicated fallback behavior.

Out of scope:

- New mechanics, full Operations UI, economy/cooldown/regeneration systems, Intel integration, progression, final content, and EPIC-005 closeout decision.

Allowed stubs/mocks:

- Existing placeholder scenario data, placeholder command IDs/labels, placeholder stack IDs, minimal text/button presentation.

Human-approved exceptions:

- Narrow source-authority exception approved for cited Champion Operations sections despite draft/pending front matter.
- Human approval on 2026-06-13 authorizes this immediate EPIC-005 usability/targeting implementation packet.

## Branch / PR requirements

- Branch name: `story/STORY-CMD-004-tactical-command-usability-and-targeting-pass`
- PR title: `STORY-CMD-004 Tactical command usability and targeting pass`
- Required linked story ID: `STORY-CMD-004`
- Required linked GDD/ADR/control docs: tactical combat Champion Operations sections, tactical combat readability goals, strategic map handoff sections, control manifest, testing strategy, CI automation.
- Required root/scoped AGENTS.md instructions: Unity root plus scoped files touched.
- Required evidence summary: tests, PlayMode PNG evidence, CI run URLs, omissions.
- Required omissions section: must state known omissions or `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A with approved exception.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified or explicitly N/A.
- [x] UX/content/art/worldbuilding references are linked if relevant.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied or marked blocking.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed, or approved exceptions are documented.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY for Codex implementation. Improve player-facing usability and targeting for the existing `Rally Order` and `Drone Strike` command pair only; do not add new command mechanics or mark EPIC-005 DONE from implementation alone.
