---
title: STORY-INTEL-001 Faction Intel and Data Cache Pickup
type: story
status: done
phase: production
owner: shared
created: 2026-06-12
updated: 2026-06-12
source_lore: [digital-net, greenland, blue-monday]
related:
  [
    design/gdd/intel-resource,
    design/gdd/strategic-map,
    design/gdd/game-pillars,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-004-intel-resource-on-ramp,
  ]
approval: approved
---

# Story: STORY-INTEL-001 Faction Intel and Data Cache Pickup

## Status

DONE / merged. Implemented in Unity PR #33 and merged to `main` as `c28e64a25f6283c18463e404ff0368047fbb7ad2` on 2026-06-12. PR-gate Unity Actions passed for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests before merge; post-merge main CI was queued at closeout.

This is intentionally the smallest Intel on-ramp: add a faction-level Intel resource and one visible one-time data cache pickup. Do not add spending, upgrades, fog/hidden information, dirty-information systems, or full economy behavior.

## Story type

Strategic Logic + UI/Integration + Config/Data + UX/Smoke.

## Estimate

- Size: M.
- Basis: adds a minimal resource field, one cache interaction path, validation/presentation, and PlayMode evidence. It should not require new scenes, final assets, economy balancing, or tactical changes.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-004-intel-resource-on-ramp.md`.

## User/player/system value

As a vertical-slice tester, I need to see a faction discover and claim Intel on the strategic map, so the prototype starts proving the “secrets become power” pillar before adding spending or dirty-information complexity.

## Source requirements

- `design/gdd/intel-resource.md` §§19-24 for summary/layer; §§51-78 for player fantasy and core rules; §§79-91 for acquisition modes; §§103-118 for prototype values; §§156-164 for acceptance criteria.
- `design/gdd/strategic-map.md` §§6, 8, 10, 11, 12, 13 for sites, control, resources, recruitment/reinforcement context, and turn persistence.
- `design/gdd/game-pillars.md` for Intel as secrets turned into power.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Parent epic: `EPIC-VSLICE-MVP-004`.
- Baseline: Unity `main` after PR #32 / merge commit `2ed6d38624bc7aabd824ec1ce2162e6ce7523dd2` plus README pointer commit `7409b3dbfaa97b3c632ba6f8c7da10eb17b667df`.

Authority note: the broader Intel GDD remains draft/pending. This story approves only the exact minimal Intel earning/display scope below.

## Problem statement

The current vertical slice has movement, recruitment, guarded combat, objective victory feedback, Champion-vs-Champion conflict, and casualty stakes. It still lacks any visible Intel resource, so the cyberpunk “secrets turned into power” pillar is not yet represented in gameplay.

## In scope

- Add faction-level Intel resource state to the current strategic scenario/runtime snapshot.
- Show each relevant faction's Intel amount in player-facing HUD/status text using placeholder labels, e.g. `INTEL 0` / `INTEL 5`.
- Add one deterministic data cache source to the current scenario using placeholder IDs/text.
- Allow the active faction to claim the data cache once when its Champion reaches/interacts with the cache through existing strategic interaction boundaries.
- Award a small placeholder amount: `+5 Intel`.
- Mark the cache claimed/depleted/controlled so the same cache cannot award Intel twice.
- Preserve Intel state across end-turn transitions.
- Add or extend validation for any new data/definition fields introduced by this story, including stable IDs and non-negative Intel reward values.
- Add EditMode/application/domain tests for resource state, one-time award, invalid/no-duplicate interaction, and persistence semantics.
- Add PlayMode smoke asserting visible cache, visible Intel amount before/after claim, one-time claim feedback, and turn persistence.
- Produce PNG evidence under `production/evidence/STORY-INTEL-001/` showing before claim, after claim, and persistence/summary.
- Keep existing LOOP-004/objective/combat regressions green.

## Out of scope

- Intel spending, upgrades, asset empowerment, operations, hacks, doctrine, recruitment-site upgrades, elite unlocks, or map-layer reveals.
- Intel subtypes such as HUMINT/SIGINT/Research/Proof.
- Fog of war, hidden routes/sites, spoofing, polluted feeds, dirty-information state, or counter-intel cleanup.
- Reverse-engineering/dismantling assets.
- Recurring weekly income, Intel Exchanges, Analysis Cells, markets, or full resource economy balancing.
- Tactical optional objectives or post-battle Intel rewards.
- Strategic AI or enemy autonomous collection.
- Final content/lore names, icons, art, animation, accessibility, or broad UI redesign.
- Save/load implementation.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder data cache ID, site/node label, localization key, and HUD copy.
- Hardcoded prototype value `+5 Intel` if it is attached to a scenario/cache definition or clearly isolated test fixture; avoid scattering tunable constants through presentation code.
- Existing crude strategic map visuals and placeholder UI.
- PNG evidence from CI/local smoke capture.

Not allowed:

- Fake evidence that does not come from the actual Unity scene/test path.
- Hidden resource mutation outside approved domain/application result paths.
- Adding spending systems only to make the resource feel useful.
- Adding final cyberpunk lore/content names under this story.

## Dependencies

- Required prior stories:
  - `STORY-LOOP-004` DONE / merged in Unity PR #32.
- Required architecture decisions:
  - Existing Unity root/scoped `AGENTS.md` rules remain binding.
  - Existing strategic-map application/domain/presentation boundaries remain binding.
- Required data/assets:
  - Placeholder IDs only; no final art/content dependencies.

## Acceptance criteria

- [ ] Given the MVP scenario starts, the active faction has `0` Intel and the HUD/status visibly communicates that amount.
- [ ] Given the active Champion reaches/selects the data cache, the player can see that it is an Intel/data-cache source before claiming it.
- [ ] Given the active Champion claims the data cache, the active faction gains `+5 Intel`, the HUD/status updates visibly, and feedback communicates the gain.
- [ ] Given the same cache is selected after it has been claimed, it cannot award Intel a second time and no partial/duplicate mutation occurs.
- [ ] Given turn ownership advances after the claim, the claiming faction's Intel total persists and the other faction's Intel total is unchanged.
- [ ] Given validators run, any introduced data/cache reward fields require stable IDs and non-negative Intel reward values.
- [ ] Existing objective/combat/recruitment regressions remain green.
- [ ] PNG evidence shows before claim, after claim, and persisted Intel state.
- [ ] CI passes.

## Verification requirements

- Unit/EditMode tests: required for resource state, one-time data-cache award, invalid duplicate/no-partial-mutation behavior, and turn persistence semantics.
- Unity PlayMode tests: required for visible Intel HUD/status, visible data cache source, claim feedback, and persistence across turn transition.
- Integration/data validation tests: required if any scenario/cache definition fields are added.
- Placeholder validator: must remain passing and should cover new fields if applicable.
- Screenshot/video evidence: PNG evidence required under `production/evidence/STORY-INTEL-001/` or equivalent story evidence path.
- CI evidence: required on PR branch and post-merge main if merged.
- TDD evidence required? Yes for production logic and validators.
- Automation deferred? No, except final visual/readability judgement is supplemental.

## Ambiguity Check

Status: PASS.

Human-approved decisions recorded on 2026-06-12:

1. Next implementation spine after EPIC-VSLICE-MVP-003 is a minimal Intel resource on-ramp.
2. `STORY-INTEL-001` may add only faction Intel earning/display and one deterministic data cache pickup.
3. The broader Intel GDD remains draft/pending; this story must not implement spending, upgrades, fog, dirty information, economy depth, tactical Intel rewards, or final content.
4. Use placeholder IDs/copy and current prototype UI/evidence style.

Assumptions for implementation:

- Intel is stored globally per faction for MVP.
- The first data cache awards `+5 Intel`.
- Data cache interaction should use existing strategic interaction/application boundaries where feasible.

## Branch / PR requirements

- Branch name: `story/STORY-INTEL-001-faction-intel-data-cache-pickup`
- PR title: `STORY-INTEL-001 Faction Intel and data cache pickup`
- Required linked story ID: `STORY-INTEL-001`
- Required evidence summary: Intel resource state, data-cache claim, duplicate/no-partial-mutation test, visible HUD/status feedback, PlayMode/PNG evidence, CI, omissions.
- Required omissions section: no Intel spending/upgrades, no fog/hidden information, no dirty information, no tactical Intel rewards, no recurring Intel economy, no final content/art/UI redesign.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest sources are linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given for implementation / READY promotion.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence pass on the PR branch.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes on PR branch; post-merge `main` run was queued when the story was closed.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged. No further implementation is authorized under this story; use `STORY-INTEL-002` for the next approved Intel slice.
