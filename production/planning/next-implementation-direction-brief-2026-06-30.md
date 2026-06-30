---
title: Next Implementation Direction Brief — 2026-06-30
type: decision-brief
status: draft
phase: production
owner: shared
created: 2026-06-30
updated: 2026-06-30
related:
  - production/epics/epic-vslice-mvp-011-champion-assets-and-operations-depth
  - production/stories/story-champ-ops-003-operation-aftermath-and-closeout-readability-smoke
  - design/gdd/intel-resource
  - design/gdd/strategic-map
  - design/gdd/tactical-combat
approval: pending
---

# Next Implementation Direction Brief — 2026-06-30

## State

`STORY-CHAMP-OPS-003` is DONE / merged. Unity PR #114 merged as `bee8f80459cdaff36f618dfe95b6810a5fabd817`; exact-head PR CI and post-merge `main` CI passed. Unity current-task cleanup PR #115 merged as `dfeae1dd4c34bac12c712b7df1eb45fb97cff14f`; pointer PR CI and post-merge `main` CI passed.

`EPIC-VSLICE-MVP-011 Champion Assets and Operations Depth` is DONE / closed for the approved vertical-slice scope. The project now has a visible Champion Asset/Operation surface, one prototype forecast Operation, target readability, post-use/repeat-denial feedback, and connected strategic-loop smoke evidence.

This brief is not implementation authorization. A next epic/story must be explicitly approved before Codex starts Unity runtime work.

## Viable next directions

1. **Intel and dirty-information layer** — make Intel less placeholder-like: scouting, forecast/reveal, misinformation hooks, blackmail-style operations, and false-certainty language without full fog-of-war.
2. **Tactical combat role depth** — build on the readable tactical surface with one or two unit-role abilities/counters, clearer AP choices, morale/cohesion-lite, or reaction readability.
3. **Strategic economy/base depth** — extend base/facility choices, income-chain readability, and recruitment dwellings carefully, without full town-tree sprawl.
4. **Scenario pressure and victory readability** — sharpen the playable duel/race objective loop with clearer pressure, pacing, win/loss signals, and one connected playability smoke.

## Recommended default

Recommend **Intel and dirty-information layer** as the next epic direction.

Why:

- It naturally follows EPIC-011: Champion Operations already spend Intel and forecast sites, so the next layer can deepen Intel without inventing magic.
- It strengthens a core Neon Champions pillar: secrets, infrastructure access, PR/hearts-and-minds, and contested certainty.
- It can stay narrow: one readable Intel action/effect, one proof path, and explicit deferral of full fog-of-war or strategic AI.
- It differentiates the game from a generic HoMM-like while reusing existing map/site/HUD surfaces.

## Suggested first implementation slice if approved

`STORY-INTEL-DIRTY-001 Intel Lead and False Certainty On-Ramp`:

- Add a minimal Intel Lead presentation model tied to existing strategic sites or guarded-site forecast state.
- Show one readable Intel action/effect that changes player certainty or site knowledge without full fog-of-war.
- Use existing Intel resource language; do not add new resources or recurring income.
- Add focused EditMode coverage plus PlayMode evidence for before/after certainty, invalid/repeat attempt behavior, and one normal strategic loop remaining usable.

## Approval gate

Approval pending. If the human approves this direction, create/approve a bounded epic and first READY story/prompt before updating the Unity current-task pointer.
