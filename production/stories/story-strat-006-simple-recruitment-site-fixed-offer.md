---
title: STORY-STRAT-006 Simple Recruitment Site and Fixed Offer
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-08
updated: 2026-06-08
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
approval: pending
---

# Story: STORY-STRAT-006 Simple Recruitment Site and Fixed Offer

## Status

READY-candidate next implementation packet after `STORY-MAP-001` merged in Unity PR #21. Not READY until explicit human implementation approval is recorded.

## Story type

Logic + UI/Integration + Config/Data.

## Estimate

- Size: M.
- Basis: adds one fixed recruitment/reinforcement offer to the existing strategic map/site interaction path without implementing town buildings, full economy, reserves, dynamic stock refresh, or faction-specific recruitment systems.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat.md`.

## User/player/system value

As a player/designer, I want one visible recruitment/reinforcement site with a fixed offer and clear cost/stock feedback, so the larger map begins to test army-growth pressure rather than only movement, objectives, and guarded-site capture.

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
- Add one fixed placeholder offer with:
  - stable offer ID;
  - placeholder unit/stack reference;
  - fixed cost using existing MVP resources only: Credits and/or Materials; Intel may be present only if the existing stockpile/resource path already supports it safely;
  - fixed finite stock count.
- Preview recruitment before commitment: show offer ID/unit, cost, stock/availability, and whether the active faction can afford it.
- Apply recruitment through explicit site interaction only after validation.
- Add recruited/reinforced units to the active Champion army for MVP, preserving existing army/state serialization patterns.
- Deduct cost from the active faction stockpile only on successful apply.
- Consume/decrement offer stock only on successful apply.
- Keep existing route movement, hotseat turn ownership, guarded-site tactical handoff, BattleResult application, central objective interaction, and map readability behavior intact.
- Add evidence package under `production/evidence/STORY-STRAT-006/README.md`.

## Out of scope

- Full base production, town buildings, construction, upgrade trees, market/economy depth, dynamic pricing, recurring stock refresh, faction-specific recruitment economies, reserves/caravans/garrisons, multiple recruitment sites, multiple offers, final unit balance, final unit names, final site names, final UI art, strategic AI, save/load format changes, and tactical mechanics changes.
- Recruitment from starting hubs unless required as a tiny technical hook for the single recruitment site; if used, it must remain non-player-facing and documented.
- Any automatic recruitment on move/visit without explicit player interaction.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder recruitment site, offer, unit, and localization IDs.
- A single placeholder unit stack added to the active Champion army.
- Simple fixed cost/stock values.
- Minimal text/HUD controls and labels.

Not allowed:

- Final lore/site/unit names.
- Hidden free recruitment that bypasses cost/stock validation.
- Recruitment that mutates tactical battle state directly.
- Recruitment that grants units to the wrong faction, inactive Champion, enemy Champion, or global hidden reserve.

## Dependencies

- Required prior stories:
  - `STORY-MAP-001` DONE / merged in Unity PR #21.
  - Existing larger map, real base/hub site type, two guarded neutral choices, central objective interaction, route movement, hotseat turn ownership, site interaction path, and strategic presentation/HUD must remain on Unity `main`.
- Required data/assets:
  - Placeholder-only recruitment site/offer/unit IDs are sufficient.
- Required architecture decisions:
  - Strategic-map §11 fixed-offer recruitment minimum is binding.
  - Current Unity data/runtime/presentation boundaries remain binding.
- Required Unity/package setup:
  - Existing Unity CI and self-hosted Windows runner path.

## Acceptance criteria

- [ ] Given a new scenario starts, the larger map includes exactly one visible recruitment/reinforcement site reachable through authored routes.
- [ ] Given the recruitment site is displayed, its site category/type and offer availability are readable enough for screenshot review.
- [ ] Given the active Champion reaches the recruitment site and previews interaction, the UI/state shows the fixed offer ID/unit, cost, remaining stock, and affordability before commitment.
- [ ] Given the active faction can afford the offer and stock is available, committing recruitment deducts the correct resources, adds the correct placeholder stack/count to the active Champion army, decrements stock, consumes the Champion's major interaction, and shows readable feedback.
- [ ] Given the active faction cannot afford the offer, committing recruitment is rejected with readable feedback and does not mutate resources, army, stock, movement, site control, or turn ownership.
- [ ] Given stock is exhausted, committing recruitment is rejected with readable feedback and no unintended mutation.
- [ ] Given an inactive faction/Champion attempts recruitment, the interaction is rejected and no state mutates.
- [ ] Given guarded-site capture and central-objective interaction still exist on the larger map, their existing behavior and PlayMode smoke remain valid.
- [ ] Given placeholder recruitment/site/unit labels are used, they are explicitly documented as non-final and stable enough for tests/evidence.
- [ ] CI passes.

## Verification requirements

- Unity EditMode tests: Required for recruitment offer definition validation, cost/stock validation, successful recruitment resource/army/stock mutation, unaffordable rejection/no mutation, exhausted-stock rejection/no mutation, inactive-faction rejection/no mutation, and regression coverage for guarded-site/central-objective preservation.
- Unity PlayMode tests: Required for visible recruitment site readability, offer preview, successful recruitment feedback, and at least one rejection case if feasible.
- Integration/data validation tests: Required if new recruitment fixture/schema validation is added.
- Manual Unity scene/prefab checks: Required if presentation wiring or scene layout changes.
- Screenshot/video evidence: Required for offer preview and successful recruitment state; rejection screenshot preferred if feasible.
- CI evidence: Required.
- TDD evidence required? Yes for recruitment validation/application and regression fixes.
- Automation deferred? No known exception at draft time.

## Ambiguity Check

Status: PASS-candidate / human approval pending.

Assumptions:

- The first recruitment implementation should add units to the active Champion army, matching strategic-map §12.7.
- The first offer should be one fixed placeholder stack with one fixed cost and one fixed finite stock.
- Credits and/or Materials are sufficient for the first cost; do not invent new resources.
- Recruitment site can be an added/converted node in the existing deterministic map as long as the total remains modest and readable.

Open questions:

- Should the first offer use Credits only, Materials only, or Credits + Materials?
- Should recruitment add a new stack when no matching stack exists, or reinforce an existing matching stack up to maximum count if present?
- Should the first recruitment site be guarded before use, or unguarded so this story isolates recruitment mechanics?

Out of scope:

- Full recruitment economy, town/base production, multiple offers/sites, final unit names/balance, reserves/garrisons, and tactical changes.

Allowed stubs/mocks:

- Placeholder site/offer/unit/localization IDs, fixed cost, fixed stock, minimal text controls.

Human-approved exceptions:

- None. User approval is still required before implementation.

## Branch / PR requirements

- Branch name: `story/STORY-STRAT-006-simple-recruitment-site-fixed-offer`
- PR title: `STORY-STRAT-006 Simple recruitment site and fixed offer`
- Required linked story ID: `STORY-STRAT-006`
- Required linked GDD/ADR/control docs: strategic-map §§4, 6, 8, 10, 11, 12; control-manifest; testing strategy; CI/build automation.
- Required root/scoped AGENTS.md instructions: game-design repo `AGENTS.md`; Unity root/scoped `AGENTS.md` files for touched runtime, presentation, tests, and evidence paths.
- Required evidence summary: recruitment checklist, tests, screenshot/video status, CI, omissions/stubs.
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
- [ ] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [ ] Human approval has been given or delegated gate approval is recorded.

## DONE gate

A story may be marked DONE only when all items are true:

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

READY-candidate. Human approval and ambiguity resolution are required before implementation.
