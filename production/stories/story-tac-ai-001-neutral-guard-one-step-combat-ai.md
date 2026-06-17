---
title: STORY-TAC-AI-001 Neutral Guard One-Step CombatAI
type: story
status: ready
phase: production
owner: shared
created: 2026-06-17
updated: 2026-06-17
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency,
    production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger,
    production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed,
    production/stories/story-tac-ret-001-minimal-melee-retaliation,
    production/stories/story-tac-afford-001-movement-and-attack-affordance-pass,
    production/stories/story-tac-unit-001-minimal-unit-definition-stats,
    production/stories/story-tac-ap-001-minimal-tactical-ap-and-defend-state,
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/ap-actions-and-reactions,
    design/gdd/tactical-combat/implementation-contracts,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-TAC-AI-001 Neutral Guard One-Step CombatAI

## Status

READY / approved for implementation. Human approval recorded 2026-06-17: `STORY-TAC-AI-001` is approved as the next EPIC-006 implementation packet.

Approved answer: deterministic one-step neutral guard AI may Attack if already in range, otherwise Move one legal step toward the nearest living attacker, otherwise Defend/Pass.

## Story type

Tactical AI / Domain Rules / Presentation Readability.

## Parent epic

- [EPIC-VSLICE-MVP-006 Tactical Battle Readability and Defender Agency](../epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md)

## User/player/system value

As a player, I want neutral guarded-site defenders to take a small readable tactical turn instead of sitting inert, so guarded battles start to feel contested while the prototype remains deterministic and reviewable.

## Source requirements

Exact source references:

- Parent epic:
  - `production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md` child story target: `STORY-TAC-AI-001 Neutral Guard One-Step CombatAI`.
- Prior story/controller source:
  - `production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger.md` requires guarded-site defender controller data as `CombatAI`, but explicitly did not implement AI behavior there.
- Prior implementation prerequisites:
  - `production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed.md` DONE / merged.
  - `production/stories/story-tac-ret-001-minimal-melee-retaliation.md` DONE / merged.
  - `production/stories/story-tac-afford-001-movement-and-attack-affordance-pass.md` DONE / merged.
  - `production/stories/story-tac-unit-001-minimal-unit-definition-stats.md` DONE / merged.
  - `production/stories/story-tac-ap-001-minimal-tactical-ap-and-defend-state.md` DONE / merged.
- GDD path + section/rule:
  - `design/gdd/tactical-combat.md` active tactical-combat first-read authority.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` for current Move / Basic Attack / Defend AP behavior already implemented by `STORY-TAC-AP-001`.
  - `design/gdd/tactical-combat/implementation-contracts.md` for deterministic, testable tactical systems and event/log visibility.
- ADR / architecture / control:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation tasks proposed by this story:

- Add the smallest deterministic CombatAI action path for neutral guarded-site defender stacks using existing tactical board/session rules.
- Apply it only to tactical sides/stacks whose controller is already `CombatAI` / neutral guard data from guarded-site battle setup.
- Add one explicit AI-step command or orchestration path that advances the current CombatAI-controlled activation by at most one chosen action.
- Deterministic one-step priority:
  1. If the active CombatAI stack has enough AP and a living enemy target is legally attackable with existing Basic Attack rules, perform one Basic Attack against the nearest/first deterministic legal target.
  2. Else, if the active CombatAI stack has enough AP and can legally move closer to the nearest living enemy using existing movement rules, perform one legal Move that reduces distance by the clearest deterministic tie-breaker.
  3. Else, if Defend is available, Defend.
  4. Else, Pass/end activation with clear feedback.
- Reuse existing AP, movement, attack, retaliation, Defend, unit-definition, battle-end, and event-feed behavior. Do not create alternate AI-only combat rules.
- Surface the AI step through existing tactical feedback: event feed/diagnostic text must make it clear which guard acted and whether it attacked, moved, defended, or passed.
- Preserve human-player command controls for HumanLocal sides.
- Add focused tests proving deterministic attack choice, move-toward choice, fallback Defend/Pass, AP spend, retaliation interaction, battle-end behavior, and no mutation for invalid/no-action states.
- Add PlayMode/evidence for a guarded-site battle where a neutral guard takes at least one visible AI action.

## Out of scope

Not authorized by this story:

- No strategic-map AI, faction AI, opponent planning, recruitment/base/economy AI, route selection, or turn planning.
- No initiative system, Wait action, multi-round tactical AI planner, behavior tree, utility AI, personality model, difficulty scaling, or stochastic/random AI.
- No new attacks, abilities, status effects, overwatch, Zone of Control, opportunity attacks, cover, LOS, terrain, damage types, armor/shield redesign, morale/rout, or final defense formula.
- No auto-resolve, battle simulation outside the existing tactical board/session, or hidden damage/movement shortcuts.
- No final animation/VFX/audio/UI skin, portrait, lore copy, or localization pass.
- No broad controller architecture rewrite beyond the narrow seam needed for one deterministic CombatAI step.

## Allowed stubs, mocks, placeholders, or temporary data

- Existing neutral guard placeholder stacks/controllers remain allowed.
- A small deterministic AI policy/service/class is allowed if it is bounded to this one-step prototype behavior.
- Tie-breakers may be simple and deterministic, e.g. side/stack order then coordinate order, if covered by tests.
- Placeholder feedback strings are allowed if clear and covered by tests/evidence.

## Dependencies

- Required prior stories:
  - `STORY-STRAT-004` DONE / merged for guarded-site `CombatAI` controller data.
  - `STORY-TAC-READ-002` DONE / merged.
  - `STORY-TAC-RET-001` DONE / merged.
  - `STORY-TAC-AFFORD-001` DONE / merged.
  - `STORY-TAC-UNIT-001` DONE / merged.
  - `STORY-TAC-AP-001` DONE / merged.
- Required data/assets:
  - Existing guarded-site defender setup and tactical stack presentation.
- Required architecture decisions:
  - Existing Unity technical scheme/control manifest; no new ADR required if AI remains a deterministic prototype service.
- Required Unity/package setup:
  - Existing Unity project and CI.

## Acceptance criteria

- [ ] Given a guarded-site battle is launched and the current activation belongs to a CombatAI-controlled neutral guard stack, when the AI step is invoked, then exactly one legal action is selected and applied through existing tactical command rules.
- [ ] Given a living attacker is legally attackable, the AI chooses Basic Attack before movement/Defend, spends AP according to existing AP rules, applies definition-derived damage, triggers existing retaliation rules if applicable, and emits readable feedback.
- [ ] Given no target is attackable but a legal move can reduce distance to the nearest living enemy, the AI moves one legal step/action toward that enemy, spends AP according to existing AP rules, and emits readable feedback.
- [ ] Given the AI cannot attack or improve position, the AI uses Defend if available and the visible Defending state/effect follows the existing `STORY-TAC-AP-001` rules.
- [ ] Given no legal AI action exists, the AI passes/ends activation with clear feedback and no partial mutation.
- [ ] Given multiple legal targets or moves exist, the same input state always produces the same AI action by documented tie-breakers.
- [ ] Given the AI action defeats the last opposing stack, the existing battle-end/result-return behavior is used and no special AI-only battle outcome path is introduced.
- [ ] Given the current activation belongs to a HumanLocal side, the AI step is rejected or ignored with no mutation.
- [ ] Existing HumanLocal movement, attack, retaliation, AP/Defend, command, guarded-site capture, Champion encounter, and objective smoke behavior are not intentionally regressed.

## Verification requirements

- Unit tests: Required for deterministic AI action selection/tie-breakers if implemented as isolated domain/service code.
- Unity edit-mode tests: Required for attack choice, move choice, fallback Defend/Pass, AP spend, retaliation interaction, battle-end behavior, HumanLocal rejection/no mutation, and deterministic tie-breakers.
- Unity play-mode tests: Required guarded-site smoke/evidence showing a neutral guard taking at least one visible AI action in the tactical board flow.
- Integration/data validation tests: Existing placeholder validator must remain green; add validation only if new authored data files are introduced.
- Manual Unity scene/prefab checks: Supplemental only.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-TAC-AI-001/` in the Unity repo.
- Performance budget or N/A: N/A; one-step AI must be deterministic and cheap.
- CI evidence: Unity Foundation CI exact-head before merge.
- Playtest evidence, if applicable: Optional after implementation; not required before PR.
- TDD evidence required? Yes for selection and no-mutation behavior.
- Automation deferred? No broad exception approved.

## Ambiguity Check

Status: PASS.

Open questions:

- None.

Human-approved answers:

1. Approved 2026-06-17: deterministic one-step neutral guard AI may Attack if already in range, otherwise Move one legal step toward the nearest living attacker, otherwise Defend/Pass.

Approved assumptions:

- The one-step priority is Attack, else Move toward nearest enemy, else Defend, else Pass.
- Tie-breakers are implementation-owned if deterministic and covered by tests.
- The AI may be invoked by an explicit command/orchestration seam rather than a fully automatic tactical loop if that keeps the slice smaller and clearer.

Out of scope:

- Strategic AI, advanced tactical AI, behavior trees/utility AI, initiative/Wait, ZoC/Overwatch, new combat mechanics, final UI/audio/VFX/content.

Allowed stubs/mocks:

- Prototype one-step deterministic policy.
- Placeholder neutral guard labels and feedback strings.

Human-approved exceptions:

- Narrow source-authority exception: `design/gdd/tactical-combat/ap-actions-and-reactions.md` and `design/gdd/tactical-combat/implementation-contracts.md` are draft/pending overall, but their cited Move / Basic Attack / Defend AP behavior and deterministic/testable tactical-system passages are approved as implementation authority only for this story's neutral guard one-step CombatAI. Broader initiative, Wait, advanced tactical AI, behavior trees/utility AI, strategic AI, ZoC, Overwatch, new combat mechanics, statuses, and final combat formulas remain out of scope.

If status is FAIL, this story is not READY.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-AI-001-neutral-guard-one-step-combat-ai`.
- PR title: `STORY-TAC-AI-001 Neutral guard one-step CombatAI`.
- Required linked story ID: `STORY-TAC-AI-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/tactical-combat.md`.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md`.
  - `design/gdd/tactical-combat/implementation-contracts.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Application/Domain/Presentation/Tests/Evidence directories.
- Required evidence summary: tests run, PlayMode/PNG evidence path, CI URL.
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
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given and recorded.

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

READY for implementation.
