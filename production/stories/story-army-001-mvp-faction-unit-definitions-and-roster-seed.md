---
title: STORY-ARMY-001 MVP Faction Unit Definitions and Roster Seed
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-18
updated: 2026-06-18
source_lore: [greenland, qxz-meridian, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity,
    production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan,
    design/gdd/faction-unit-rosters,
    design/gdd/tactical-combat,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-ARMY-001 MVP Faction Unit Definitions and Roster Seed

## Status

READY-candidate / approval pending. This story is drafted from human EPIC-008 direction on 2026-06-18 but is not yet authorized for Unity implementation.

Do not implement until human approval promotes this story to `status: ready` and `approval: approved`.

## Story type

Data + Tactical Setup + Presentation Foundation.

## Parent epic

- [EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity](../epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md)

## User/player/system value

As a player, I want early faction armies to contain visibly different unit types, so that Home Rule Coalition and QXZ Meridian feel like different political/military philosophies rather than cloned placeholder stacks.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/faction-unit-rosters.md` §§Shared Unit Design Rules, Roster Scale Proposal, Home Rule Coalition, QXZ Meridian.
  - `design/gdd/tactical-combat.md` §§3, 4, 5, 6.1, 6.3, 6.4, 6.5, 6.7 for stack-first entities, simple AP/action assumptions, retaliation hooks, range/delivery, and visible statuses.
  - `design/gdd/strategic-map.md` §§2-8 and §§10-13 for two-faction hotseat, recruitment/reinforcement future use, and tactical handoff.
- World / lore bridge:
  - World vault `design-bridges/greenland-faction-unit-rosters.md` for the soft-canon Home Rule Coalition / QXZ direction and the naming guardrail against using Kalaallit as a faction brand.
- ADR / architecture / control-manifest:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation tasks authorized if promoted to READY:

- Add or formalize an MVP unit definition schema for tactical/army units, with stable IDs and validation.
- Add data for this 3-line-per-faction roster seed:
  - Home Rule Coalition:
    - `settlement_watch` / Settlement Watch: defensive infantry / baseline melee.
    - `sled_logistics_team` / Sled Logistics Team: support/mobility placeholder role.
    - `hunter_scouts` / Hunter-Scouts: recon/skirmisher.
  - QXZ Meridian:
    - `meridian_security` / Meridian Security: disciplined infantry / baseline attacker.
    - `strato_sensor_swarm` / Strato Sensor Swarm: ranged/recon drone and future Sensor Lock owner.
    - `climate_bulwark` / Climate Bulwark: heavy defender.
  - Neutral/shared guarded-site defenders:
    - `survey_drones` and/or `site_guards`, whichever best matches existing code shape.
- Include only fields needed to support current and near-next tactical roles, such as:
  - stable unit ID;
  - display name/key;
  - faction or allegiance bucket;
  - tactical role tag;
  - default stack count or setup count;
  - movement range;
  - attack range;
  - attack damage or current equivalent strength/damage field;
  - can-retaliate flag;
  - can-use-sensor-lock / support-role future flag only if cheap and explicit;
  - short UI role description.
- Wire current tactical setup / BattleSetup generation to read unit definitions instead of treating all stacks as identical placeholders where practical.
- Ensure tactical labels/event feed display the unit names/counts from the definitions.
- Add validation and tests for unit definitions and invalid IDs.
- Add Unity evidence showing distinct unit definitions in tactical mode.

## Out of scope

Not authorized by this story:

- No recruitment UI or strategic recruitment action. That belongs to ARMY-003.
- No Sensor Lock / Marked behavior yet, except future-safe fields if cheap and inert. Tactical behavior belongs to ARMY-002.
- No full town/dwelling tree.
- No upgraded unit variants.
- No full faction roster beyond the listed 3+3 and neutral guard seed.
- No balancing pass beyond safe placeholder values.
- No new tactical AP economy, cover, morale, LOS, damage taxonomy, or Champion operation expansion.
- No final art/icons/VFX/audio/animation.
- No hard-canon rename of Home Rule Coalition.

## Allowed stubs, mocks, placeholders, or temporary data

- Placeholder stats are allowed if they create readable distinctions and are documented.
- Unit display names are approved as game-facing MVP names but may be revised later.
- Home Rule Coalition is soft-canon/provisional; do not imply it represents all Greenlandic people.
- `Kalaallit` must not be used as a faction brand.
- If existing code cannot support all desired fields cleanly, add the minimal field set needed for this story and document deferred fields.

## Dependencies

- Required prior stories:
  - EPIC-006 tactical readability and EPIC-007 strategic readability are DONE / closed.
- Required data/assets:
  - Existing tactical board/stack setup and presentation surfaces.
- Required architecture decisions:
  - Existing Unity technical scheme and control manifest.
- Required Unity/package setup:
  - Existing Unity project and Unity Foundation CI.

## Acceptance criteria

- [ ] A unit-definition source exists with stable IDs for the approved roster seed.
- [ ] Definition validation catches duplicate IDs, missing display names, invalid faction/allegiance values, and impossible numeric stats.
- [ ] Tactical setup can spawn at least three distinct unit definitions in the same battle.
- [ ] Home Rule and QXZ units appear with distinct display names/counts in tactical labels and event-feed text where relevant.
- [ ] At least one unit has melee/baseline profile, one has ranged/recon profile, and one has heavy/defender profile represented in data.
- [ ] Existing tactical movement, attack, retaliation, AP, CombatAI, strategic handoff, and map presentation behavior is not intentionally changed beyond consuming/displaying definitions.
- [ ] Invalid or missing unit IDs fail safely with a testable error/default path, not silent placeholder corruption.
- [ ] Evidence documents provisional stats and deferred behavior fields.

## Verification requirements

- Unit tests: Required for unit-definition validation and lookup behavior.
- Unity edit-mode tests: Required for data registry/definition loading and tactical setup consuming unit definitions where practical.
- Unity play-mode tests: Required if current PlayMode smoke can verify labels/spawn composition.
- Integration/data validation tests: Existing placeholder/data validators must remain green or be replaced by stricter validators.
- Manual Unity scene/prefab checks: Supplemental only.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-ARMY-001/` in the Unity repo showing distinct unit names/counts in tactical mode.
- Performance budget or N/A: N/A.
- CI evidence: Unity Foundation CI exact-head before merge.
- TDD evidence required? Yes for validation/lookup and setup logic.
- Automation deferred? No broad exception approved; document any UI-only manual evidence.

## Ambiguity Check

Status: FAIL until human approval promotes this story to READY / approved.

Open questions before READY:

1. Are the listed unit IDs/names acceptable as the first implementation seed?
2. Should `Sled Logistics Team` be represented tactically now as a support/mobility placeholder, or should it start as a simple low-damage support stack until ARMY-002?
3. Should neutral defenders be `Survey Drones`, `Site Guards`, or both in ARMY-001?

Assumptions proposed for approval:

- Use `Home Rule Coalition` as the provisional game-facing soft-canon faction name.
- Use `Sled Logistics Team` as the third Home Rule MVP line.
- Give QXZ `Strato Sensor Swarm` the future Sensor Lock / Marked lane, but do not implement the status effect until ARMY-002.
- Include both `Survey Drones` and `Site Guards` only if technically cheap; otherwise choose the one closest to current guarded-site setup.

Human-approved exceptions:

- None yet.

If status is FAIL, this story is not READY.

## Branch / PR requirements

- Branch name after approval: `story/STORY-ARMY-001-mvp-faction-unit-definitions-roster-seed`
- PR title after approval: `STORY-ARMY-001 MVP faction unit definitions and roster seed`
- Required linked story ID: `STORY-ARMY-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/faction-unit-rosters.md`.
  - `design/gdd/tactical-combat.md`.
  - `design/gdd/strategic-map.md`.
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

READY-candidate / approval pending. Good first packet for EPIC-008, but not approved for Unity implementation yet.
