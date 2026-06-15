---
title: STORY-TAC-RET-001 Minimal Melee Retaliation
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
    production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed,
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/army-deployment-and-stacks,
    design/gdd/tactical-combat/ap-actions-and-reactions,
    design/gdd/tactical-combat/targeting-damage-and-defense,
    design/research/homm-like-tactical-battle-ui-reference,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-TAC-RET-001 Minimal Melee Retaliation

## Status

DONE / merged. Human direction: defenders must get to answer; current prototype felt attacker-only. Unity PR #49 merged 2026-06-15 as squash commit `cfc24e04c53da0a6917b0117452c72a230ef9a84`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27552604744

## Story type

Tactical Rules / Defender Agency / Combat Event Feed.

## Parent epic

- [EPIC-VSLICE-MVP-006 Tactical Battle Readability and Defender Agency](../epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md)

## User/player/system value

As a player, I want adjacent defenders to retaliate after being attacked, so tactical combat feels two-sided and I can understand casualty exchange rather than seeing only attacker-initiated damage.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/tactical-combat.md` active tactical-combat first-read authority.
  - `design/gdd/tactical-combat/army-deployment-and-stacks.md` for stack/count presentation.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§119-146 for base Retaliation direction, especially immediate answer, once-per-round/limited response, and event-log visibility.
  - `design/gdd/tactical-combat/targeting-damage-and-defense.md` for current placeholder damage/defense constraints.
- UX/reference source:
  - `design/research/homm-like-tactical-battle-ui-reference.md` for HoMM-like attack + retaliation result readability.
  - `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` tactical ordering: event feed/labels first, retaliation next.
- ADR / architecture / control:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Parent/prior story:
  - `production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md`.
  - `production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed.md` DONE / merged.

## In scope

Concrete implementation tasks authorized by this story:

- Add minimal melee retaliation for the current tactical board/session:
  - When a legal adjacent standard attack hits a living, melee-capable target, that target immediately retaliates against the attacker if it still has retaliation available.
  - Use current placeholder damage/count rules unless the code already exposes a clearer single constant; do not design a new formula.
  - If the original attack defeats the target, no retaliation occurs.
  - If retaliation defeats or damages the attacker, battle completion and next activation still resolve deterministically.
- Add or expose enough result data for presentation and tests:
  - retaliation occurred / did not occur;
  - retaliator stack id;
  - retaliation target stack id;
  - retaliation damage applied;
  - attacker remaining count or defeated state after retaliation;
  - whether retaliation was unavailable/already spent when relevant.
- Add readable event-feed text using the existing `STORY-TAC-READ-002` style, e.g.:
  - `unit_placeholder_infantry attacks unit_placeholder_guard for 3 damage. unit_placeholder_guard loses 3; 3 remain. unit_placeholder_guard retaliates for 3 damage. unit_placeholder_infantry loses 3; 7 remain.`
  - If no retaliation because defeated: explicitly avoid claiming a defender answer.
- Add focused EditMode/domain tests for retaliation rules and non-retaliation cases.
- Add focused PlayMode/smoke evidence that a guarded-site battle visibly shows attack + retaliation in the combat event feed.

## Out of scope

Not authorized by this story:

- No AP economy.
- No Defend armor/bonus implementation.
- No Zone of Control, opportunity attacks on movement, or Overwatch.
- No ranged retaliation rules beyond the existing placeholder melee adjacency rule.
- No multiple retaliations per stack per retaliation cycle.
- No full round/initiative system beyond the minimum state needed to keep retaliation deterministic in the current two-side activation model.
- No CombatAI / automatic enemy turn logic.
- No new tactical units, final unit names, final roster data, balance pass, damage types, armor, shields, cover, LOS, range falloff, morale, or terrain.
- No strategic map, base, recruitment, objective, save/load, networking, or final art/VFX/audio work.

## Allowed stubs, mocks, placeholders, or temporary data

- Placeholder unit keys remain allowed.
- Current fixed damage constants may remain.
- Minimal retaliation availability state may be implemented directly on placed tactical stacks or board/session state if that is the smallest safe path.
- Because there is no full tactical round/initiative system yet, a simple documented refresh rule is allowed, such as refreshing retaliation availability when the current activation cycle returns to the attacker side, as long as tests lock it down and event text does not overclaim final design.

## Dependencies

- Required prior stories:
  - `STORY-TAC-READ-002` DONE / merged.
  - Current tactical movement/attack/battle-result stories are already DONE in prior epics.
- Required data/assets:
  - Existing tactical board, placed stack, and event-feed presentation surfaces.
- Required architecture decisions:
  - Existing Unity technical scheme/control manifest; no new ADR required.
- Required Unity/package setup:
  - Existing Unity project and CI.

## Acceptance criteria

- [ ] Given a living adjacent defender is attacked and survives, it immediately retaliates once against the attacker in the same command resolution.
- [ ] Given the defender is defeated by the initial attack, no retaliation damage is applied.
- [ ] Given a defender has already spent retaliation availability in the current minimal cycle, it does not retaliate again until the documented refresh point.
- [ ] Given retaliation damages the attacker, stack counts and defeated flags are updated correctly and battle completion remains deterministic.
- [ ] Given retaliation occurs, the event feed names attacker, defender/retaliator, primary damage, retaliation damage, and resulting counts/defeat states in concise player-facing language.
- [ ] Given retaliation does not occur due to defeat or spent availability, feedback remains truthful and does not imply a hidden defender attack.
- [ ] Existing legal move, legal attack, pass/wait/defend, Champion command, battle handoff, objective, and Champion encounter behavior is not intentionally regressed.
- [ ] PlayMode evidence captures a visible attack + retaliation event in tactical mode.

## Verification requirements

- Unit tests: N/A unless pure helper formatters are introduced; if introduced, test them.
- Unity edit-mode tests: Required for tactical domain/session retaliation rules, including surviving defender retaliates, defeated defender does not, and once-per-cycle availability.
- Unity play-mode tests: Required focused PlayMode/smoke for visible attack + retaliation feed.
- Integration/data validation tests: Existing placeholder validator must remain green.
- Manual Unity scene/prefab checks: Supplemental only.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-TAC-RET-001/` in the Unity repo.
- Performance budget or N/A: N/A; no expensive systems should be added.
- CI evidence: Unity Foundation CI exact-head before merge.
- Playtest evidence, if applicable: Optional after implementation; not required before PR.
- TDD evidence required? Yes for tactical rules.
- Automation deferred? No broad exception approved.

## Ambiguity Check

Status: PASS.

Open questions:

- None blocking. Full initiative/AP/round semantics are deferred; the story authorizes a minimal documented retaliation-availability cycle for the current activation model.

Assumptions:

- Current placeholder attacks are melee/adjacent attacks because `AttackRange` is currently 1.
- Retaliation uses existing placeholder standard attack damage unless the implementation discovers a current domain constant better represents standard stack damage.
- Final unit display names are not available, so placeholder unit keys remain acceptable.

Out of scope:

- AP, Defend bonus, ZoC, Overwatch, CombatAI, unit roster/stat expansion, strategic-map redesign, final art/content.

Allowed stubs/mocks:

- Minimal retaliation availability field/state.
- Placeholder unit labels.
- Fixed damage constants.

Human-approved exceptions:

- None.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-RET-001-minimal-melee-retaliation`.
- PR title: `STORY-TAC-RET-001 Minimal melee retaliation`.
- Required linked story ID: `STORY-TAC-RET-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/tactical-combat.md`.
  - `design/gdd/tactical-combat/army-deployment-and-stacks.md`.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§119-146.
  - `design/gdd/tactical-combat/targeting-damage-and-defense.md`.
  - `design/research/homm-like-tactical-battle-ui-reference.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Domain/Application/Presentation/Tests/Evidence directories.
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

DONE / merged. This story established minimal defender retaliation. Next authorized child story: `STORY-TAC-AFFORD-001 Movement and Attack Affordance Pass`.
