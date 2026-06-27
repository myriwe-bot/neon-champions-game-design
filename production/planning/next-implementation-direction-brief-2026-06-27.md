---
title: Next Implementation Direction Brief — 2026-06-27
type: decision-brief
status: superseded
phase: production
owner: shared
created: 2026-06-27
updated: 2026-06-27
related:
  - production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction
  - design/gdd/strategic-map
  - design/gdd/tactical-combat
  - design/gdd/intel-resource
  - design/gdd/faction-unit-rosters
---

# Next Implementation Direction Brief — 2026-06-27

## State

EPIC-009 is DONE / closed. There is no current READY / approved Unity implementation story. This brief is not implementation authorization. A new epic/story must be explicitly approved before Codex starts runtime work.

## Viable next directions

1. **Champion Assets / Operations depth** — deepen Champion identity beyond current Command on-ramp: persistent assets, operation slots, or Champion-specific strategic pressure that can spend Intel/credits without becoming magic.
2. **Intel and dirty-information layer** — make Intel less placeholder-like: scouting/forecast/reveal/blackmail-style operations, false certainty, and asymmetric information hooks.
3. **Tactical combat role depth** — improve tactical differentiation after roster seed: unit abilities, clearer counterplay, AP/Defend extensions, or morale/cohesion.
4. **Strategic economy/base depth** — extend EPIC-009 carefully: more meaningful facility choices, multiple base pressure, or limited external dwellings, without full town-tree sprawl.

## Recommended default

Recommend **Champion Assets / Operations depth** as the next epic direction.

Why:

- It directly supports the project pillar of Champions as legitimacy and force projection.
- It connects to Intel, infrastructure power, and PR/hearts-and-minds warfare without requiring final world map scope.
- It differentiates Neon Champions from a generic HoMM-like by making leaders and assets matter strategically.
- It can be sliced into small implementation stories: data model, one visible operation, one costed spend, one connected smoke.

## Approval gate

Before implementation, human should choose one direction or provide a different one. Then prepare a new epic plus first READY-candidate story and guarded Codex prompt.


## Human decision update — EPIC-010

The initial default recommendation in this brief was superseded by human direction on 2026-06-27. Approved next direction: **Terrain, Tactical Battlefields, and Map-Space Readability**.

Recorded boundary:

- Include strategic-map terrain identity/presentation and tactical-layout-family selection because terrain is being introduced.
- Put real terrain gameplay first on the tactical map: authored layout families, deployment zones, blockers, simple defensive/cover cells, and readability.
- Exclude strategic terrain movement costs, supply/logistics, weather, fog/stealth, strategic AI terrain valuation, and topology rewrites.

Prepared artifacts:

- `production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability.md`
- `production/stories/story-terrain-001-strategic-terrain-tags-and-tactical-layout-family-contract.md`
- `production/sprints/codex-story-terrain-001.prompt.txt` guarded candidate prompt
