---
title: STORY-INTEL-002 First Intel Spending Sink — Field Upgrade
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
    production/stories/story-intel-001-faction-intel-and-data-cache-pickup,
  ]
approval: approved
---

# Story: STORY-INTEL-002 First Intel Spending Sink — Field Upgrade

## Status

DONE / merged. Implemented in Unity PR #34 and squash-merged to `main` as `cc0b3070de38da8891f5f0f02de4a354e90aed06` on 2026-06-12. PR-gate Unity Actions passed for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests on exact PR head `188fbfa4bb0bd363a5a76539c0812b7109255b02`; post-merge `main` Unity Actions also completed successfully at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27419055491.

This is intentionally the smallest Intel-use slice: add one visible, one-time placeholder Intel spend that turns the newly claimed data cache into a concrete tactical/strategic advantage. Do not build a full upgrade tree, asset inventory, operation system, fog/hidden information, dirty-information mechanics, recurring economy, or final content.

## Story type

Strategic Economy + Domain Logic + UI/Integration + UX/Smoke.

## Estimate

- Size: M.
- Basis: adds one spend command/service path, one placeholder upgrade state/effect, validation, UI affordance/feedback, and PlayMode evidence. It should not require new scenes, final art, asset inventory, save/load, AI, or broad economy balancing.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-004-intel-resource-on-ramp.md`.

## User/player/system value

As a vertical-slice tester, I need to spend newly earned Intel on one visible placeholder field upgrade, so Intel stops being only a displayed number and starts proving the “secrets become power” pillar.

## Source requirements

- `design/gdd/intel-resource.md` §§19-24 for Intel summary/layer; §§51-78 for player fantasy/core rules; §§92-118 for spending modes and prototype values; §§146-164 for tuning knobs and acceptance criteria.
- `design/gdd/strategic-map.md` §§6, 8, 10, 11, 12, 13 for sites, control, resources, turn state, and tactical battle handoff context.
- `design/gdd/game-pillars.md` for Intel as secrets turned into power.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Parent epic: `EPIC-VSLICE-MVP-004`.
- Required prior story: `STORY-INTEL-001` DONE / merged in Unity PR #33 as merge commit `c28e64a25f6283c18463e404ff0368047fbb7ad2`.

Authority note: the broader Intel GDD remains draft/pending. Human approval on 2026-06-12 authorizes only this bounded first spend subset: one placeholder field upgrade using global faction Intel. Broader Intel spending systems remain unapproved.

## Problem statement

`STORY-INTEL-001` made Intel visible and collectible through one data cache. The player can now see Intel increase, but cannot yet convert it into power. The next useful vertical-slice proof is a tiny spend loop: collect Intel, spend it once, see a concrete upgrade, and verify no duplicate/invalid spending occurs.

## In scope

- Add one deterministic placeholder Intel spending sink named `field_upgrade_alpha` or similarly neutral placeholder ID.
- Cost: `5 Intel` for this story, as a narrow prototype tuning exception within the GDD safe range for basic asset upgrades (`5-20`) so the `+5 Intel` cache from INTEL-001 can immediately prove the earn->spend loop.
- The spend targets the active selected Champion and uses the active faction's global Intel stockpile.
- Applying the upgrade must:
  - deduct exactly `5 Intel` from the active faction;
  - mark the target Champion as having the placeholder field upgrade so it cannot be applied twice;
  - produce a small visible prototype advantage by increasing the Champion's attached army first valid stack current and maximum count by `+2`, or an equally narrow existing-stack-strength effect if implementation finds a safer current-domain equivalent;
  - preserve the upgraded state/effect across end-turn transitions;
  - flow naturally into existing guarded-site or Champion-vs-Champion battle setup if the attached army participates later.
- Add preview/availability text in the current crude UI/HUD so the player can see the spend option, cost, affordability, and result using placeholder copy.
- Add commit/action path through existing application/domain boundaries; presentation must not mutate domain state directly.
- Add validation/diagnostics for insufficient Intel, missing selected/active Champion, duplicate upgrade, missing faction stockpile, and invalid upgrade definition/cost if a new definition shape is introduced.
- Add EditMode/application/domain tests for preview, successful spend, resource deduction, upgrade marker/effect, duplicate rejection, insufficient-Intel rejection, no partial mutation, and turn persistence.
- Add PlayMode smoke asserting visible spend availability after claiming the cache, visible cost/result feedback, visible Intel decrease to `0`, visible upgraded army/status summary, and persistence after turn transition.
- Produce PNG evidence under `production/evidence/STORY-INTEL-002/` showing before spend, spend preview, after spend, and persisted upgraded state.
- Keep existing INTEL-001, LOOP-004, objective/combat/recruitment regressions green.

## Out of scope

- Upgrade trees, multiple spend options, multiple levels, refund/respec, tooltips beyond placeholder copy, or balance UX.
- Asset inventory, artifact equipment, operation/hack/doctrine leveling, recruitment-site upgrades, elite unlocks, map-layer reveals, counter-intel cleanup, dirty information, fog/hidden information, Intel subtypes, or recurring Intel economy.
- Additional data caches, guarded data vaults, tactical optional objectives, or post-battle Intel rewards.
- Strategic AI or enemy autonomous spending.
- Final cyberpunk names, final icons, art, animation, accessibility pass, broad UI redesign, save/load implementation, or persistence beyond existing runtime state.

## Allowed stubs, mocks, placeholders, or temporary data

Placeholder naming note: `field_upgrade_alpha` / “Field Upgrade” is not a canon designed upgrade system. Human decision on 2026-06-12: keep “Field Upgrade” approved for now as a temporary placeholder name/mechanic for the first Intel spend sink; it may be renamed, re-fictionalized, or replaced when Champion assets/upgrades are designed properly.

Allowed:

- Placeholder upgrade ID/name/copy such as `field_upgrade_alpha` / `FIELD UPGRADE` / `Analyzed field kit`.
- Prototype cost `5 Intel`, explicitly scoped to this first earn->spend proof.
- Prototype effect `+2` to one existing attached-army stack, if represented through existing domain state and covered by tests.
- Existing crude strategic map visuals and placeholder UI.
- PNG evidence from CI/local smoke capture.

Not allowed:

- Fake evidence that does not come from the actual Unity scene/test path.
- Hidden resource mutation outside approved domain/application result paths.
- Presentation code directly changing Champion/army/resource state.
- Creating a general-purpose upgrade framework, final asset system, or broader economy just to support this one spend.
- Weakening the INTEL-001 one-time cache semantics.

## Dependencies

- Required prior stories:
  - `STORY-INTEL-001` DONE / merged.
- Required architecture decisions:
  - Existing Unity root/scoped `AGENTS.md` rules remain binding.
  - Existing strategic-map application/domain/presentation boundaries remain binding.
  - Existing resource summary and site interaction patterns should be reused where feasible.
- Required data/assets:
  - Placeholder IDs/copy only; no final art/content dependencies.

## Acceptance criteria

- [ ] Given the active faction has claimed the INTEL-001 data cache and has `5 Intel`, the player can see a placeholder field-upgrade spend option with cost `5 Intel`.
- [ ] Given the player commits the field upgrade for the active selected Champion, the active faction's Intel decreases by exactly `5`, the Champion is marked upgraded, and feedback communicates the spend and result.
- [ ] Given the upgrade is applied, the Champion's attached army shows a small visible prototype improvement (`+2` to the first valid stack current/maximum count, or the approved narrow equivalent), and that improvement is reflected in presentation/army summary.
- [ ] Given the same Champion tries to buy the same upgrade again, the action is rejected with a diagnostic and no duplicate resource or stack mutation occurs.
- [ ] Given a faction has insufficient Intel, the spend option is unavailable or rejected with a diagnostic and no partial mutation occurs.
- [ ] Given turn ownership advances after the spend, the claiming faction's Intel total, upgraded Champion marker/effect, and attached-army improvement persist in runtime state and visible summary when control returns to that faction.
- [ ] Given validators/tests run, any introduced spend/upgrade definition fields require stable IDs, non-negative costs, supported resource IDs, and valid non-negative stack effect values.
- [ ] Existing INTEL-001, objective/combat/recruitment regressions remain green.
- [ ] PNG evidence shows before spend, spend preview, after spend, and persisted upgraded state.
- [ ] CI passes.

## Verification requirements

- Unit/EditMode tests: required for spend preview, valid spend, insufficient Intel, duplicate rejection, no partial mutation, resource deduction, upgrade marker/effect, and turn persistence.
- Unity PlayMode tests: required for visible spend option/cost, claim->spend flow, spend feedback, Intel decrease, upgraded army/status summary, and persistence across turn transition.
- Integration/data validation tests: required if any upgrade/spend definition fields are added.
- Placeholder validator: must remain passing and should cover new placeholder fields if applicable.
- Screenshot/video evidence: PNG evidence required under `production/evidence/STORY-INTEL-002/` or equivalent story evidence path.
- CI evidence: required on PR branch and post-merge main if merged.
- TDD evidence required? Yes for production logic and validators.
- Performance budget: N/A; no heavy rendering/pathfinding/simulation work authorized.

## Ambiguity Check

Status: PASS.

Human-approved decisions recorded on 2026-06-12:

1. After INTEL-001, the next slice should make Intel useful rather than only visible.
2. This story may implement one narrow placeholder spend sink only.
3. Cost `5 Intel` is allowed for this story so the existing `+5 Intel` cache can prove the earn->spend loop immediately; this is not final balance.
4. The first spend is represented as a placeholder Champion field upgrade, not a full asset inventory or upgrade tree.
5. A small existing-stack improvement is allowed as the temporary visible gameplay effect because current MVP has attached armies and tactical handoff, but final asset/gear systems remain unapproved.
6. Broader Intel systems remain draft/pending and out of scope.

Assumptions for implementation:

- Intel remains stored globally by faction for MVP.
- The active selected Champion is the target of the spend.
- If the selected Champion has no valid attached stack, the spend must reject instead of inventing a new unit or asset.
- If the existing domain has a safer narrow way to represent the field upgrade than `+2` to the first valid stack, the implementer may use it only if it is equally small, visible, tested, and does not require broader design decisions.

## Branch / PR requirements

- Branch name: `story/STORY-INTEL-002-first-intel-spending-sink-field-upgrade`
- PR title: `STORY-INTEL-002 First Intel spending sink field upgrade`
- Required linked story ID: `STORY-INTEL-002`
- Required evidence summary: earn->spend flow, spend preview, resource deduction, one-time upgrade, insufficient/duplicate rejection, visible HUD/status feedback, PlayMode/PNG evidence, CI, omissions.
- Required omissions section: no upgrade tree, no asset inventory, no operations/hacks/doctrine, no recruitment-site upgrades, no fog/hidden information, no dirty information, no tactical Intel rewards, no recurring Intel economy, no final content/art/UI redesign.

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
- [x] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence pass.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes on PR branch and post-merge `main`.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged. No further implementation is authorized under this story; use `STORY-INTEL-003` only after human approval promotes it from DRAFT / READY-candidate to READY / approved.
