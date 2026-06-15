---
title: STORY-TAC-AFFORD-001 Movement and Attack Affordance Pass
type: story
status: ready
phase: production
owner: shared
created: 2026-06-15
updated: 2026-06-15
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency,
    production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed,
    production/stories/story-tac-ret-001-minimal-melee-retaliation,
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

# STORY-TAC-AFFORD-001 Movement and Attack Affordance Pass

## Status

READY / approved. Human direction: the prototype still makes it unclear how far units can move or what they can attack. `STORY-TAC-READ-002` and `STORY-TAC-RET-001` are DONE / merged, so the next narrow EPIC-006 implementation packet is tactical movement/attack affordance clarity.

## Story type

Tactical UI / Interaction Affordance / Readability Repair.

## Parent epic

- [EPIC-VSLICE-MVP-006 Tactical Battle Readability and Defender Agency](../epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md)

## User/player/system value

As a player, I want legal move hexes, attack targets, and range limits to be obvious before I click, so I can plan tactical actions without guessing from failed commands.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/tactical-combat.md` active tactical-combat first-read authority.
  - `design/gdd/tactical-combat/army-deployment-and-stacks.md` for stack and marker presentation context.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§78-91 for base move/attack/pass/wait/defend action feedback.
- UX/reference source:
  - `design/research/homm-like-tactical-battle-ui-reference.md` §§Minimum UI contract and Design stance: reachability overlay, valid targets, blocked/occupied inspection, range/adjacency distinction.
  - `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` §§3 Movement and attack affordance pass.
- ADR / architecture / control:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Parent/prior stories:
  - `production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md`.
  - `production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed.md` DONE / merged.
  - `production/stories/story-tac-ret-001-minimal-melee-retaliation.md` DONE / merged.

## In scope

Concrete implementation tasks authorized by this story:

- Improve visible tactical affordance data for the active stack:
  - movement range value;
  - attack range value;
  - current coordinate;
  - legal move destination count/list;
  - legal attack target count/list;
  - retaliation availability if already exposed by the current stack marker/card.
- Improve tactical board/side-panel/readable overlay wording so the player can distinguish:
  - legal move hexes;
  - occupied/blocked hexes near the active stack;
  - legal attack targets;
  - enemies that exist but are not currently attackable.
- Improve pre-commit affordance labels and button/card text using existing prototype-safe UI surfaces.
- Improve denial feedback for the already-supported failure cases:
  - occupied destination;
  - destination outside movement range;
  - target outside attack range;
  - same-side target;
  - missing/defeated target.
- Preserve and regression-test existing legal move/attack highlighting and the combat event feed from `STORY-TAC-READ-002` / `STORY-TAC-RET-001`.
- Add focused EditMode and PlayMode evidence that shows legal moves, attack targets, range values, and denial explanations visibly enough at the current target resolution.

## Out of scope

Not authorized by this story:

- No AP economy.
- No Defend armor/bonus implementation.
- No Zone of Control, opportunity attacks, Overwatch, cover, LOS, range falloff, terrain bonuses, path preview, multi-hex pathfinding, or movement animation.
- No new tactical units, final unit names, final roster data, balance pass, damage types, armor, shields, morale, or terrain.
- No CombatAI.
- No strategic map, base, recruitment, objective, save/load, networking, or final art/VFX/audio work.
- No redesign of the tactical board geometry; use existing board/marker/canvas surfaces.

## Allowed stubs, mocks, placeholders, or temporary data

- Placeholder unit keys remain allowed.
- Current fixed movement range, attack range, and damage constants may remain.
- Prototype text/color/marker affordances are allowed; final icons/art are not required.
- Existing legal-destination/target calculations are the authority unless a test reveals a concrete bug.

## Dependencies

- Required prior stories:
  - `STORY-TAC-READ-002` DONE / merged.
  - `STORY-TAC-RET-001` DONE / merged.
- Required data/assets:
  - Existing tactical board, placed stack, and presentation snapshot surfaces.
- Required architecture decisions:
  - Existing Unity technical scheme/control manifest; no new ADR required.
- Required Unity/package setup:
  - Existing Unity project and CI.

## Acceptance criteria

- [ ] Given tactical mode is active, the visible UI/presentation snapshot states the active stack's movement range, attack range, and current coordinate.
- [ ] Given legal move destinations exist, they are visually/textually distinguishable from non-legal/occupied hexes.
- [ ] Given legal attack targets exist, they are visually/textually distinguishable from enemies that are not currently attackable.
- [ ] Given an occupied destination is attempted, feedback states the destination is occupied and board state does not mutate.
- [ ] Given an out-of-range move is attempted, feedback states it is outside movement range and board state does not mutate.
- [ ] Given an out-of-range attack is attempted, feedback states it is outside attack range and board state does not mutate.
- [ ] Given same-side or defeated/missing attack target cases are attempted, feedback stays concrete and truthful.
- [ ] Existing movement, attack, retaliation, pass/wait/defend, Champion command, battle handoff, objective, and Champion encounter behavior is not intentionally regressed.
- [ ] PlayMode evidence captures legal move affordances, legal attack affordances, and at least one denial explanation.

## Verification requirements

- Unit tests: N/A unless pure formatter/helper functions are introduced; if introduced, test them.
- Unity edit-mode tests: Required for tactical presentation snapshot/feedback fields and no-mutation denial behavior where practical.
- Unity play-mode tests: Required focused PlayMode/smoke for visible move/attack affordances and denial feedback.
- Integration/data validation tests: Existing placeholder validator must remain green.
- Manual Unity scene/prefab checks: Supplemental only.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-TAC-AFFORD-001/` in the Unity repo.
- Performance budget or N/A: N/A; no expensive systems should be added.
- CI evidence: Unity Foundation CI exact-head before merge.
- Playtest evidence, if applicable: Optional after implementation; not required before PR.
- TDD evidence required? Yes for presentation helpers/denial regressions where practical.
- Automation deferred? No broad exception approved.

## Ambiguity Check

Status: PASS.

Open questions:

- None blocking. Exact visual styling is implementation-owned within existing prototype-safe text/color/marker constraints.

Assumptions:

- Current target resolution remains 1280x720 for PlayMode readability evidence unless the existing tests establish a different target.
- The implementation can improve affordance labels/side panels/readable overlays without final art or a new input system.

Out of scope:

- AP, Defend bonus, ZoC, Overwatch, CombatAI, unit roster/stat expansion, strategic-map redesign, final art/content.

Allowed stubs/mocks:

- Placeholder unit labels.
- Fixed movement/attack constants.
- Prototype text/color/marker affordances.

Human-approved exceptions:

- None.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-AFFORD-001-movement-attack-affordance-pass`.
- PR title: `STORY-TAC-AFFORD-001 Movement and attack affordance pass`.
- Required linked story ID: `STORY-TAC-AFFORD-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/tactical-combat.md`.
  - `design/gdd/tactical-combat/army-deployment-and-stacks.md`.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§78-91.
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

READY / approved for Unity implementation. This story is the only current implementation authority from EPIC-006 after `STORY-TAC-RET-001`.
