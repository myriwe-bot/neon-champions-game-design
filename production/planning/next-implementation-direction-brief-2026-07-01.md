---
title: Next Implementation Direction Brief — 2026-07-01
type: decision-brief
status: ready-candidate
phase: production
owner: shared
created: 2026-07-01
updated: 2026-07-01
related:
  - production/epics/epic-vslice-mvp-012-intel-leads-and-verification
  - production/stories/story-intel-dirty-003-intel-layer-closeout-smoke
  - design/gdd/intel-resource
  - design/gdd/strategic-map
  - design/gdd/tactical-combat
approval: pending
---

# Next Implementation Direction Brief — 2026-07-01

## State

`STORY-INTEL-DIRTY-003 Intel Layer Closeout Smoke` is DONE / merged. Unity PR #124 merged as `a94f83b651bf181fa85dd23165e4ae7a9a1b5b93`; exact-head PR CI and post-merge `main` CI passed. Unity current-task cleanup PR #125 merged as `362a407bf8a6f3c1955544981ad38d25950904ec`; pointer-cleanup CI and post-cleanup `main` CI passed.

`EPIC-VSLICE-MVP-012 Intel Leads and Verification` is DONE / closed for the approved MVP slice. The game now has visible normal `Intel Lead`, deterministic `Stale Lead`, active-Champion verification, defender-strength / tactical-risk previews, repeat no-spend feedback, unrelated-marker preservation, and connected strategic-loop smoke evidence.

This brief is not implementation authorization. A next epic/story must be explicitly approved before Codex starts Unity runtime work.

## Viable next directions

1. **Scenario pressure and victory readability** — sharpen the duel/race objective loop with clearer pressure, pacing, win/loss signals, and one connected playability smoke.
2. **Tactical combat role depth** — build on the readable tactical surface with one narrow role/counter mechanic, better AP choice clarity, or reaction readability.
3. **Strategic economy/base depth** — extend base/facility choices, income-chain readability, and recruitment dwellings without full town-tree sprawl.
4. **Dirty-information next epic** — start a new, explicitly approved layer for contested/false leads, PR/hearts-and-minds, or counter-intel; this must not be smuggled into closed EPIC-012.

## Recommended default

Recommend **Scenario pressure and victory readability** as the next implementation direction.

Why:

- It converts the accumulated strategic/tactical/intel slices into a more testable game loop rather than adding another disconnected subsystem.
- It should expose the most valuable next playtest blockers: pacing, victory/loss comprehension, pressure, and whether the current strategic choices matter.
- It can stay narrow: one objective-pressure/readability story, one connected smoke, no new economy, no broad AI, no full campaign layer.
- It preserves the new Intel layer as a readable support surface without immediately jumping to false-information complexity.

## Suggested first implementation slice if approved

`STORY-PRESSURE-001 Objective Pressure and Victory Readability Smoke`:

- Use the existing scenario objective/victory surfaces; do not add a new campaign mode.
- Make the current objective pressure, threat/timer/contest state, and win/loss direction clearer in HUD/status text.
- Prove one connected loop where a player can understand what is pressuring them, what action changes it, and how victory/loss feedback appears.
- Add focused EditMode/PlayMode coverage and generated evidence for before-pressure, pressure-change, victory/loss-readability, and surrounding-loop-unbroken states.

## Approval gate

Approval pending. If the human approves option 1 / Scenario pressure, promote a narrow first story and runnable Codex prompt to READY / approved, then update the Unity README current-task pointer through a CI-gated docs PR before handing off implementation.
