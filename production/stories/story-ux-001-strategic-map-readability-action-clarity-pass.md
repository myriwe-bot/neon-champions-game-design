---
title: STORY-UX-001 Strategic Map Readability and Action Clarity Pass
type: story
status: done
phase: production
owner: shared
created: 2026-06-12
updated: 2026-06-12
source_lore: [greenland, digital-net, blue-monday]
related:
  [
    design/gdd/strategic-map,
    design/gdd/intel-resource,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-004-intel-resource-on-ramp,
    production/stories/story-intel-004-intel-on-ramp-closeout-smoke,
  ]
approval: approved
---

# Story: STORY-UX-001 Strategic Map Readability and Action Clarity Pass

## Status

DONE / merged. Human approved implementation on 2026-06-12.

This is the next implementation packet after `STORY-INTEL-004` because the prototype now has a connected strategic loop with movement, cache claim, placeholder Field Upgrade spend, guarded reward, and tactical return. Before adding deeper systems, the next risk is whether a human can read and operate the crude strategic map well enough to evaluate the loop.

## Story type

UI / Visual-Feel / Playability Smoke.

## Parent / context

- Immediate predecessor: `STORY-INTEL-004 Intel On-Ramp Closeout Smoke` DONE / merged.
- Context epic: `production/epics/epic-vslice-mvp-004-intel-resource-on-ramp.md` awaiting human closeout/playtest review.

## User/player/system value

As a human tester, I need the current strategic-map prototype to clearly show who is acting, what is selected, what can be clicked, what action is available, and what changed after each action, so I can actually play/review the vertical slice instead of decoding raw debug text.

## Source requirements

- `design/gdd/strategic-map.md` for strategic map interaction, nodes/routes/sites, turn state, active faction, and battle handoff.
- `design/gdd/intel-resource.md` only for preserving existing Intel display and placeholder Field Upgrade clarity; no new Intel mechanics are authorized.
- `docs/architecture/control-manifest.md`.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Required prior stories:
  - `STORY-INTEL-001` DONE / merged.
  - `STORY-INTEL-002` DONE / merged.
  - `STORY-INTEL-003` DONE / merged.
  - `STORY-INTEL-004` DONE / merged.

Authority note: human approval on 2026-06-12 authorizes only this bounded readability/action-clarity pass before further gameplay/system expansion.

## Problem statement

The connected Intel smoke proves the loop technically works, but it is still a crude prototype. If the player cannot quickly tell the active faction, selected Champion, reachable routes/nodes, selected site, available action, Intel total, Field Upgrade state, guarded reward state, and action result, then further gameplay features will outrun playability.

## In scope

- Improve the existing strategic-map prototype presentation enough to make the current loop readable at 1280x720 evidence resolution.
- Make the following states visually/textually clear without requiring source-code knowledge:
  - active faction and turn/round;
  - selected Champion and current army summary;
  - reachable nodes/routes;
  - selected site and available action;
  - current Intel total;
  - placeholder `field_upgrade_alpha` / “Field Upgrade” status, cost, affordability, and applied state;
  - guarded reward preview/result;
  - latest diagnostic/action result.
- Prefer layout/label/focus/highlight changes in existing presentation code over new mechanics.
- Add or refine PlayMode assertions that visible text/elements do not overlap critical controls at the target evidence resolution where feasible.
- Produce before/after PNG evidence under `production/evidence/STORY-UX-001/`.
- Keep existing INTEL-001/002/003/004, objective/combat/recruitment, and tactical regressions green.

## Out of scope

- New gameplay mechanics, new Intel sources/sinks, new field-upgrade mechanics, new tactical objectives, save/load, strategic AI, accessibility pass beyond the current crude prototype, final art/icons/animation, final UI skin, localization, broad redesign, camera/zoom system, or replacing the prototype with a full production UI architecture.

## Ambiguity Check

Status: PASS.

Human-approved decisions recorded on 2026-06-12:

1. Run this readability/action-clarity pass before further gameplay/system expansion.
2. Keep scope to small layout, focus, highlight, label, and copy changes in the current prototype presentation.
3. Broader UI architecture work, camera/zoom, final art, and full production UI are deferred and out of scope.
4. Generic prototype-readability criteria are acceptable for this packet; if implementation/evidence reveals concrete overlap/clickability issues, preserve them as acceptance evidence and fix only within this bounded pass.

## Branch / PR requirements if later approved

- Branch name: `story/STORY-UX-001-strategic-map-readability-action-clarity-pass`
- PR title: `STORY-UX-001 Strategic map readability and action clarity pass`
- Required linked story ID: `STORY-UX-001`
- Required omissions section: no new gameplay mechanics, no new Intel systems, no save/load, no strategic AI, no final art/UI redesign.

## Story readiness gate

- [x] Stable ID, title, type, status, and parent/context exist.
- [x] User/player/system value is clear.
- [x] Prior dependencies are listed.
- [x] Candidate scope is bounded.
- [x] Out-of-scope work is explicit.
- [x] Human approval has been given for implementation / READY promotion.
- [x] Ambiguity Check status is PASS.
- [x] Concrete readability/playability acceptance drivers are approved or accepted as generic prototype-readability criteria.

## Verdict

READY / approved for implementation. Codex may implement exactly this packet from the checked-in prompt file `production/sprints/codex-story-ux-001.prompt.txt` after preflight confirms status/approval/PASS.

## Merge result

Merged PR: https://github.com/myriwe-bot/neon-champions-unity/pull/37

Squash merge commit: `a43ed135bb07f495a7cff791aeca562d5afe936b`

Review note: independent review found a right-panel overflow/readability blocker; fixed before merge with compact high-risk states and stronger PlayMode layout assertions.
