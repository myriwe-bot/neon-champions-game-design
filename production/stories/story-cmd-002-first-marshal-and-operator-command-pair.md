---
title: STORY-CMD-002 First Marshal and Operator Command Pair
type: story
status: done
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
  ]
approval: approved
---

# Story: STORY-CMD-002 First Marshal and Operator Command Pair

## Status

DONE / merged. Unity PR #41 implemented and merged on 2026-06-13 after merge-gate review, review fixes, exact-head CI, and post-merge `main` CI passed.

This is the second child story for `EPIC-VSLICE-MVP-005`. It adds the first active, finite Command spending proof: one Marshal-like Minor Command and one Operator-like Major Operation. It must remain a narrow prototype pair, not a full Operations system.

## Story type

Tactical Rules + UI/Integration + PlayMode Smoke.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp.md`

## User/player/system value

As a player, I want one Marshal command and one Operator operation to spend finite Command during battle, so that Champion command profiles start producing distinct tactical interventions instead of only passive HUD labels.

## Source requirements

- GDD path + section/rule:
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§29-80 for Marshal/Operator poles and Command/Operations/Doctrine definitions.
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§93-98 for example Marshal commands and Operator operations.
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§98-155 for finite Command, no default regeneration, Major Operation cadence, and Minor Command direction.
  - `design/gdd/strategic-map.md` §§6, 7, 14 for Champion strategic state and strategy-to-tactical handoff context.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Prior story:
  - `production/stories/story-cmd-001-champion-command-archetype-state-and-tactical-hud.md` DONE / merged.
- Parent epic:
  - `production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp.md`.

Source-authority decision: human-approved narrow implementation-source exception inherited from EPIC-005 and CMD-001. The Champion Operations split article has draft/pending front matter, but this story may use the cited sections for Marshal/Operator poles, finite Command, one Marshal Minor Command, and one Operator Major Operation only.

## Approved first command pair

### Marshal Minor Command: `rally_order`

- Display label: `Rally Order`.
- Profile access: `marshal_alpha` only.
- Type: Minor Command.
- Channel/flavor: Doctrine.
- Cost: 1 Command.
- Timing: during an allied stack activation before the battle is complete.
- Effect: restore 1 current stack count to the currently active allied stack, capped at that stack's starting/current maximum count.
- Restrictions:
  - Cannot target defeated stacks.
  - Cannot increase a stack above its starting/current maximum count.
  - Cannot be used if current Command is below cost.
  - Cannot be used by `operator_alpha`.
  - Does not revive a defeated / zero-count stack.

### Operator Major Operation: `drone_strike`

- Display label: `Drone Strike`.
- Profile access: `operator_alpha` only.
- Type: Major Operation.
- Channel/flavor: Fire Support.
- Cost: 2 Command.
- Timing: during an allied stack activation before the battle is complete.
- Effect: apply 1 direct damage to one opposing, non-defeated tactical stack.
- Restrictions:
  - Requires `Major Operation Slots >= 1`.
  - At most one Major Operation may be used per battle in this MVP story; do not add round/cooldown infrastructure yet.
  - Cannot target allied, missing, or defeated stacks.
  - Cannot be used if current Command is below cost.
  - Cannot be used by `marshal_alpha`.

These are prototype mechanics for this story only. They do not establish final balance, final operation names, final targeting UI, operation channels, skill trees, Doctrine, cooldown rules, or round-based cadence.

## In scope

- Add an explicit finite Command spending path to tactical runtime state for the existing CMD-001 command profiles.
- Implement exactly two active command definitions/effects:
  - `rally_order` for `marshal_alpha`.
  - `drone_strike` for `operator_alpha`.
- Deduct Command on successful command/operation use only.
- Expose current/maximum Command after spending in tactical presentation/HUD/status.
- Add minimal tactical UI affordance(s) sufficient to trigger or smoke-test the two approved actions if existing presentation architecture supports it cleanly.
- Add deterministic validation and diagnostics for invalid profile, insufficient Command, invalid target, defeated target, battle complete, and major-operation-already-used cases.
- Add tests for allowed use, denial cases, Command deduction/no-deduction, capped Rally restore, Drone Strike damage, and presentation/HUD updates.
- Add PlayMode evidence proving both command profiles can spend Command and the HUD/status updates visibly.

## Out of scope

- No full Operations/spellbook UI.
- No more than `rally_order` and `drone_strike`.
- No new Champion classes, levels, skills, Doctrine/passive mechanics, loadouts, perks, equipment, or progression UI.
- No final operation names, lore copy, icons, portraits, animations, VFX, audio, or balance claims.
- No Command regeneration.
- No round system, cooldown system, reaction/interrupt timing, initiative rewrite, or broad action economy redesign.
- No Intel integration, Field Upgrade replacement, operation upgrades, tactical Intel rewards, dirty information, fog/hidden information, save/load, strategic AI usage, or campaign persistence.
- No changes to final faction identity/canon.

## Allowed stubs, mocks, placeholders, or temporary data

- Placeholder command IDs and labels are approved for this story only:
  - `rally_order` / `Rally Order`.
  - `drone_strike` / `Drone Strike`.
- Prototype costs/effects are approved for this story only:
  - `rally_order`: cost 1, restore 1 current stack count capped at the stack's starting/current maximum.
  - `drone_strike`: cost 2, deal 1 direct damage to one enemy stack, at most once per battle.
- Minimal button/text presentation is allowed; final icons/VFX are explicitly out of scope.
- If tactical UI implementation cannot cleanly expose arbitrary target choice yet, Codex may use the current legal opposing target / deterministic first enemy target for the MVP smoke, provided tests document the behavior and the PR lists it as a known placeholder.

## Dependencies

- Required prior stories:
  - `STORY-CMD-001` DONE / merged.
- Required data/assets:
  - Existing `marshal_alpha` and `operator_alpha` profile state from CMD-001.
  - Placeholder text only.
- Required architecture decisions:
  - Existing Unity technical scheme and control manifest.
- Required Unity/package setup:
  - Existing Unity Foundation CI.

## Acceptance criteria

- [ ] Given a Marshal tactical state with `marshal_alpha` and at least 1 Command, when `rally_order` is used on the currently active allied stack that is below its starting/current maximum count, then Command decreases by 1 and the stack current count increases by 1 without exceeding its cap.
- [ ] Given a Marshal tactical state with full-health current stack, when `rally_order` is attempted, then the action is rejected, no Command is deducted, and a diagnostic/status message explains the cap/no-op.
- [ ] Given an Operator tactical state with `operator_alpha`, at least 2 Command, and an opposing non-defeated target stack, when `drone_strike` is used, then Command decreases by 2 and the target stack takes exactly 1 direct damage using the existing stack-count/defeat rules.
- [ ] Given `drone_strike` has already succeeded once in the battle, when another Major Operation is attempted, then the action is rejected, no Command is deducted, and the denial is visible/tested.
- [ ] Given a profile tries to use the other profile's command (`marshal_alpha` using `drone_strike` or `operator_alpha` using `rally_order`), then the action is rejected and no Command is deducted.
- [ ] Given insufficient Command, missing/invalid target, defeated target, allied target for Drone Strike, defeated active stack for Rally, missing board, or completed battle, then the command is rejected safely without partial mutation.
- [ ] Given command/operation spending succeeds or fails, then tactical HUD/status reflects current/maximum Command and a concise result/denial message.
- [ ] Given the existing attack/move/end-turn controls, then their prior behavior remains covered by tests and is not broadened into an unapproved action economy rewrite.

## Verification requirements

- Unit/domain tests: command definition/validation/spend helpers if pure domain logic is added.
- Unity edit-mode tests: tactical command session spending, invalid-denial cases, Command deduction/no-deduction, Rally cap, Drone Strike damage/defeat, major-operation-once-per-battle, and presentation snapshot/status output.
- Unity play-mode tests: smoke path showing Marshal `Rally Order` spend and Operator `Drone Strike` spend with visible Command/HUD/status updates.
- Integration/data validation tests: required if command definitions are authored as data assets/fixtures.
- Manual Unity scene/prefab checks: N/A unless scene/prefab edits are required; prefer code/test changes.
- Screenshot/video evidence: PNG evidence of tactical HUD/status after each successful command/operation spend.
- Performance budget or N/A: N/A; small tactical state/action logic only.
- CI evidence: Unity Foundation CI exact-head required before merge.
- Playtest evidence, if applicable: N/A for this first command-spending proof.
- TDD evidence required? Yes for production logic and bug fixes.
- Automation deferred? No, except final art/VFX/audio are out of scope.

## Ambiguity Check

Status: PASS

Open questions:

- None for CMD-002 implementation.

Assumptions:

- Marshal and Operator remain archetype poles, not final rigid classes.
- `rally_order` and `drone_strike` are placeholder prototype actions for proving Command spending only.
- At most one Major Operation per battle is an explicit MVP simplification replacing full round/cadence infrastructure for this story.

Out of scope:

- Full Operations UI/spellbook, command trees, round/cooldown/reaction systems, Command regeneration, final content, Intel integration, and progression.

Allowed stubs/mocks:

- Placeholder command IDs/labels, deterministic target fallback if UI target choice is not clean yet, and minimal text/button presentation.

Human-approved exceptions:

- Narrow source-authority exception approved for cited Champion Operations sections despite draft/pending front matter.
- Prototype command pair, costs, and effects approved for CMD-002 only.

## Branch / PR requirements

- Branch name: `story/STORY-CMD-002-first-marshal-operator-command-pair`
- PR title: `STORY-CMD-002 First Marshal and Operator command pair`
- Required linked story ID: `STORY-CMD-002`
- Required linked GDD/ADR/control docs: tactical combat Champion Operations sections, strategic map handoff sections, control manifest, testing strategy, CI automation.
- Required root/scoped AGENTS.md instructions: Unity root plus scoped files touched.
- Required evidence summary: tests, PlayMode evidence, CI run URLs, omissions.
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

DONE / merged. Implemented exactly one Marshal Minor Command (`rally_order`) and one Operator Major Operation (`drone_strike`) with finite Command spending, bounded validation, presentation feedback, tests, and PlayMode evidence.

## Implementation evidence

- Unity PR: https://github.com/myriwe-bot/neon-champions-unity/pull/41
- Branch head reviewed before merge: `59865fbc9840111fdeb741799194c9a10b5c810a`
- Merge commit on main: `73a15d98d24a93857405bcdff09c3f20ddac498c`
- PR exact-head CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27467133863
- Post-merge main CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27467415661
- Required jobs passed: Compile / Standalone Check, EditMode Tests, PlayMode Smoke Tests, Placeholder Validator.
- Review verdict: PASS, recorded on PR.
- Gate fixes during review: null-safe Drone Strike fallback, null-safe tactical presentation population for missing placed-stack collections, and added denial/no-partial-mutation regression coverage.
- Omissions/deferred: no full Operations UI, no additional command effects, no Command regeneration/cooldowns/round cadence/reactions, no progression, no final art/lore/UI/VFX/audio, no Intel integration, no strategic AI usage, no save/load.
