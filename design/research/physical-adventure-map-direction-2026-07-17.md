---
title: Physical Adventure Map Direction Research
aliases: [Physical Corridor Adventure Map Research]
type: reference
status: approved
phase: production
owner: shared
created: 2026-07-17
updated: 2026-07-17
approval: approved
canon: reference
related: [design/gdd/strategic-map, design/art/prototype-visual-target-and-asset-ledger, design/ux/player-shell, production/playtests/playtest-journal, production/epics/epic-018-physical-adventure-map-and-player-entry-recovery]
---

# Physical Adventure Map Direction Research

## Decision supported by this research

Human-approved on 2026-07-17 after the failed `STORY-PROTOTYPE-CONTINUITY-QA-001` playtest:

- Keep the authored node-route graph as the temporary rules substrate.
- Replace its player-facing polygon/node/graph presentation with a physical Arctic adventure map.
- Present roads, ice tracks, bridges, passes, coastlines, sea/air links, bases, and infrastructure sites as the topology.
- Keep nodes and graph edges hidden in normal play.
- Use restrained contextual overlays for selection, route preview, reachability, ownership, and objective pressure.
- Defer full strategic square-tile, hex, free-movement, terrain-pathfinding, and province simulation.
- Prepare one representative human-reviewable map-and-shell vertical slice before scaling the treatment across the whole scenario.

This note records research and rationale. Implementation authority still requires an approved READY story.

## Human evidence that triggered correction

The standalone build showed the Unity splash and then a gray window. In the Unity Editor, the tester could launch only after manually adding `Strategic Map Bootstrap`. The map then blocked further testing:

- "There seems to be no interactivity whatsoever."
- "The readability on the map is horrible."
- "I have no idea what do do."
- "The map is very strange and text is unreadable, it is in general a mess."
- The polygons did not communicate what they represented.
- The base could not be opened or upgraded through the discovered interaction path.
- Champion inventory, units, and stacks could not be found.
- `Mobility support` was visible but unexplained.
- Opponent movement toward nodes after End Turn was visible and understood.
- The visible node-map basis remained an explicit concern.

The closeout verdict is `REJECT`; the experience was not judgeable beyond the limited opponent-movement observation.

## Reference findings

### Heroes of Might and Magic III

Sources:

- <https://heroes.thelazy.net/index.php/Adventure_Map>
- <https://heroes.thelazy.net/index.php/Movement>
- <https://heroes.thelazy.net/index.php/Town>
- <https://heroes.thelazy.net/index.php/Mine>

Useful lessons:

- The simulation uses square tiles, but the player reads a continuous illustrated landscape first.
- Roads, terrain, mountains, water, vegetation, and structures embody corridors and chokepoints.
- Towns, mines, dwellings, treasures, guards, and heroes are recognizable world objects.
- Hero movement, army composition, town anticipation, and site rewards stay coupled to physical place.

A full H3-like tile simulation would additionally require tile occupancy, diagonal movement, terrain costs, blockers, pathfinding, AI valuation, save-state representation, and denser map authoring. Those systems are not required to repair the current presentation failure.

### Heroes of Might and Magic: Olden Era

Source and official screenshots:

- <https://store.steampowered.com/app/3105440/Heroes_of_Might_and_Magic_Olden_Era/>

Useful lessons:

- Official material emphasizes terrain, mountain passes, chokepoints, alternate pathways, towns, structures, and limited movement points.
- Roads and physical barriers communicate meaningful route forks without exposing a graph.
- The selected hero and army remain anchored in a persistent player-facing panel.
- Towns and sites are visual destinations, not labels attached to abstract geometry.

### Songs of Conquest

Sources and official screenshots:

- <https://www.songsofconquest.com/>
- <https://store.steampowered.com/app/867210/Songs_of_Conquest/>

Useful lessons:

- Physical terrain and roads dominate the adventure map.
- Wielder identity, resources, objectives, minimap, and end-turn control remain peripheral and hierarchically separated.
- Detailed text appears contextually rather than being permanently stamped over noisy terrain.
- Settlements and interactables are recognized through silhouette and placement.

### Hero's Hour

Source and official screenshots:

- <https://store.steampowered.com/app/1656780/Heros_Hour/>

Useful lessons:

- A low-budget visual production can still communicate a physical world through biomes, roads, coastlines, towns, mines, objects, and persistent hero/army UI.
- Cheap art is not a reason to expose the topology as a flowchart.
- Dense tiny POIs are an anti-pattern for Neon Champions; silhouette and spacing must remain controlled.

### King's Bounty and Age of Wonders 4

Sources:

- <https://store.steampowered.com/app/25900/Kings_Bounty_The_Legend/>
- <https://store.steampowered.com/app/1135300/Kings_Bounty_II/>
- <https://www.paradoxinteractive.com/games/age-of-wonders-4/about>

Useful boundaries:

- King's Bounty supports visible hero/army continuity and physical exploration, but third-person/free locomotion is too costly and weak for strategic scanning in the current prototype.
- Age of Wonders supports progressive overlays and readable empire state, but a province/4X model would pull Neon Champions away from its Champion-led HoMM-like adventure-map focus.

## Approved player-facing contract

### World first, graph second

The player sees a continuous elevated or shallow-isometric Arctic landscape. The internal graph exists only to resolve legal routes, costs, occupancy, interactions, AI plans, and save state.

### Physical route grammar

Every current graph edge must be representable as a believable corridor such as:

- road or ice road;
- bridge or mountain pass;
- maintenance track or pipeline corridor;
- sea lane or ferry connection;
- air corridor or remote logistics link;
- Treaty-Net or industrial service route.

Permanent luminous graph lines are forbidden in normal play. A selected route may receive a temporary restrained preview.

### Physical site grammar

Current nodes become recognizable locations: bases, settlements, recruitment depots, mines, salvage fields, sensor arrays, archives, data centers, guarded yards, and central White Sky infrastructure. The broad site category should be readable before detailed text is opened.

### No polygon-region substitute

`Region/site map` does not authorize a colored polygon quilt. Regions may exist as scenario metadata or optional overlays, but physical geography must remain understandable with overlays off.

### Interaction and shell

- Champion selection exposes persistent movement and army-stack information.
- Unit name, count, and role are inspectable; unexplained labels such as `Mobility support` require concrete tooltips or removal.
- Bases are dominant landmarks and open through direct selection/Inspect.
- Context actions show relevant legal actions and useful denial reasons rather than a permanent debug wall.
- The first-turn path teaches selection, army inspection, reachable destinations, movement preview, and base opening.

## Deferred topology decision

A hidden square-cell or other richer spatial layer remains a future option. Revisit it only after a successful physical-map playtest identifies arbitrary positioning, terrain occupancy, guard radius, or continuous path economy as missing strategic fun. Do not use a tile/hex rewrite as a substitute for fixing launch, interaction, hierarchy, or visual readability.

## Accessibility guardrails

References:

- <https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html>
- <https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html>

Use at least 4.5:1 contrast for normal text and 3:1 for meaningful non-text UI boundaries as baseline guardrails. Critical explanatory text should use controlled panel backing rather than uncontrolled terrain backgrounds.

## Approval

Approved by the human owner on 2026-07-17. This approval locks the direction and repair sequence; it does not make every later map implementation story READY automatically.
