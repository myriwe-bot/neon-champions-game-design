---
title: STORY-TAC-UNIT-001 Minimal Unit Definition Stats
type: story
status: ready-candidate
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
    production/stories/story-tac-afford-001-movement-and-attack-affordance-pass,
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/army-deployment-and-stacks,
    design/gdd/tactical-combat/mvp-content-and-faction-rosters,
    design/gdd/tactical-combat/implementation-contracts,
    production/planning/prototype-readability-and-map-next-steps-2026-06-15,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-TAC-UNIT-001 Minimal Unit Definition Stats

## Status

READY-candidate / approval pending. This is the recommended next EPIC-006 packet after `STORY-TAC-AFFORD-001` merged. It is drafted for review; it does not authorize Unity implementation until human approval promotes it to READY.

## Story type

Tactical Data / Domain Rules / Presentation Readability.

## Parent epic

- [EPIC-VSLICE-MVP-006 Tactical Battle Readability and Defender Agency](../epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md)

## User/player/system value

As a player, I want different tactical stacks to have their own visible movement, attack, damage, and retaliation capabilities, so the battlefield stops feeling like identical placeholder blocks and the new affordance UI communicates meaningful unit differences.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/tactical-combat.md` active tactical-combat first-read authority.
  - `design/gdd/tactical-combat/army-deployment-and-stacks.md` for stack/army presentation context.
  - `design/gdd/tactical-combat/mvp-content-and-faction-rosters.md` §§Unit roster contract and implementation readiness gates: roster implementation should prioritize data-driven unit definitions so roster coverage does not create one-off tactical code.
  - `design/gdd/tactical-combat/implementation-contracts.md` §§Tactical Implementation Contracts: tactical content should use implementation-safe data contracts and avoid hardcoded one-offs.
- Planning source:
  - `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` §§4 Minimal unit definition data.
- ADR / architecture / control:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Parent/prior stories:
  - `production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md`.
  - `production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed.md` DONE / merged.
  - `production/stories/story-tac-ret-001-minimal-melee-retaliation.md` DONE / merged.
  - `production/stories/story-tac-afford-001-movement-and-attack-affordance-pass.md` DONE / merged.

## In scope

Concrete implementation tasks proposed by this story:

- Add a minimal tactical unit definition data contract with stable unit ID and prototype-safe fields:
  - stable `UnitDefinitionId`;
  - player-facing display label / short label;
  - movement range;
  - attack range;
  - attack damage;
  - can-retaliate flag;
  - melee-capable or melee-retaliation-capable flag if needed to keep rules explicit;
  - optional role tag / role label for prototype readability.
- Provide a tiny built-in placeholder definition catalog for currently used prototype unit IDs, including at least:
  - `unit_placeholder_infantry`;
  - `unit_placeholder_guard`;
  - existing Champion-vs-Champion placeholder IDs currently emitted by battle setup smoke paths.
- Update tactical board creation so `PlacedTacticalStack` derives movement range, attack range, attack damage, display label, and retaliation capability from the unit definition catalog.
- Update basic attack and retaliation to use the acting stack's definition-derived attack damage instead of one universal hardcoded damage value.
- Preserve current prototype behavior where intended by assigning default placeholder stats equivalent to current values unless the story/test explicitly establishes a small contrast.
- Add at least one intentionally different placeholder stat profile so tests/evidence prove unit stats are data-driven, not all copied from constants.
- Surface definition-derived display labels and stats through the existing tactical presentation snapshot / affordance UI.
- Validate missing or invalid unit definition references in tactical setup/factory paths with clear diagnostics and no partial accepted tactical board state.
- Add focused tests proving definition lookup, factory population, attack/retaliation damage, missing-definition rejection, and visible presentation of unit-derived stats.

## Out of scope

Not authorized by this candidate story:

- No full faction roster implementation.
- No final unit names, final lore copy, final art/icons, animations, VFX, audio, portraits, or localization pass.
- No balance pass beyond tiny prototype-safe stat differences needed to prove the data path.
- No armor, shields, damage types, morale, statuses, cover, LOS, terrain, range falloff, or ability system.
- No AP economy or Defend bonus.
- No Zone of Control, opportunity attacks, Overwatch, CombatAI, or initiative system.
- No recruitment/economy/base/strategic-map topology changes.
- No ScriptableObject/editor tooling unless already trivial and consistent with existing project patterns; code-side placeholder definitions are acceptable for this first data contract.

## Allowed stubs, mocks, placeholders, or temporary data

- Placeholder unit IDs and labels remain allowed.
- A code-defined placeholder catalog is allowed for this first implementation slice.
- Existing current stats may be preserved for most units to avoid accidental balance/design decisions.
- One or two deliberately different prototype stat values are allowed only to prove the data-driven path and must be documented in evidence/PR omissions.
- Final roster names and lore are explicitly deferred.

## Dependencies

- Required prior stories:
  - `STORY-TAC-READ-002` DONE / merged.
  - `STORY-TAC-RET-001` DONE / merged.
  - `STORY-TAC-AFFORD-001` DONE / merged.
- Required data/assets:
  - Existing tactical board, placed stack, battle setup, and presentation snapshot surfaces.
- Required architecture decisions:
  - Existing Unity technical scheme/control manifest; no new ADR required if the catalog is kept minimal and code-side.
- Required Unity/package setup:
  - Existing Unity project and CI.

## Acceptance criteria

- [ ] Given tactical board setup uses a known unit ID, the placed tactical stack receives movement range, attack range, attack damage, retaliation capability, and display label from the unit definition catalog.
- [ ] Given setup references an unknown/blank unit ID, tactical board creation fails with a clear diagnostic and does not return a partial accepted board.
- [ ] Given a unit definition has a non-default movement range, legal move destinations reflect that value and the presentation snapshot reports it.
- [ ] Given a unit definition has a non-default attack range, legal attack targets reflect that value and the presentation snapshot reports it.
- [ ] Given a unit definition has non-default attack damage, basic attack and retaliation apply the definition-derived damage and the combat event feed reports the resulting damage/counts.
- [ ] Given a unit cannot retaliate, melee retaliation is skipped with clear event-feed text when retaliation would otherwise be expected.
- [ ] Given current placeholder units are used in existing smoke paths, existing battle handoff, movement, attack, retaliation, Champion command, objective, and encounter behavior is not intentionally regressed.
- [ ] PlayMode evidence captures at least one visible definition-derived stat difference and one combat outcome using definition-derived damage.

## Verification requirements

- Unit tests: Required for pure unit definition lookup/catalog behavior if implemented as isolated domain/service code.
- Unity edit-mode tests: Required for tactical board factory population, missing-definition rejection/no partial board, legal move/attack range behavior, definition-derived damage, and retaliation capability.
- Unity play-mode tests: Required focused smoke/evidence showing visible unit-derived stats and damage/count output.
- Integration/data validation tests: Existing placeholder validator must remain green; add validation coverage only if new authored data files are introduced.
- Manual Unity scene/prefab checks: Supplemental only.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-TAC-UNIT-001/` in the Unity repo.
- Performance budget or N/A: N/A; catalog lookup must be deterministic and cheap.
- CI evidence: Unity Foundation CI exact-head before merge.
- Playtest evidence, if applicable: Optional after implementation; not required before PR.
- TDD evidence required? Yes for catalog/factory/damage behavior.
- Automation deferred? No broad exception approved.

## Ambiguity Check

Status: NEEDS APPROVAL.

Open questions for human approval:

1. Approve the first unit-data slice as code-side placeholder catalog only, with no ScriptableObject/editor tooling yet?
2. Approve one or two tiny prototype stat differences to prove the data path, while keeping final balance deferred?
3. Approve the candidate retaliation flag behavior: a non-retaliating unit simply skips melee retaliation and the feed explains the reason?

Assumptions if approved:

- Exact placeholder labels/stat values are implementation-owned within tiny prototype-safe bounds, but must be documented in evidence and tests.
- The implementation should preserve existing story smoke behavior unless a test explicitly proves a unit-data-driven change.

Out of scope:

- Full roster, balance, AP, Defend bonus, ZoC, Overwatch, CombatAI, abilities/statuses, strategic-map/base work, final art/content.

Allowed stubs/mocks:

- Code-defined placeholder unit catalog.
- Placeholder display labels.
- Prototype stat values.

Human-approved exceptions:

- None yet.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-UNIT-001-minimal-unit-definition-stats`.
- PR title: `STORY-TAC-UNIT-001 Minimal unit definition stats`.
- Required linked story ID: `STORY-TAC-UNIT-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/tactical-combat.md`.
  - `design/gdd/tactical-combat/army-deployment-and-stacks.md`.
  - `design/gdd/tactical-combat/mvp-content-and-faction-rosters.md`.
  - `design/gdd/tactical-combat/implementation-contracts.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Application/Domain/Tests/Evidence directories.
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
- [x] Dependencies are listed and satisfied or marked non-blocking.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [ ] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [ ] Human approval recorded.

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

READY-candidate / approval pending. Do not run Codex implementation until this story is promoted to READY / approved.
