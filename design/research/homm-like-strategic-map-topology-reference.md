---
title: HoMM-like Strategic Map Topology Reference
aliases: [Strategic Map Topology Reference, Adventure Map Reference]
type: reference
status: draft
phase: pre-production
owner: agent
created: 2026-06-15
updated: 2026-06-15
canon: reference
sources:
  - https://heroes.thelazy.net/index.php/Adventure_Map
  - https://heroes.thelazy.net/index.php/Movement
  - https://heroes.thelazy.net/index.php/Mine
  - https://heroes.thelazy.net/index.php/Wandering_creature
  - https://heroes.thelazy.net/index.php/Combat
  - https://store.steampowered.com/app/3105440/Heroes_of_Might_and_Magic_Olden_Era/
  - https://www.songsofconquest.com/
  - https://store.steampowered.com/app/25900/Kings_Bounty_The_Legend/
  - https://store.steampowered.com/manual/25900
related:
  - design/gdd/strategic-map
  - production/planning/prototype-readability-and-map-next-steps-2026-06-15
---

# HoMM-like Strategic Map Topology Reference

> Reference only. This note captures strategic/adventure-map lessons for the Neon Champions prototype. It does not override the approved MVP strategic-map GDD, which currently authorizes a node-route graph over a visual map.

## Why this note exists

Current prototype feedback: the node-based strategic map works as a proof, but it may not communicate the HoMM-like fantasy strongly enough. The question is whether Neon Champions should move toward a tile, hex, or region-map layer with bases, guarded sites, recruitment, and clearer movement range.

## Source observations

### Heroes of Might and Magic III

Sources:

- Adventure map: <https://heroes.thelazy.net/index.php/Adventure_Map>
- Movement: <https://heroes.thelazy.net/index.php/Movement>
- Mines: <https://heroes.thelazy.net/index.php/Mine>
- Wandering creatures: <https://heroes.thelazy.net/index.php/Wandering_creature>
- Combat: <https://heroes.thelazy.net/index.php/Combat>

Reference pattern:

1. The adventure map is a square-tile strategic board.
2. Movement is tile-to-tile with a daily movement-point budget. The movement page describes heroes moving from tile to tile and needing enough points to move to the next square; diagonal movement costs more than orthogonal movement.
3. Towns are major bases: recruitment, buildings, garrisons, faction identity, economic development.
4. Mines and other adventure objects are capturable or visitable strategic sites.
5. Wandering creatures guard passages, resources, artifacts, mines, and other objects. Guarding is spatial, not just menu gating.
6. Combat transitions to a separate hex battlefield.

Design lesson:

- H3's strategic clarity comes from exact spatial economy: tile reach, routes, road/terrain costs, guarded chokepoints, and capturable production sites.
- The node-route prototype captures site choice but not yet the visual feeling of territory, path cost, guarded space, or base economy.

### Heroes of Might and Magic: Olden Era

Source:

- Steam page and media: <https://store.steampowered.com/app/3105440/Heroes_of_Might_and_Magic_Olden_Era/>

Reference pattern:

1. Olden Era explicitly presents itself as a return to HoMM's turn-based strategy formula.
2. Public page text and media reference exploration, towns, resources, garrisons, world structures, underground layers, map templates/editor, and separate tactical battlefields.
3. Towns construct buildings, recruit/upgrade units, hire heroes, and station garrisons.

Design lesson:

- Modern HoMM-like strategy still expects visible map geography, towns/bases, guarded sites, resource economy, and tactical battle handoff.
- A node graph can be a prototype implementation layer, but the player-facing layer should probably become more map-like.

### Songs of Conquest

Source:

- Official site: <https://www.songsofconquest.com/>

Reference pattern:

1. Official text emphasizes exploring maps with enemies and valuable loot, managing resources, researching advancements, expanding a kingdom, and planning towns.
2. Combat is separate and tactical, with battlefield affordances such as high ground and bottlenecks.
3. The presentation is a modern isometric tile-map style rather than an abstract route diagram.

Design lesson:

- Songs is a useful middle reference: HoMM-like but cleaner and more modern.
- It supports a map that feels spatial without necessarily exposing every old-school movement arithmetic detail.

### King's Bounty: The Legend

Sources:

- Steam page: <https://store.steampowered.com/app/25900/Kings_Bounty_The_Legend/>
- Steam manual: <https://store.steampowered.com/manual/25900>

Reference pattern:

1. King's Bounty uses real-time adventure-map exploration with visible enemies, castles, NPCs, buildings, objects, and portals.
2. Tactical combat happens in separate turn-based arenas.
3. It keeps guarded treasures and recruitment/adventure-site logic without H3's turn-based tile movement economy.

Design lesson:

- This is a useful anti-reference for Neon Champions. It proves guarded sites and tactical handoff do not require a strict tile economy, but it is weaker for deterministic hotseat strategy and movement-range readability.

## Topology options for Neon Champions

### Option A: Keep pure node-route graph

Pros:

- Fastest to author and iterate.
- Current implementation already supports it.
- Good for proving site choice, guarded battles, recruitment, and objective contest.

Cons:

- Reads like a prototype board or flowchart, not a world map.
- Movement range can remain abstract unless heavily dressed up.
- Bases and territory feel weak.

Use if the next goal is still only mechanical loop proof.

### Option B: Region map with embedded sites

Pros:

- Strong middle path from current implementation.
- Sites remain node-like internally, but are placed inside visible regions/territories.
- Supports ownership color, contested regions, routes, weather/terrain labels, and movement pips.
- Easier than full tile pathfinding.

Cons:

- Less precise than H3 tiles.
- Needs careful UI so regions do not become just bigger nodes.

Recommended near-term direction.

### Option C: Square/isometric tile map

Pros:

- Closest to H3/Songs adventure-map grammar.
- Strong for roads, terrain, chokepoints, mines, bases, fog, and map editor aspirations.
- Familiar to HoMM-like players.

Cons:

- Adds pathfinding, terrain-cost UI, diagonal rules, tile occupancy, blocker placement, and much more map-authoring complexity.
- Larger jump from current graph model.

Good later if movement/path economy becomes central to fun.

### Option D: Hex strategic map

Pros:

- Cleaner movement math and range visualization than square diagonals.
- Good for zones, influence, guard radius, and modern strategy readability.
- Could visually harmonize with tactical hexes.

Cons:

- Less HoMM3-authentic than square adventure tiles.
- Bases/roads/buildings can be harder to stage visually than on isometric square maps.

Good if Neon Champions wants a more boardgame/operational feel.

## Recommended phased path

1. Keep the current node-route graph as the rules substrate for the next few stories.
2. Improve the player-facing map into a region/site layer:
   - bases as visible home regions/sites;
   - resource/recruitment/objective sites placed spatially;
   - routes drawn as roads/corridors;
   - reachable area/sites highlighted from movement points;
   - guarded zones clearly marked.
3. Add map data fields that do not block future tile/hex migration:
   - site presentation coordinates;
   - region ID;
   - route type;
   - terrain/theme tag;
   - guard radius / guarded-object link;
   - optional tile/hex anchor fields later.
4. Only promote full square/hex movement after playtests prove the strategic path economy is worth the implementation cost.

## Minimum map readability contract

Before changing topology, the prototype should make these visible:

1. Current faction and active Champion.
2. Remaining movement / reachable sites this turn.
3. Path cost before commitment.
4. Site category: base, resource, recruitment, guarded, objective, cache.
5. Ownership/contested/guarded state.
6. What interaction will happen if clicked: move, battle, recruit, claim, collect, contest, blocked.
7. Battle transition context: why a fight starts and what is at stake.
8. Return summary: losses, rewards, captured site, objective progress.

## Bases and units implication

The next base/unit direction should be deliberately small:

- Bases should become visible home hubs first: spawn, ownership anchor, safe inspection, maybe one fixed reinforcement/recruitment action.
- Do not jump to full HoMM town building trees yet.
- Units need minimal data definitions before real roster variety: display name, stack count, movement, attack range, damage, melee-capable flag, retaliation capability, optional role tag.
- Tactical readability should come before large unit count; many opaque units will make the prototype less readable, not more.
