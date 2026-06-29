---
title: Next Implementation Direction Brief — 2026-06-29
type: decision-brief
status: approved
phase: production
owner: shared
created: 2026-06-29
updated: 2026-06-29
related:
  - production/stories/story-ux-002-tactical-playability-scale-resource-hud-and-stack-clarity
  - production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability
  - design/gdd/strategic-map
  - design/gdd/tactical-combat
  - design/gdd/faction-unit-rosters
  - design/gdd/intel-resource
approval: approved
---

# Next Implementation Direction Brief — 2026-06-29

## State

`STORY-UX-002` is DONE / merged. Unity PR #105 merged as `6e22e844fba6c8744424d1963f3a6a35ccfb9b2f`; exact-head PR CI and post-merge `main` CI passed.

The immediate EPIC-010 + cross-epic UX/readability repair train is complete. Unity current-task pointer cleanup PR #106 merged as `fda58fe7d880b557357f834d80041b3c39cbce32`; pointer PR CI and post-merge `main` CI passed. There is no current READY / approved Unity implementation story after `STORY-UX-002`.

This brief is not implementation authorization. A next epic/story must be explicitly approved before Codex starts runtime work.

## Viable next directions

1. **Champion Assets / Operations depth** — deepen Champions as strategic legitimacy and force-projection actors: persistent assets, operation slots, one visible non-magical operation, and a costed spend tied to existing resource/command language.
2. **Intel and dirty-information layer** — make Intel less placeholder-like: scouting, forecast/reveal, misinformation, blackmail-style operations, and false certainty hooks without full fog-of-war.
3. **Tactical combat role depth** — build on the now-readable tactical surface with one or two unit-role abilities/counters, clearer AP choices, or morale/cohesion-lite.
4. **Strategic economy/base depth** — extend base/facility choices and external dwellings carefully, without full town-tree sprawl or large-map production complexity.

## Recommended default

Recommend **Champion Assets / Operations depth** as the next epic direction.

Why:

- It strengthens the project pillar that Champions are political/operational actors, not just army tokens.
- It connects naturally to Intel, infrastructure, PR/hearts-and-minds pressure, and command resources without becoming magic.
- It gives the player a new strategic choice layer that can stay small: one asset slot, one operation, one cost, one visible result.
- It differentiates Neon Champions from a generic HoMM-like earlier than another tactical-only mechanics pass.

## Suggested first implementation slice if approved

`STORY-CHAMP-OPS-001 Champion Asset Slot and Prototype Operation On-Ramp`:

- Add a minimal Champion asset/operation presentation model using approved existing Champion/runtime state.
- Show one prototype operation option in the strategic HUD for the active Champion.
- Spend an existing approved resource/command counter; do not invent a new economy.
- Apply a narrow, reversible visible effect such as revealing/forecasting a nearby guarded site or marking a route/site for the current turn.
- Add EditMode + PlayMode evidence and exact-head Unity Foundation CI.

## Approval gate

Human approval recorded 2026-06-29: "Approved". Approved direction: **Champion Assets / Operations depth**. Prepared implementation authority:

- `production/epics/epic-vslice-mvp-011-champion-assets-and-operations-depth.md`
- `production/stories/story-champ-ops-001-champion-asset-slot-and-prototype-operation-on-ramp.md`
- `production/sprints/codex-story-champ-ops-001.prompt.txt`

`STORY-CHAMP-OPS-001` is READY / approved for Unity implementation after the Unity current-task pointer is updated and verified.
