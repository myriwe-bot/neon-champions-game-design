---
title: STORY-STRAT-006 Simple Recruitment Site and Fixed Offers
type: story
status: implemented
phase: production
owner: shared
created: 2026-06-08
updated: 2026-06-09
source_lore: []
related:
  [
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat,
    production/stories/story-map-001-larger-two-base-strategic-map-slice,
  ]
approval: approved
---

# Story: STORY-STRAT-006 Simple Recruitment Site and Fixed Offers

## Status

DONE / merged. Unity PR #22 merged on 2026-06-09 as commit `a699055d67087821a5e6fdcb0f2e84c7d5891b28`; post-merge `main` CI passed for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests.

Implementation delivered the approved dwelling/recruitment site direction: two player-choice offers, normal and upgraded; normal costs Credits only, upgraded costs Credits + Materials; both add placeholder stacks; the site is unguarded for now.

## Story type

Logic + UI/Integration + Config/Data.

## Estimate

- Size: M.
- Basis: adds one simple dwelling/recruitment site with two fixed player-choice offers to the existing strategic map/site interaction path without implementing town buildings, full economy, reserves, dynamic stock refresh, or faction-specific recruitment systems.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat.md`.

## User/player/system value

As a player/designer, I want one visible dwelling/recruitment site with a normal and upgraded fixed offer, so the larger map begins to test meaningful army-growth choice without adding full town/base production.

## Source requirements

- `design/gdd/strategic-map.md` §4 MVP In Scope.
- `design/gdd/strategic-map.md` §6 Core Loop Contract.
- `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft.
- `design/gdd/strategic-map.md` §10 Site and Infrastructure States.
- `design/gdd/strategic-map.md` §11 Resources, Intel, and Recruitment/Reinforcement Minimum.
- `design/gdd/strategic-map.md` §12 Champion/Army Strategic State and Movement Allowance.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.

## In scope

- Add exactly one visible recruitment/reinforcement site to the current deterministic `STORY-MAP-001` strategic map fixture.
- Represent the site as a real `RecruitmentSite` or equivalent approved site category in domain data/runtime/presentation, not only as a label.
- Add exactly two fixed placeholder offers from that one site:
  - a normal offer with stable offer ID, placeholder unit/stack reference, fixed finite stock, and Credits-only cost;
  - an upgraded offer with stable offer ID, upgraded placeholder unit/stack reference, fixed finite stock, and Credits + Materials cost;
  - no Intel cost in this story.
- Preview both recruitment choices before commitment: show normal/upgraded offer IDs, unit/stack labels, costs, stock/availability, and whether the active faction can afford each offer.
- Apply exactly the player-selected offer through explicit site interaction only after validation.
- Add the selected offer as a new placeholder stack to the active Champion army for MVP, preserving existing army/state serialization patterns.
- Deduct cost from the active faction stockpile only on successful apply.
- Consume/decrement only the selected offer stock on successful apply.
- Keep existing route movement, hotseat turn ownership, guarded-site tactical handoff, BattleResult application, central objective interaction, and map readability behavior intact.
- Add evidence package under `production/evidence/STORY-STRAT-006/README.md`.

## Out of scope

- Full base production, town buildings, construction, upgrade trees, market/economy depth, dynamic pricing, recurring stock refresh, faction-specific recruitment economies, reserves/caravans/garrisons, multiple recruitment sites, multiple offers, final unit balance, final unit names, final site names, final UI art, strategic AI, save/load format changes, and tactical mechanics changes.
- Recruitment from starting hubs unless required as a tiny technical hook for the single recruitment site; if used, it must remain non-player-facing and documented.
- Any automatic recruitment on move/visit without explicit player interaction.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder dwelling/recruitment site, normal/upgraded offer, unit, and localization IDs.
- One new placeholder stack added to the active Champion army per successful recruitment.
- Simple fixed cost/stock values: normal = Credits only; upgraded = Credits + Materials.
- Minimal text/HUD controls and labels.

Not allowed:

- Final lore/site/unit names.
- Hidden free recruitment that bypasses cost/stock/player-choice validation.
- Recruitment that mutates tactical battle state directly.
- Recruitment that grants units to the wrong faction, inactive Champion, enemy Champion, or global hidden reserve.

## Dependencies

- Required prior stories:
  - `STORY-MAP-001` DONE / merged in Unity PR #21.
  - Existing larger map, real base/hub site type, two guarded neutral choices, central objective interaction, route movement, hotseat turn ownership, site interaction path, and strategic presentation/HUD must remain on Unity `main`.
- Required data/assets:
  - Placeholder-only dwelling/recruitment site, normal/upgraded offer, and unit IDs are sufficient.
- Required architecture decisions:
  - Strategic-map §11 fixed-offer recruitment minimum is binding.
  - Current Unity data/runtime/presentation boundaries remain binding.
- Required Unity/package setup:
  - Existing Unity CI and self-hosted Windows runner path.

## Acceptance criteria

- [ ] Given a new scenario starts, the larger map includes exactly one visible recruitment/reinforcement site reachable through authored routes.
- [ ] Given the recruitment site is displayed, its site category/type and both normal/upgraded offer availability states are readable enough for screenshot review.
- [ ] Given the active Champion reaches the recruitment site and previews interaction, the UI/state shows both fixed offers with offer ID/unit, cost, remaining stock, and affordability before commitment.
- [ ] Given the active faction selects the normal offer and can afford it, committing recruitment deducts Credits only, adds the normal placeholder stack/count to the active Champion army, decrements only normal stock, consumes the Champion's major interaction, and shows readable feedback.
- [ ] Given the active faction selects the upgraded offer and can afford it, committing recruitment deducts Credits + Materials, adds the upgraded placeholder stack/count to the active Champion army, decrements only upgraded stock, consumes the Champion's major interaction, and shows readable feedback.
- [ ] Given the active faction cannot afford the selected offer, committing recruitment is rejected with readable feedback and does not mutate resources, army, either offer stock, movement, site control, or turn ownership.
- [ ] Given selected-offer stock is exhausted, committing recruitment is rejected with readable feedback and no unintended mutation to resources, army, or the other offer stock.
- [ ] Given an inactive faction/Champion attempts recruitment, the interaction is rejected and no state mutates.
- [ ] Given guarded-site capture and central-objective interaction still exist on the larger map, their existing behavior and PlayMode smoke remain valid.
- [ ] Given placeholder recruitment/site/unit labels are used, they are explicitly documented as non-final and stable enough for tests/evidence.
- [ ] CI passes.

## Verification requirements

- Unity EditMode tests: Required for recruitment offer definition validation, normal Credits-only cost/stock validation, upgraded Credits+Materials cost/stock validation, successful selected-offer resource/army/stock mutation, unaffordable rejection/no mutation, exhausted-stock rejection/no mutation, inactive-faction rejection/no mutation, and regression coverage for guarded-site/central-objective preservation.
- Unity PlayMode tests: Required for visible recruitment site readability, both-offer preview, successful normal or upgraded recruitment feedback, and at least one rejection case if feasible.
- Integration/data validation tests: Required if new recruitment fixture/schema validation is added.
- Manual Unity scene/prefab checks: Required if presentation wiring or scene layout changes.
- Screenshot/video evidence: Required for both-offer preview and successful recruitment state; rejection screenshot preferred if feasible.
- CI evidence: Required.
- TDD evidence required? Yes for recruitment validation/application and regression fixes.
- Automation deferred? No known exception at draft time.

## Ambiguity Check

Status: PASS.

Resolved user decisions, 2026-06-08:

- The site is a dwelling/recruitment site with two player-choice offers.
- Normal offer: Credits-only cost.
- Upgraded offer: Credits + Materials cost.
- Recruitment adds a new placeholder stack; do not merge/reinforce an existing stack in this story.
- Recruitment site is unguarded for now so this packet isolates recruitment mechanics.

Assumptions:

- Both offers use fixed finite stock.
- Placeholder unit IDs are acceptable and non-final.
- The recruitment site can be an added/converted node in the existing deterministic map as long as the total remains modest and readable.

Out of scope:

- Full recruitment economy, town/base production, multiple offers/sites, final unit names/balance, reserves/garrisons, and tactical changes.

Allowed stubs/mocks:

- Placeholder site/normal-offer/upgraded-offer/unit/localization IDs, fixed costs, fixed stocks, minimal text controls.

Human-approved exceptions:

- User approved the two-offer dwelling direction, new-stack behavior, and unguarded recruitment site on 2026-06-08.

## Branch / PR requirements

- Branch name: `story/STORY-STRAT-006-simple-recruitment-site-fixed-offer`
- PR title: `STORY-STRAT-006 Simple recruitment site and fixed offers`
- Required linked story ID: `STORY-STRAT-006`
- Required linked GDD/ADR/control docs: strategic-map §§4, 6, 8, 10, 11, 12; control-manifest; testing strategy; CI/build automation.
- Required root/scoped AGENTS.md instructions: game-design repo `AGENTS.md`; Unity root/scoped `AGENTS.md` files for touched runtime, presentation, tests, and evidence paths.
- Required evidence summary: normal/upgraded recruitment checklist, tests, screenshot/video status, CI, omissions/stubs.
- Required omissions section: placeholder recruitment/site/unit labels, no town/base production, no full economy, no final balance/content.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest sources are linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/art/worldbuilding references are linked if relevant or explicitly N/A.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded on 2026-06-08.

## DONE gate

A story may be marked DONE only when all items are true:

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

DONE. Unity PR #22 merged and post-merge main CI passed on 2026-06-09. Follow-up `STORY-LOOP-003` was approved, then blocked during implementation by the one-attacker-stack tactical setup limitation; `STORY-TAC-006` is the active prerequisite packet.
