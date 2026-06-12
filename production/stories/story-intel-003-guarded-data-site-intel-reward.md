---
title: STORY-INTEL-003 Guarded Data Site Intel Reward
type: story
status: draft
phase: production
owner: shared
created: 2026-06-12
updated: 2026-06-12
source_lore: [digital-net, greenland, blue-monday]
related:
  [
    design/gdd/intel-resource,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-004-intel-resource-on-ramp,
    production/stories/story-intel-001-faction-intel-and-data-cache-pickup,
    production/stories/story-intel-002-first-intel-spending-sink-field-upgrade,
  ]
approval: pending
---

# Story: STORY-INTEL-003 Guarded Data Site Intel Reward

## Status

DRAFT / READY-candidate only. Not approved for Unity implementation.

This packet is a prepared next-step candidate after `STORY-INTEL-002` merged. It exists so the next human review can decide whether the Intel on-ramp should continue into guarded/tactical reward flow, stop for epic closeout/playtest, or pivot elsewhere.

## Story type

Tactical/Strategic Integration + Economy + Smoke.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-004-intel-resource-on-ramp.md`.

## User/player/system value

As a vertical-slice tester, I need one guarded data site or guarded reward path to grant Intel only after resolving combat, so Intel can be earned from a higher-risk interaction rather than only a free cache.

## Source requirements

- `design/gdd/intel-resource.md` for Intel as secrets turned into power and for broader reward concepts; note that the broader GDD remains draft/pending.
- `design/gdd/strategic-map.md` for guarded sites, site interaction, control, resources, and battle handoff.
- `design/gdd/tactical-combat.md` for existing tactical resolution boundaries.
- `docs/architecture/control-manifest.md`.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Required prior stories:
  - `STORY-INTEL-001` DONE / merged.
  - `STORY-INTEL-002` DONE / merged.

Authority note: this candidate is not yet an implementation authority. Human approval must decide whether guarded data rewards are the next slice and exactly how narrow the reward should be.

## Candidate problem statement

`STORY-INTEL-001` made Intel collectible from a free data cache. `STORY-INTEL-002` proved one spend sink. The next possible slice is a single guarded data reward: win or resolve one existing guarded encounter, then award a small amount of Intel through the existing strategic result path.

## Candidate in scope, if approved

- Add exactly one guarded data reward path tied to an existing guarded site or a new placeholder guarded data site if reuse is unsafe.
- Reward a small fixed amount of global faction Intel only after the approved guarded-site/tactical resolution condition succeeds.
- Preview/communicate that the guarded site can yield Intel without adding hidden/fog/dirty-information systems.
- Award Intel exactly once, reject duplicates, and prevent partial mutation.
- Preserve existing `STORY-INTEL-001` free cache and `STORY-INTEL-002` field upgrade behavior.
- Add EditMode/application/domain tests for reward preview/commit, tactical/result gating, duplicate rejection, invalid data, resource mutation, and turn persistence.
- Add PlayMode smoke and PNG evidence for before guarded reward, reward preview/encounter, after reward, and persisted Intel total.
- Keep existing objective/combat/recruitment/Intel regressions green.

## Candidate out of scope

- Multiple data vaults, tactical optional objectives, post-battle loot tables, recurring Intel economy, Intel subtypes, fog/hidden information, dirty information, counter-intel cleanup, operations/hacks/doctrine systems, upgrade trees, asset inventory, final content/art/UI redesign, save/load, or strategic AI spending.

## Ambiguity Check

Status: FAIL until human review.

Open decisions before approval:

1. Should the next implementation continue EPIC-004 with a guarded Intel reward, or should EPIC-004 close after the free cache plus first spend sink?
2. Should the guarded reward reuse an existing guarded site, add a placeholder guarded data site, or wait for a broader site-content pass?
3. What exact success condition awards Intel: tactical victory, site capture, battle result return, or a narrower existing smoke condition?
4. What fixed reward amount is approved?
5. Is PNG evidence from the current crude strategic/tactical loop enough, or is a playtest/UX pass required first?

## Branch / PR requirements if later approved

- Suggested branch name: `story/STORY-INTEL-003-guarded-data-site-intel-reward`
- Suggested PR title: `STORY-INTEL-003 Guarded data site Intel reward`
- Required linked story ID: `STORY-INTEL-003`
- Required omissions section: no recurring economy, Intel subtypes, fog/hidden information, dirty information, tactical optional objectives beyond the approved single path, operations/hacks/doctrine, upgrade trees, asset inventory, final content/art/UI redesign, save/load, or strategic AI spending.

## Story readiness gate

- [x] Stable ID, title, type, status, and parent epic exist.
- [x] User/player/system value is clear.
- [x] Prior dependencies are listed.
- [x] Candidate scope is bounded.
- [x] Out-of-scope work is explicit.
- [ ] Human approval has been given for implementation / READY promotion.
- [ ] Ambiguity Check status is PASS.
- [ ] Exact reward amount and success condition are approved.

## Verdict

DRAFT / READY-candidate only. Do not implement until human approval promotes this story to READY / approved and the Ambiguity Check passes.
