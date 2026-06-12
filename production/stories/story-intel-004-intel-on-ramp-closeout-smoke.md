---
title: STORY-INTEL-004 Intel On-Ramp Closeout Smoke
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
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-004-intel-resource-on-ramp,
    production/stories/story-intel-001-faction-intel-and-data-cache-pickup,
    production/stories/story-intel-002-first-intel-spending-sink-field-upgrade,
    production/stories/story-intel-003-guarded-data-site-intel-reward,
  ]
approval: pending
---

# Story: STORY-INTEL-004 Intel On-Ramp Closeout Smoke

## Status

DRAFT / READY-candidate only. Not approved for Unity implementation.

This candidate exists because `STORY-INTEL-001`, `STORY-INTEL-002`, and `STORY-INTEL-003` now prove the three separate Intel beats: free cache earning, first spend sink, and guarded reward. The next useful step is a narrow closeout smoke that proves the whole Intel on-ramp is visible and coherent enough for human review, without adding new Intel mechanics.

## Story type

Connected Smoke + UX/QA + Evidence.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-004-intel-resource-on-ramp.md`.

## User/player/system value

As a vertical-slice tester, I need one visible play path that shows Intel being earned, spent, and earned again from a guarded reward, so the EPIC-004 Intel on-ramp can be judged as a coherent player loop rather than three isolated features.

## Source requirements

- `design/gdd/intel-resource.md` for Intel as secrets turned into power; only the already-approved INTEL-001/002/003 subset is implementation authority.
- `design/gdd/strategic-map.md` for site interaction, resources, turn state, guarded sites, and battle return.
- `docs/architecture/control-manifest.md`.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Required prior stories:
  - `STORY-INTEL-001` DONE / merged.
  - `STORY-INTEL-002` DONE / merged.
  - `STORY-INTEL-003` DONE / merged.

Authority note: this candidate is not yet implementation authority. Human approval must decide whether EPIC-004 needs this closeout smoke before epic closeout/playtest review.

## Candidate problem statement

The separate Intel slices pass individually, but human review still needs one concise evidence path that answers: can a player/tester see Intel start at 0, earn it from a cache, spend it on the field upgrade, earn it again from a guarded reward, and understand what changed?

## Candidate in scope, if approved

- Add or refine exactly one connected PlayMode smoke path that covers the existing Intel sequence end to end:
  1. active faction starts with visible `Intel 0`;
  2. claims the existing free data cache and reaches `Intel 5`;
  3. spends `5 Intel` on the existing placeholder `field_upgrade_alpha` field upgrade and returns to `Intel 0`;
  4. resolves the existing guarded Intel reward path and receives exactly `5 Intel`;
  5. verifies the field-upgraded Champion/army state and final Intel total persist across a turn transition / return to faction.
- Add only minimal HUD/status copy or evidence-label adjustments if the existing smoke is unreadable or cannot communicate the sequence.
- Produce PNG evidence under `production/evidence/STORY-INTEL-004/` showing the connected sequence and final persisted state.
- Keep all INTEL-001/002/003, objective/combat/recruitment, and tactical regressions green.

## Candidate out of scope

- New Intel sources or sinks.
- New guarded sites beyond the existing INTEL-003 path.
- New tactical optional objectives, loot tables, recurring economy, Intel subtypes, fog/hidden information, dirty information, counter-intel cleanup, operations/hacks/doctrine systems, upgrade trees, asset inventory, save/load, final content/art/UI redesign, strategic AI spending, or broad UI/playability pass.

## Ambiguity Check

Status: FAIL until human review.

Open decisions before approval:

1. Is an extra closeout smoke needed before EPIC-004 human closeout/playtest review, or is INTEL-003 evidence sufficient?
2. If approved, should this be implementation work in Unity, or a design/QA closeout packet with no runtime changes?
3. Are minimal HUD/status copy changes allowed only if the connected evidence is unclear?

## Branch / PR requirements if later approved

- Suggested branch name: `story/STORY-INTEL-004-intel-on-ramp-closeout-smoke`
- Suggested PR title: `STORY-INTEL-004 Intel on-ramp closeout smoke`
- Required linked story ID: `STORY-INTEL-004`
- Required omissions section: no new Intel mechanics, no new economy systems, no hidden/dirty information, no new tactical objectives, no final content/art/UI redesign.

## Story readiness gate

- [x] Stable ID, title, type, status, and parent epic exist.
- [x] User/player/system value is clear.
- [x] Prior dependencies are listed.
- [x] Candidate scope is bounded.
- [x] Out-of-scope work is explicit.
- [ ] Human approval has been given for implementation / READY promotion.
- [ ] Ambiguity Check status is PASS.
- [ ] Closeout-smoke vs direct epic-closeout decision is approved.

## Verdict

DRAFT / READY-candidate only. Do not implement until human approval promotes this story to READY / approved and the Ambiguity Check passes.
