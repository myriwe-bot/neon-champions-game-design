---
title: Strategic Map Realism Brief
type: planning-brief
status: draft
phase: production
owner: shared
created: 2026-06-25
updated: 2026-06-26
related:
  - design/gdd/strategic-map
  - design/research/homm-like-strategic-map-topology-reference
  - design/research/homm-town-building-reference
  - production/stories/story-army-005-army-recruitment-and-map-readability-repair
approval: design-brief-approved-only
---

# Strategic Map Realism Brief

## Status

DRAFT / design-only. Human direction recorded 2026-06-25: start this brief in parallel with `STORY-ARMY-005`, but do not implement a realistic map replacement inside that repair story.

## Purpose

Define what “move to a more realistic map” means before implementation changes strategic topology, camera rules, terrain, art, or scenario data.

## Current human direction

- The current map cannot be moved and is annoying to focus on a specific area.
- The current UI/readability repair should add panning now.
- A more realistic map should be worked on quite soon, but first as a design brief.

## EPIC-009 planning decisions recorded 2026-06-26

The next preferred epic direction is `Strategic Map Geography, Bases, and Simple Facility Construction`.

Locked decisions:

1. Direction: strategic-map geography/readability plus bases and simple buildings/facilities.
2. Rules posture: visual/geography upgrade over current node-route graph rules; no movement/topology rewrite in this epic.
3. Naming/content posture: scenario-authored and future editor-friendly. Base/town/site names are data/localization keys, not hardcoded canon.
4. Story size: medium-batched.
5. Base facility model: simple build/upgrade during scenario; buildings cost resources.
6. Facility construction timing: one build per base per turn.
7. Base capture: starting bases cannot be captured in this epic.
8. Future map editor posture: data fields plus validation now; no actual editor UI yet.

Reference-game research summary:

- Heroes 3 town halls provide the core income-chain model: Village Hall 500 gold/day, Town Hall 1000/day, City Hall 2000/day, Capitol 4000/day, with escalating costs and prerequisite breadth.
- Heroes 3 creature dwellings provide weekly recruitable growth and upgraded dwellings, but the full seven-tier model is out of scope for the next Neon Champions epic.
- Olden Era confirms the modern HoMM-like pattern of city buildings, recruit/upgrade structures, external dwellings, accumulated dwelling growth, gold-growth buildings such as Bank/Treasury, and editor/custom-object relevance.
- Full research note: `design/research/homm-town-building-reference.md`.

Recommended MVP facility scope:

| Lane | Scope |
| --- | --- |
| Administration / income | Three levels total: basic, mid, high. |
| Recruitment / dwelling | One to two specific dwelling/facility offers per faction. |
| Support / infrastructure | At most one small support facility unless later approved. |

## Questions to answer before implementation

1. Visual vs rules change:
   - Is the next map primarily a more realistic visual presentation over the current node/corridor rules?
   - Or does it change movement/topology rules?

2. Geography fidelity:
   - Should the map visibly evoke Greenland geography/coast/settlement logic?
   - Should real-world geography be abstracted to avoid overcommitting canon or scale?

3. Movement model:
   - Preserve node/corridor movement under the hood?
   - Move to regions/zones?
   - Move to tile/hex/freeform terrain later?

4. HoMM-like strategic readability:
   - Which HoMM3 elements matter most now: roads, towns, dwellings, resource nodes, guarded sites, fog, pickups, or path previews?

5. MVP boundary:
   - What is the first realistic-map slice: visual map replacement, camera/navigation, site layout clarity, or strategic geography rules?

## Non-authority

This brief does not authorize Unity runtime work. A future READY story or epic must define the chosen map direction, source authority, scope, acceptance criteria, and verification requirements.
