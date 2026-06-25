---
title: Strategic Map Realism Brief
type: planning-brief
status: draft
phase: production
owner: shared
created: 2026-06-25
updated: 2026-06-25
related:
  - design/gdd/strategic-map
  - design/research/homm-like-strategic-map-topology-reference
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
