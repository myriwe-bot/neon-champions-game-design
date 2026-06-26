---
title: HoMM Town Building Reference for Neon Champions Bases
type: research-note
status: draft
phase: production
owner: shared
created: 2026-06-26
updated: 2026-06-26
related:
  - design/gdd/strategic-map
  - production/planning/strategic-map-realism-brief-2026-06-25
source_games:
  - Heroes of Might and Magic III
  - Heroes of Might and Magic: Olden Era
approval: reference-only
---

# HoMM Town Building Reference for Neon Champions Bases

## Purpose

Reference note for the next Neon Champions strategic-map/base epic. It records the external comparison requested before locking the first simple base-facility set.

## Sources checked

- Heroes 3 Wiki / The Lazy: `Town`, `Halls`, `Creature dwelling`, and town pages such as `Castle`, `Rampart`, and `Tower`.
- Heroes of Might and Magic: Olden Era Steam page and Steam news/devlogs/patch notes, especially descriptions of city buildings, recruitment/upgrades, dwellings, Bank/Treasury gold growth, faction Laws, RMG/map objects, and map editor notes.

## Heroes 3: town income chain

Heroes 3 uses a simple but powerful hall progression:

| Hall | Cost | Requirements | Income |
| --- | ---: | --- | ---: |
| Village Hall | N/A | Starting town building | 500 gold/day |
| Town Hall | 2500 gold | Village Hall + Tavern | 1000 gold/day |
| City Hall | 5000 gold | Town Hall + Blacksmith + Mage Guild + Marketplace | 2000 gold/day |
| Capitol | 10000 gold | City Hall + Castle | 4000 gold/day |

Design lessons:

1. The income chain is easy to read: each upgrade is a bigger daily-gold engine.
2. Requirements force breadth before maximum economy; City Hall and Capitol are not just linear money purchases.
3. Capitol is strategically special because it is normally limited to one per kingdom.
4. Halls make towns matter even before full creature recruitment is considered.

## Heroes 3: creature dwellings

Town creature dwellings:

- Unlock recruitable creature lines.
- Produce fixed weekly growth.
- Store unbought creatures in town dwellings, so recruitment can accumulate.
- Have upgraded versions that unlock upgraded creature forms.
- Higher-tier dwellings usually cost more and require earlier buildings or broader town development.

External map dwellings:

- Can be flagged/captured on the adventure map.
- Let visiting heroes recruit creatures.
- In base Heroes 3, external dwelling stock is constrained by weekly growth; in Horn of the Abyss and Olden Era-style handling, external dwelling growth can accumulate over weeks.
- Some high-level external dwellings are guarded by the creatures they provide.
- Capturing some external dwellings can improve growth for matching town dwellings.

Design lessons:

1. Dwellings are both economy and army identity.
2. Recruitment capacity should be separate from recruitment cost.
3. External dwellings give map control value beyond one-shot rewards.
4. Full seven-tier dwelling trees are too large for the next Neon Champions slice.

## Olden Era: relevant modernization signals

Public Olden Era material confirms a similar strategic shape without exposing all final numeric tables:

- Cities allow players to construct buildings, recruit and upgrade units.
- Dwellings exist both in cities and on the strategic map.
- External dwellings stack growth over time, per official FAQ/devlog language.
- Town halls generate faction Law points based on upgrade level, adding a second progression currency/track beyond gold.
- Patch notes mention Bank/Treasury gold-growth display, AI city building construction, hiring costs, city recruitment buildings, and map editor/custom object fixes.
- RMG/devlog material emphasizes authored/controlled object placement, roads, starting cities, external dwellings, and mandatory-content controls.

Design lessons:

1. Keep the H3 town logic, but allow modern data-driven scenario/map-authoring hooks.
2. Buildings may produce more than money; they can produce faction-law/strategic points later.
3. External dwelling accumulation is a good future option, but does not need to be active in the first Neon Champions base story.
4. Editor compatibility should start with definitions/validation, not a full editor UI.

## Neon Champions translation

Approved planning direction for the next epic:

- Use H3 as the hard mechanical reference for income chains, prerequisites, and dwellings.
- Use Olden Era as a modernization reference for accumulated dwellings, faction meta-points, and editor-friendly scenario authoring.
- Implement a tiny base-facility model before any full town tree.
- Starting bases are not capturable in the next epic.
- Facility construction costs resources and is limited to one build per base per turn.
- Income chain target: three levels total — basic, mid, high.
- Recruitment target: one to two faction-specific dwelling/facility offers per faction.
- Map/base/site names are scenario-authored data/localization keys, not hardcoded canon.

## Recommended first Neon Champions facility lanes

| Lane | MVP Purpose | Notes |
| --- | --- | --- |
| Administration / income | Credits income progression | H3 Town Hall → City Hall → Capitol analogue, but capped to three total levels for MVP. |
| Recruitment / dwelling | Unlock 1-2 unit offers per faction | Provides army growth without full 6-7 line rosters. |
| Support / infrastructure | Small utility hook | Candidate: Supply Depot, Sensor Node, Clinic/Repair Ward, or Intel Node. Keep to one support facility in the first implementation unless trivial. |

## Scope guard

Do not import the whole HoMM town system yet. The next Neon Champions epic should not include:

- full seven-tier creature dwelling trees;
- upgraded unit dwellings;
- full Capitol special-case kingdom limit unless later needed;
- marketplace/resource trading;
- siege/capture rules for starting bases;
- actual map editor UI;
- strategic AI building decisions.
