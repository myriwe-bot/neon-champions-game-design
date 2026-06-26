---
title: STORY-BASE-002 Administration Income Chain and Recruitment Dwellings
type: story
status: ready
phase: production
owner: shared
created: 2026-06-26
updated: 2026-06-26
source_lore: [greenland, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction,
    production/stories/story-base-001-base-definition-and-facility-construction-core,
    design/gdd/strategic-map,
    design/research/homm-town-building-reference,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-BASE-002 Administration Income Chain and Recruitment Dwellings

## Status

READY / approved. Prepared after `STORY-BASE-001` merged via Unity PR #80 and post-merge Unity Foundation CI passed. This story is the next EPIC-009 implementation packet: make constructed base facilities produce the first tiny economy/recruitment effects while preserving the existing map, battle, and objective loop.

## Story type

Strategic Economy + Recruitment + UI + Validation.

## Parent epic

- [EPIC-VSLICE-MVP-009 Strategic Map Geography, Bases, and Facility Construction](../epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction.md)

## User/player/system value

As a player, I want base facilities to create visible recurring Credits income and unlock/refresh limited faction-specific recruitment offers, so that building choices begin to matter across turns instead of only recording constructed state.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §12 for the approved H3-inspired small base facility model: three-level administration income chain, one to two faction-specific recruitment/dwelling offers per faction, resource-costed construction, data-driven authored names, no capture/siege/editor UI.
  - `design/gdd/strategic-map.md` §13 for Champion army and recruitment boundaries.
  - `design/gdd/strategic-map.md` §14 for start-of-turn recurring income timing and turn summary visibility.
  - `design/gdd/strategic-map.md` §§15-16 for tactical boundary preservation and acceptance criteria.
- Research / planning:
  - `design/research/homm-town-building-reference.md` for the H3/Olden Era extraction: halls produce recurring income, dwellings unlock recruitable growth/stock, and full town trees are out of scope.
  - `production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction.md` for locked human direction.
- ADR / architecture / control-manifest:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation tasks authorized:

- Extend the existing `BaseFacilityDefinition` / runtime model from `STORY-BASE-001` with data-driven effect metadata sufficient for this story:
  - administration income effect amount in Credits;
  - administration chain level or tier where needed;
  - recruitment/dwelling offer unlock or refresh metadata;
  - stable effect IDs/localization keys if the current code shape needs them.
- Seed the current two-faction scenario with a tiny three-level administration chain shape:
  - level 1/basic income facility may be starting/default or prebuilt if that is the narrowest way to express baseline income;
  - level 2 and level 3 are buildable/upgradable via existing construction rules and prerequisites;
  - recurring income is Credits only for this story.
- Apply recurring Credits income for the active faction at deterministic start-of-faction-turn timing, before normal actions, using constructed base facilities owned by that active faction.
- Surface start-of-turn income feedback in the existing strategic HUD/diagnostic/status text.
- Add one to two faction-specific base recruitment/dwelling offers per faction, data-driven through base/facility state rather than hardcoded UI branches.
- Make recruitment/dwelling offer availability depend on constructed facility state and deterministic stock/refresh rules.
- Keep recruitment effects limited to the active Champion army / existing recruitment service path; do not add faction reserves, caravans, or garrisons.
- Add validation/tests for facility effect metadata, income chain prerequisites, recruitment offer unlock references, stock/refresh rules, and no partial mutation on invalid data/actions.
- Add PlayMode/smoke evidence showing income feedback and a facility-unlocked recruitment/dwelling offer.

## Out of scope

Not authorized by this story:

- No starting-base capture, siege, garrisons, ownership transfer, or defense management.
- No full Heroes-style town tree.
- No full seven-tier dwelling model.
- No upgraded-unit dwellings.
- No marketplace/resource trading.
- No Capitol/global-one-per-kingdom special rule.
- No strategic AI construction/recruitment planning.
- No map editor UI.
- No procedural map generation.
- No topology rewrite, fog, supply, logistics, or weather.
- No final map/base art, icons, VFX, audio, or animation.
- No new victory condition.

## Allowed stubs, mocks, placeholders, or temporary data

- Prototype facility IDs/localization keys are allowed if scenario-authored and validated.
- Prototype Credits income amounts and recruitment stock/growth values are allowed if documented and test-backed.
- Recruitment/dwelling UI may reuse existing recruitment/base panel text surfaces.
- Effect metadata may be simple strings/classes/enums as long as it remains serializable and data-driven.

## Dependencies

- Required prior stories:
  - `STORY-MAP-REAL-001` DONE / merged.
  - `STORY-BASE-001` DONE / merged via Unity PR #80.
- Required data/assets:
  - Current authored scenario/base/facility definitions in Unity.
- Required architecture decisions:
  - Existing Unity technical scheme, control manifest, testing strategy, and CI build automation.
- Required Unity/package setup:
  - Existing Unity project and Unity Foundation CI.

## Acceptance criteria

- [ ] Facility definitions can express administration income effects and recruitment/dwelling offer unlocks with stable, validated data.
- [ ] The scenario contains a three-level administration chain shape for the current two starting bases, with level/prerequisite data validated.
- [ ] Start-of-active-faction-turn applies recurring Credits income from that faction's constructed/starting income facilities only.
- [ ] Income is not applied on preview, failed end-turn, wrong faction, or inactive/opponent base.
- [ ] Start-of-turn income feedback is visible in the strategic UI/HUD/status text.
- [ ] At least one faction-specific dwelling/recruitment offer per faction is gated by base facility state.
- [ ] Recruitment/dwelling stock or refresh behavior is deterministic, serialized in runtime state if mutable, and covered by tests.
- [ ] Existing base construction rules still pass: one build per base per turn, costs, prerequisites, affordability, no partial mutation.
- [ ] Existing movement, site interaction, current recruitment, tactical handoff, battle result application, and objective smoke behavior still pass.
- [ ] No base capture/siege/garrison/marketplace/strategic-AI behavior is added.

## Verification requirements

- Unit/EditMode tests: required for income application timing, faction/base ownership filtering, effect validation, recruitment/dwelling unlock and stock refresh, and no partial mutation cases.
- Data validation tests: required for missing/invalid income effect data, missing facility prerequisites/effect references, invalid recruitment offer references, duplicate/unsupported effect metadata.
- PlayMode tests: required for visible income feedback and facility-unlocked recruitment/dwelling offer flow while preserving existing strategic loop smoke.
- Screenshot/video evidence: required under `production/evidence/STORY-BASE-002/` in the Unity repo showing start-of-turn income feedback and a facility-unlocked recruitment/dwelling offer or recruitment result.
- CI evidence: Unity Foundation CI exact-head before merge and post-merge main CI.
- Playtest evidence: N/A for this story; EPIC-009 closeout remains later.
- TDD evidence required? Yes for production rules and validation behavior.

## Ambiguity Check

Status: PASS.

Human-approved basis:

- EPIC-009 locked income chain size as three levels total and recruitment/dwelling scope as one to two faction-specific offers per faction.
- User requested the next implementation step after `STORY-BASE-001` merge/review.

Assumptions:

- Credits-only recurring income is the narrowest valid first economy effect.
- Existing active Champion army recruitment remains the target; faction reserves/garrisons are deferred.
- Exact prototype numbers are implementation-tunable if kept simple, documented, data-driven, and test-backed.

Out of scope:

- Capture/siege, full town tree, upgraded dwellings, marketplace/trading, strategic AI, editor UI, topology rewrite, and final art.

## Branch / PR requirements

- Branch name: `story/STORY-BASE-002-administration-income-chain-and-recruitment-dwellings`
- PR title: `STORY-BASE-002 Administration income chain and recruitment dwellings`
- Required linked story ID: `STORY-BASE-002`.
- Required linked docs:
  - `design/gdd/strategic-map.md` §§12-16.
  - `design/research/homm-town-building-reference.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Domain/Application/Presentation/Tests/Evidence directories.
- Required evidence summary: tests run, validation cases, PlayMode/smoke result, PNG/manual evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest source is linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/reference sources are linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
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

READY / approved for Unity implementation. Codex may implement only this story scope and must stop rather than expanding into capture/siege, full town tree, upgraded dwellings, marketplace/trading, editor UI, strategic AI, topology rewrite, or final art.
