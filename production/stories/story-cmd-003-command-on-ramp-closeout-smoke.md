---
title: STORY-CMD-003 Command On-Ramp Closeout Smoke
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
  ]
approval: approved
---

# Story: STORY-CMD-003 Command On-Ramp Closeout Smoke

## Status

READY / approved for Codex implementation. Human requested merge of `STORY-CMD-002` and preparation of the next implementation story on 2026-06-13; this records that delegated approval for the immediate EPIC-005 closeout smoke packet.

This is the third child story for `EPIC-VSLICE-MVP-005`. It must prove the Champion Command on-ramp as a connected vertical-slice smoke: strategic setup enters tactical combat, a Champion command profile is visible, Command is spent through the approved CMD-002 actions, and battle resolution returns to the strategic layer with evidence.

## Story type

Connected Smoke + Evidence + PlayMode/Presentation Verification.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp.md`

## User/player/system value

As a player/reviewer, I want one connected smoke path that demonstrates Champion command identity from strategic context through tactical Command spending and back to battle result feedback, so EPIC-005 can be judged as a real on-ramp rather than isolated mechanics.

## Source requirements

- GDD path + section/rule:
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
- Parent epic:
  - `production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp.md`.

Source-authority decision: the same narrow implementation-source exception from EPIC-005, CMD-001, and CMD-002 applies. The Champion Operations split article has draft/pending front matter, but this story may use the cited sections only to verify the already-approved Marshal/Operator poles, finite Command visibility, `rally_order`, `drone_strike`, and connected smoke evidence.

## In scope

- Add or update a connected automated PlayMode smoke path that proves:
  - strategic state can launch tactical combat with Champion command profile visible;
  - `marshal_alpha` can visibly use `rally_order` after taking damage;
  - `operator_alpha` can visibly use `drone_strike`;
  - Command current/maximum values visibly update after spending;
  - at least one command-spending path can continue to a real battle result and return strategic result feedback.
- Capture PNG evidence for the connected path under `production/evidence/STORY-CMD-003/`.
- Add/update lightweight EditMode or PlayMode assertions for smoke sequencing if needed.
- Update evidence README with exact story scope, command sequence, screenshots, CI run expectations, and omissions.
- Preserve all CMD-001/CMD-002 behavior and tests.

## Out of scope

- No new Champion command effects beyond `rally_order` and `drone_strike`.
- No full Operations/spellbook UI.
- No new Command economy rules, regeneration, cooldowns, round cadence, reactions, interrupts, initiative changes, or action economy redesign.
- No new Champion classes, skills, Doctrine/passive mechanics, levels, progression, loadouts, perks, equipment, or strategic AI command usage.
- No Intel integration, Field Upgrade replacement, operation upgrades, dirty information, fog/hidden information, save/load, campaign persistence, or final faction/canon changes.
- No final art, icons, portraits, VFX, audio, animation, final operation names, or balance claims.
- No EPIC-005 closeout decision by implementation agent; implementation may produce evidence, but human/design-control closeout remains separate.

## Allowed stubs, mocks, placeholders, or temporary data

- Use existing placeholder command/profile IDs and labels only:
  - `marshal_alpha`, `operator_alpha`.
  - `rally_order` / `Rally Order`.
  - `drone_strike` / `Drone Strike`.
- Existing deterministic target fallback for Drone Strike remains allowed and must be documented as a placeholder if used in the smoke.
- Minimal text/button UI and generated PNG evidence are sufficient; final presentation polish is out of scope.

## Dependencies

- Required prior stories:
  - `STORY-CMD-001` DONE / merged.
  - `STORY-CMD-002` DONE / merged.
- Required data/assets:
  - Existing placeholder scenario/champion/faction data.
  - Existing command profiles and command pair.
- Required architecture decisions:
  - Existing Unity technical scheme and control manifest.
- Required Unity/package setup:
  - Existing Unity Foundation CI.

## Acceptance criteria

- [ ] Given the smoke starts from strategic state, when the relevant battle is launched, then tactical mode displays a Champion command profile and current/maximum Command.
- [ ] Given a Marshal-like Champion stack has taken damage, when `rally_order` is used in the smoke, then the evidence shows the Rally Order result and updated Command value.
- [ ] Given an Operator-like Champion has a legal opposing target, when `drone_strike` is used in the smoke, then the evidence shows the Drone Strike result, updated Command value, and target damage.
- [ ] Given the command-spending smoke continues to battle conclusion, then a real BattleResult is applied and visible strategic result feedback is captured or asserted.
- [ ] Given the smoke path uses any deterministic target fallback or minimal UI shortcut, then the evidence README explicitly lists it as a placeholder/omission.
- [ ] Given this story is closeout evidence only, then no new command mechanics, progression, final content, or broader systems are added.

## Verification requirements

- Unity edit-mode tests: only as needed for any smoke sequencing helper changes; existing CMD-001/CMD-002 domain tests must remain green.
- Unity play-mode tests: connected command on-ramp smoke with PNG evidence for Marshal Rally, Operator Drone Strike, and strategic/tactical result feedback.
- Screenshot/video evidence: PNG evidence under `production/evidence/STORY-CMD-003/` with a README explaining the sequence.
- CI evidence: Unity Foundation CI exact-head required before merge.
- Performance budget or N/A: N/A; smoke/evidence only.
- Playtest evidence, if applicable: N/A; evidence informs later human closeout/playtest review.
- TDD evidence required? Yes for any production logic changed; this story should prefer test/evidence additions over new runtime mechanics.
- Automation deferred? No for the closeout smoke; final polish/art/audio remain out of scope.

## Ambiguity Check

Status: PASS

Open questions:

- None for CMD-003 implementation.

Assumptions:

- This story is evidence/connected-smoke only; it should not add new Champion command mechanics.
- Human/design-control closeout of EPIC-005 happens after reviewing the smoke evidence; Codex does not mark the epic DONE by itself.

Out of scope:

- New mechanics, full Operations UI, economy/cooldown/regeneration systems, Intel integration, progression, final content, and EPIC-005 closeout decision.

Allowed stubs/mocks:

- Existing placeholder scenario data, placeholder command IDs/labels, deterministic target fallback if already used, minimal text/button presentation.

Human-approved exceptions:

- Narrow source-authority exception approved for cited Champion Operations sections despite draft/pending front matter.
- Human request on 2026-06-13 to merge CMD-002 and prepare the next story is recorded as approval for this immediate closeout-smoke implementation packet.

## Branch / PR requirements

- Branch name: `story/STORY-CMD-003-command-on-ramp-closeout-smoke`
- PR title: `STORY-CMD-003 Command on-ramp closeout smoke`
- Required linked story ID: `STORY-CMD-003`
- Required linked GDD/ADR/control docs: tactical combat Champion Operations sections, strategic map handoff sections, control manifest, testing strategy, CI automation.
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

READY for Codex implementation. Implement a connected closeout smoke/evidence path for the approved Champion Command on-ramp only; do not add new command mechanics or mark EPIC-005 DONE from implementation alone.
