---
title: STORY-TAC-READ-002 Tactical Stack Labels and Combat Event Feed
type: story
status: done
phase: production
owner: shared
created: 2026-06-15
updated: 2026-06-15
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency,
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/army-deployment-and-stacks,
    design/gdd/tactical-combat/ap-actions-and-reactions,
    design/research/homm-like-tactical-battle-ui-reference,
    production/planning/prototype-readability-and-map-next-steps-2026-06-15,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-TAC-READ-002 Tactical Stack Labels and Combat Event Feed

## Status

DONE / merged. Human approval recorded 2026-06-15. Unity PR #48 merged 2026-06-15 as squash commit `2c22667532ccc64e0fe746030fd33707c2edd682`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27543258160

## Story type

Tactical UI / Playability Repair / Presentation Snapshot.

## Parent epic

- [EPIC-VSLICE-MVP-006 Tactical Battle Readability and Defender Agency](../epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md)

## User/player/system value

As a player, I want tactical stacks and attack outcomes to be readable at a glance, so that I can understand who acts, how many units remain, what happened after an attack, and whether later retaliation/AI/AP work is improving the actual battle rather than adding more opaque rules.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/tactical-combat.md` active tactical-combat first-read authority.
  - `design/gdd/tactical-combat/army-deployment-and-stacks.md` stack/army presentation context.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§78-91 for base actions that need readable move/attack/pass/wait/defend feedback.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§121-138 for forthcoming retaliation language that this event feed must be able to support later, without implementing retaliation in this story.
- Reference / UX source:
  - `design/research/homm-like-tactical-battle-ui-reference.md` §§Minimum UI contract and Design stance: stack labels, reachability, clean outcome sentence, detail disclosure.
  - `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` §§1 Tactical combat event log and stack labels.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` for layered EditMode/PlayMode/evidence requirements.
  - `docs/architecture/ci-build-automation.md` for CI expectations.
- Parent epic:
  - `production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md`.

## In scope

Concrete implementation tasks authorized by this story:

- Add or improve visible tactical stack labels for every placed tactical stack:
  - readable unit display label or placeholder unit key;
  - current stack count;
  - owning side/faction/controller cue using existing prototype-safe text/color/marker surfaces;
  - clear current acting stack highlight.
- Add or improve a compact tactical combat event feed/result log for current tactical actions:
  - move success;
  - invalid move denial;
  - attack success;
  - invalid attack denial;
  - target damage and resulting count/defeat;
  - pass/wait/defend action feedback using current mechanics only;
  - battle result/next active stack feedback where available.
- Use concise HoMM-like natural language for attack outcomes, adapted to current placeholder data:
  - example shape: `Attacker Label attacks Defender Label for 3 damage. Defender Label loses 3; 5 remain.`
  - if defeated: `Defender Label is defeated.`
- Preserve or improve existing legal move and legal attack highlighting; do not regress affordances already added by `STORY-QA-006`.
- Add enough presentation-snapshot/domain event data to support the feed without changing combat rules.
- Add focused tests and PlayMode/evidence for labels and event-feed readability.

## Out of scope

Not authorized by this story:

- No retaliation/counterattack implementation. This story may make the event feed ready for future retaliation lines but must not add defender auto-attacks.
- No AP economy implementation.
- No Defend armor/bonus implementation beyond explaining the existing current behavior.
- No Zone of Control, Overwatch, cover, LOS, range falloff, armor/shield/damage-type rules.
- No neutral guard CombatAI implementation.
- No new tactical units, final unit names, final faction roster data, balance, or damage formulas.
- No strategic map redesign, base/recruitment changes, objective changes, encounter changes, or battle-result rules changes.
- No final art/icons/VFX/audio/animation/portraits.

## Allowed stubs, mocks, placeholders, or temporary data

- Placeholder unit labels/display keys are allowed if final unit names are not available.
- Prototype text/color/markers are allowed; final UI art is not required.
- Existing fixed tactical damage/count behavior may remain unchanged and should be described accurately.
- If current code has no per-unit pluralization/localization support, simple readable labels are acceptable; do not build a full localization/pluralization system in this story.

## Dependencies

- Required prior stories:
  - `STORY-QA-006`, `STORY-QA-007`, `STORY-CMD-005`, and `STORY-STRAT-OBJECTIVE-001` are DONE / merged as prior repair/context stories.
- Required data/assets:
  - Existing tactical board/stack data and presentation surfaces in the Unity repo.
- Required architecture decisions:
  - Existing Unity technical scheme/control manifest; no new ADR required.
- Required Unity/package setup:
  - Existing Unity project and CI.

## Acceptance criteria

- [ ] Given tactical mode is active, every visible tactical stack displays a readable label/key, stack count, and side/faction cue.
- [ ] Given a stack is currently acting, the active stack is visually/textually distinct from non-active stacks.
- [ ] Given legal move destinations and legal attack targets exist, this story preserves or improves their current visibility and does not confuse attack targets with selecting/owning enemy stacks.
- [ ] Given a legal move succeeds, the event feed states which stack moved and enough destination/context to understand the result.
- [ ] Given an invalid move is attempted, the event feed or existing feedback states a concrete denial reason and board state does not mutate.
- [ ] Given a legal attack succeeds, the event feed states attacker, defender, damage/current count change, and remaining count or defeat.
- [ ] Given an invalid attack is attempted, feedback states a concrete denial reason and board state does not mutate.
- [ ] Given pass/wait/defend is used, feedback accurately describes the current implemented effect without claiming unimplemented AP/armor/retaliation behavior.
- [ ] Existing tactical movement, attack, command, battle handoff, objective, and Champion encounter behavior is not intentionally changed.
- [ ] PlayMode evidence captures tactical stack labels and at least one move, one attack, one invalid/denied action, and one defeated or post-attack remaining-count event.

## Verification requirements

- Unit tests: N/A unless extracted pure formatter/event-feed helpers are introduced; if introduced, test them.
- Unity edit-mode tests: Required for tactical presentation snapshot/event text helpers where practical, and for no-mutation denial behavior if affected.
- Unity play-mode tests: Required focused PlayMode/smoke evidence for labels and event-feed behavior.
- Integration/data validation tests: Existing placeholder/data validators must remain green.
- Manual Unity scene/prefab checks: Supplemental; not a replacement for PlayMode evidence if PlayMode can cover this.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-TAC-READ-002/` in the Unity repo.
- Performance budget or N/A: N/A; no expensive systems should be added.
- CI evidence: Unity Foundation CI exact-head before merge.
- Playtest evidence, if applicable: Optional after implementation; not required before PR.
- TDD evidence required? Yes for production logic/presentation helpers where practical; UI-only wiring may use targeted tests plus PlayMode evidence.
- Automation deferred? No broad exception approved. If a requested UI check cannot be automated, document why and provide PNG/manual evidence.

## Ambiguity Check

Status: PASS.

Open questions:

- None blocking. Exact visual styling is implementation-owned within prototype-safe text/color/marker constraints.

Assumptions:

- Current tactical board/presentation surfaces can show labels and feedback without final UI art.
- Existing fixed damage/count semantics remain unchanged.

Out of scope:

- Retaliation, AP, Defend bonus, unit-definition expansion, CombatAI, strategic map redesign, final art/content.

Allowed stubs/mocks:

- Placeholder unit display names/keys.
- Prototype text/color/markers.

Human-approved exceptions:

- None.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-READ-002-tactical-stack-labels-event-feed`
- PR title: `STORY-TAC-READ-002 Tactical stack labels and combat event feed`
- Required linked story ID: `STORY-TAC-READ-002`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/tactical-combat.md`.
  - `design/gdd/tactical-combat/army-deployment-and-stacks.md`.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§78-91 and §§121-138.
  - `design/research/homm-like-tactical-battle-ui-reference.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Application/Presentation/Domain/Tests/Evidence directories.
- Required evidence summary: tests run, PlayMode/PNG evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/reference sources are linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied or marked non-blocking.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval recorded 2026-06-15.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes or human-approved exceptions are documented.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged. This story established the tactical readability baseline for stack labels and combat event-feed wording. Next authorized child story: `STORY-TAC-RET-001 Minimal Melee Retaliation`.
