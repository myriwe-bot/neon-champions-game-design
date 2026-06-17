---
title: STORY-TAC-AP-001 Minimal Tactical AP and Defend State
type: story
status: done
phase: production
owner: shared
created: 2026-06-16
updated: 2026-06-17
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency,
    production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed,
    production/stories/story-tac-ret-001-minimal-melee-retaliation,
    production/stories/story-tac-afford-001-movement-and-attack-affordance-pass,
    production/stories/story-tac-unit-001-minimal-unit-definition-stats,
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/ap-actions-and-reactions,
    production/planning/prototype-readability-and-map-next-steps-2026-06-15,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-TAC-AP-001 Minimal Tactical AP and Defend State

## Status

DONE / merged. Unity PR #53 merged 2026-06-17. Squash merge commit: `d2c55ad4820d64f6980a7cbf432f632bd4c17ce3`. Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27689580984

Original approval: Human approval recorded 2026-06-17: `STORY-TAC-AP-001` approved with a tiny prototype damage-reduction effect for Defend.

## Story type

Tactical Rules / Tactical UI / Presentation Readability.

## Parent epic

- [EPIC-VSLICE-MVP-006 Tactical Battle Readability and Defender Agency](../epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md)

## User/player/system value

As a player, I want the tactical UI to show how many actions the active stack can still take and to offer a simple Defend state when attacking or moving is not useful, so battles stop feeling like single-click exchanges and start communicating tactical tempo.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/tactical-combat.md` active tactical-combat first-read authority.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§28-91 for baseline 2 AP, Move/Basic Attack cost 1 AP, Wait posture, and Defend ending activation.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§93-118 for Defend / Brace direction.
- Planning source:
  - `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` §§5 Minimal AP + Defend bonus.
- ADR / architecture / control:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Parent/prior stories:
  - `production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed.md` DONE / merged.
  - `production/stories/story-tac-ret-001-minimal-melee-retaliation.md` DONE / merged.
  - `production/stories/story-tac-afford-001-movement-and-attack-affordance-pass.md` DONE / merged.
  - `production/stories/story-tac-unit-001-minimal-unit-definition-stats.md` DONE / merged.

## In scope

Concrete implementation tasks proposed by this story:

- Add minimal activation AP state to tactical board/session state:
  - baseline max/current AP = 2 for the active stack activation;
  - AP does not carry between activations;
  - refresh/reset behavior must be deterministic in the current prototype activation/session model.
- Make Move cost 1 AP.
- Make Basic Attack cost 1 AP.
- Reject Move / Basic Attack when current AP is insufficient, with clear diagnostics and event-feed/feedback text and no partial mutation.
- Add a minimal Defend action:
  - Defend ends the current stack activation / consumes remaining AP;
  - Defend sets a visible `Defending` state until the stack's next activation or the simplest equivalent reset point available in the current prototype;
  - Defend state is visible in tactical snapshot/HUD/event feed.
- Defend also applies a tiny prototype damage-reduction effect while the `Defending` state is active:
  - implement the smallest readable prototype rule available in the current damage pipeline;
  - document the exact temporary value/name in code comments, test names, event/feed text, or evidence notes;
  - this is not a final armor, shield, cover, damage-type, terrain, or defense formula.
- Surface current/max AP and Defend state through existing presentation snapshot, affordance summary, marker labels/cards, and denial feedback.
- Add focused tests for AP spend, insufficient-AP denial/no mutation, Defend state/reset visibility, and no regression to movement/attack/retaliation/unit-definition behavior.

## Out of scope

Not authorized by this story:

- No initiative order implementation or initiative manipulation.
- No Wait action unless separately approved; do not smuggle Wait into this slice.
- No AP carryover between turns/rounds.
- No heavy/signature 2 AP actions beyond preserving existing command actions.
- No AP cost changes for Champion Command operations unless strictly necessary to preserve current behavior and explicitly documented.
- No final armor, shields, damage types, cover, LOS, terrain, range falloff, ability system, status system, or final defense formula. The only defense effect authorized is the tiny prototype Defend damage-reduction effect approved for this story.
- No Zone of Control, opportunity attacks, Overwatch, CombatAI, or initiative.
- No strategic-map/base/recruitment/economy/topology changes.
- No final UI skin, icons, animation, VFX, audio, portraits, final lore copy, or localization pass.

## Allowed stubs, mocks, placeholders, or temporary data

- Prototype AP values may be code-side constants for this slice: baseline max AP 2; Move cost 1; Basic Attack cost 1.
- Human approval explicitly authorizes a tiny prototype Defend damage-reduction effect for this story; keep it temporary, obvious, and covered by tests.
- Placeholder UI text is allowed but must be player-facing, not debug-only.

## Dependencies

- Required prior stories:
  - `STORY-TAC-READ-002` DONE / merged.
  - `STORY-TAC-RET-001` DONE / merged.
  - `STORY-TAC-AFFORD-001` DONE / merged.
  - `STORY-TAC-UNIT-001` DONE / merged.
- Required data/assets:
  - Existing tactical board/session, presentation snapshot, event-feed/feedback, and PlayMode evidence surfaces.
- Required Unity/package setup:
  - Existing Unity project and CI.

## Acceptance criteria

- [ ] Given a stack is activated, the tactical state/snapshot exposes current AP and max AP as 2 / 2.
- [ ] Given the active stack moves legally, current AP decreases by 1 and the visible AP summary/event feed reflects the spend.
- [ ] Given the active stack attacks legally, current AP decreases by 1 and the visible AP summary/event feed reflects the spend.
- [ ] Given current AP is 0, Move and Basic Attack are rejected with clear diagnostics/feedback and no partial movement, damage, retaliation, or event mutation.
- [ ] Given the player chooses Defend, the stack enters visible Defending state, remaining AP is consumed or activation is ended, the event feed explains Defend, and a tiny prototype damage-reduction effect applies while Defending.
- [ ] Given the stack's next activation/reset point occurs, stale Defending state clears according to the documented prototype reset rule.
- [ ] Existing movement range, attack range, definition-derived damage, retaliation, command availability, and tactical presentation smoke behavior are not intentionally regressed.

## Verification requirements

- Unit/EditMode tests: Required for AP initialization, AP spend, insufficient-AP rejection/no mutation, Defend state application/reset, tiny prototype Defend damage reduction, and regression coverage around movement/attack/retaliation/unit-definition behavior.
- PlayMode tests/evidence: Required focused smoke showing visible AP values, AP spend after action, Defend state, and insufficient-AP denial feedback.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-TAC-AP-001/` in the Unity repo if implemented.
- CI evidence: Unity Foundation CI exact-head before merge.
- TDD evidence required? Yes for AP/Defend behavior.

## Ambiguity Check

Status: PASS.

Human-approved answers recorded 2026-06-17:

1. `STORY-TAC-AP-001` is approved with a tiny prototype damage-reduction effect for Defend, not visible-state-only Defend.
2. Narrow source-authority exception: `design/gdd/tactical-combat/ap-actions-and-reactions.md` and `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` remain draft/pending planning sources, but their cited AP/Defend sections are authorized only for this READY story's minimal AP, visible Defend state, and tiny prototype Defend damage-reduction effect. Broader initiative, Wait, armor, shield, cover, damage-type, terrain, status, ZoC, Overwatch, and CombatAI rules remain out of scope.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-AP-001-minimal-tactical-ap-defend-state`.
- PR title: `STORY-TAC-AP-001 Minimal tactical AP and Defend state`.
- Required linked story ID: `STORY-TAC-AP-001`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Application/Domain/Tests/Evidence directories.
- Required evidence summary: tests run, PlayMode/PNG evidence path, CI URL placeholder until PR CI runs, and omissions/deferred work.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied or marked non-blocking.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval recorded.

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

READY / approved for implementation. Human approval recorded 2026-06-17 with tiny prototype Defend damage reduction approved as the narrow effect exception; implement only the bounded AP/Defend slice above.
