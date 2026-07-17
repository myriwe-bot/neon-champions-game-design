---
title: STORY-MAP-VISUAL-SLICE-001 Physical Arctic Adventure Map and Shell Vertical Slice
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-07-17
updated: 2026-07-17
approval: pending
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, design/gdd/strategic-map, design/ux/player-shell, design/art/prototype-visual-target-and-asset-ledger, design/research/physical-adventure-map-direction-2026-07-17, production/playtests/playtest-journal]
---

# STORY-MAP-VISUAL-SLICE-001 Physical Arctic Adventure Map and Shell Vertical Slice

## Status

READY-candidate / implementation approval pending. The physical-adventure-map direction is human-approved, but this exact implementation packet is not runnable until `STORY-STANDALONE-ENTRY-001` is DONE and the human explicitly promotes it.

## Story type

Visual/Feel + UI + Integration spike with a stable replacement boundary.

## Player value

As a player, I need to perceive a frozen physical place, a Champion-led army, recognizable infrastructure, and obvious interaction targets before I read route rules, so I can understand what to inspect and where I can go without decoding a graph.

## Exact complaints preserved

- "There seems to be no interactivity whatsoever."
- "The readability on the map is horrible."
- "I have no idea what do do."
- "The map is very strange and text is unreadable, it is in general a mess."
- The polygons did not communicate what they represented.
- The base could not be opened or upgraded through the discovered path.
- Champion inventory and units/stacks could not be found.
- `Mobility support` was unexplained.
- The visible node-map basis remained a concern.

## Proposed representative slice

Produce one runnable, human-reviewable strategic-map composition using the real current scenario state and unchanged graph rules. It must include:

- one faction base;
- the selected Champion and a small composition-informed entourage;
- two embodied routes;
- one resource/recruitment destination;
- one guarded destination;
- the central White Sky/calibration infrastructure visible as a distant or connected anchor;
- a restrained top bar;
- a persistent Champion/army summary;
- one discoverable base or site selection with contextual action presentation.

The slice is a gate artifact, not permission to reskin the entire map.

## Proposed in scope

- Replace visible polygon/node/graph treatment only inside the representative slice with physical terrain, route, and site grammar.
- Keep node IDs, route IDs, movement legality, costs, interactions, AI, save state, and scenario topology unchanged.
- Use roads/tracks/passes/bridges/sea-air links as physical route embodiments.
- Hide graph lines and node circles in normal play; allow restrained temporary route/reachability overlays on selection.
- Move critical explanatory text onto controlled panels and use contrast-safe hierarchy.
- Expose selected Champion movement and inspectable stack names/counts/role hints without inventing inventory mechanics.
- Make the representative base/site visibly hoverable/selectable and show a relevant context action or denial reason.
- Capture normal, Champion-selected, and base/site-selected 1920x1080 evidence for human review.
- Preserve asset provenance, isolated AI-generated asset rules, and replaceability.

## Proposed out of scope

- Full scenario conversion, square/hex/free movement, terrain costs, pathfinding, province simulation, fog, weather rules, AI redesign, save changes, gameplay balance, new facilities/units/sites, final art, broad onboarding, or tactical changes.
- Treating `region` as permission for colored polygon surfaces.
- Permanent neon graph edges or text labels over uncontrolled terrain.
- Fake inventory or nonfunctional clickable controls.

## Proposed acceptance criteria

- [ ] With overlays off, the screenshot reads first as a physical Arctic place with recognizable base, routes, and sites rather than a graph.
- [ ] Selecting the Champion reveals movement, army stacks, and reachable destinations without permanent map clutter.
- [ ] A new reviewer can identify what can be clicked and can open the representative base/site context without explanation.
- [ ] Critical text meets contrast guardrails and is not placed directly over noisy terrain without backing.
- [ ] Current graph legality, AI, scenario topology, and save state are unchanged.
- [ ] Every non-code asset has compliant provenance and replacement metadata.
- [ ] The human owner gives an explicit APPROVE / REVISE / REJECT visual verdict before any full-map rollout story is formed.

## Ambiguity Check

Status: PASS for candidate review, not implementation authorization. Direction, slice boundary, and exclusions are explicit. Exact art composition remains human-reviewed through the output gate rather than silently scaled.

## Proposed branch / PR

- Branch: `story/STORY-MAP-VISUAL-SLICE-001-physical-arctic-map-shell`
- PR title: `STORY-MAP-VISUAL-SLICE-001 Physical Arctic adventure map and shell slice`
- Prompt: `production/sprints/codex-story-map-visual-slice-001.prompt.txt` remains guarded until explicit promotion.

## Verdict

READY-candidate. Direction approved; exact implementation remains pending and non-runnable.
