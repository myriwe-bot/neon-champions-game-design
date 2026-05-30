---
title: Strategic Map
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-30
updated: 2026-05-30
source_lore: [greenland, blue-monday, blue-week, white-sky, digital-net]
related: [design/gdd/game-concept, design/gdd/game-pillars, design/gdd/systems-index, design/gdd/tactical-combat, design/gdd/faction-unit-rosters, design/gdd/intel-resource]
approval: pending
---

# Strategic Map

> Status: Draft. Packet A/B direction is approved as the current MVP target: **C3-H two-faction hotseat strategy MVP**, using a **B1 duel map with B2 race-map pacing**. Further packets must define exact rules before implementation stories become READY.

## 1. Summary

The strategic map is the main HoMM-like decision surface for Neon Champions. The MVP should prove that the game is not only a tactics demo: two factions contest a small Greenland scenario through Champion movement, site control, resource gains, recruitment/reinforcement, and tactical battles.

Quick reference:

| Field | Value |
|---|---|
| Layer | Core |
| Priority | MVP |
| Player fantasy | Command a public Champion across a contested cyberpunk Arctic map where infrastructure, routes, guarded sites, and faction pressure shape every fight. |
| MVP target | C3-H: two-faction local hotseat strategy MVP. |
| First scenario shape | B1 duel map with B2 pacing: direct contest plus early race for neutral sites/resources before the central clash. |
| Main dependencies | Data Registry, Turn/Time, Factions, Champions, Resources, Intel, Tactical Combat, UX/HUD. |
| Main risk | Building a full strategy game before the core loop is playable. |

## 2. Approved MVP Direction

### C3-H: Two-Faction Hotseat Strategy MVP

The MVP target is a real two-faction strategic contest without strategic AI.

Rules:

1. The first playable MVP has two in-world factions in one scenario.
2. Each faction has a local controller. In MVP this means local hotseat control; future controller types may include strategic AI.
3. Each faction begins with one Champion and one army.
4. Factions take sequential strategic turns.
5. The strategic layer supports movement, site interaction, guarded encounters, enemy-faction contesting, resource/reward gains, recruitment or reinforcement, and victory/loss evaluation.
6. Tactical battles are entered from the strategic map and return results back to the strategic layer.
7. Hotseat is local only. No online multiplayer, simultaneous turns, networking, lobbies, accounts, or live-service systems are in MVP scope.
8. Strategic AI is out of scope for the first MVP. Combat AI is in scope because neutral guards and optional AI-controlled battle sides need it.

Design implication:

- **Faction** = in-world side.
- **Controller** = decision-maker for a side, such as `HumanLocal`, future `StrategicAI`, or tactical-only `CombatAI`.
- **Champion** = strategic map actor owned by a faction.
- **Army** = stack collection associated with a Champion or site.
- **BattleSide** = tactical participant generated from strategic state.
- **BattleSideController** = tactical decision-maker, such as `HumanLocal` or `CombatAI`.

## 3. First Scenario Shape

### B1 Duel Map With B2 Pacing

The first scenario should be a compact duel/race map.

Rules:

1. The scenario has two faction starting hubs.
2. The map contains a small number of neutral sites between and around the starts.
3. Early turns should reward racing to useful neutral sites instead of immediately forcing one central fight.
4. Midgame pressure should concentrate around one central objective or high-value infrastructure site.
5. Both factions should have plausible early choices: secure resources, recruit/reinforce, contest the center, or attack the opponent's path.
6. The map should be small enough that playtests reach tactical battles and strategic consequences quickly.

Working first-map content budget:

| Element | MVP Working Range | Purpose |
|---|---:|---|
| Factions | 2 | Hotseat strategic contest. |
| Champions | 1 per faction | Keep strategic control readable. |
| Starting hubs | 1 per faction | Spawn, ownership anchor, possible recruitment/reinforcement point. |
| Neutral sites | 6-10 | Exploration, resources, recruitment, pacing choices. |
| Guarded resource sites | 2-3 | Tactical battle entry and resource reward test. |
| Recruitment/reinforcement sites | 1-2 | Army growth loop. |
| Central objective site | 1 | Midgame contest and win-pressure anchor. |
| Tactical battle types | Guarded site, faction-vs-faction site contest | Minimum proof that strategy hands off into combat. |

## 4. MVP In Scope

- Two factions in one scenario.
- Local hotseat turn order.
- One Champion per faction.
- One active army per Champion.
- Strategic movement across the map.
- Site ownership/control states.
- Guarded neutral sites.
- Enemy-faction contested sites.
- Basic resource stockpiles and rewards.
- Intel as a reward/resource if the required Intel rules are ready; otherwise it may be represented as a locked placeholder with stable ID.
- Basic recruitment or reinforcement path.
- Tactical battle handoff and result application.
- Tactical side controller modes: `HumanLocal` and `CombatAI`.
- Neutral guard combat AI.
- At least one victory condition.
- Serializable scenario runtime state design from the start.

## 5. Explicitly Out of Scope for First MVP

- Online or networked multiplayer.
- Simultaneous turns.
- Strategic AI opponent.
- Full diplomacy.
- Full town/city building tree.
- Deep economy or market simulation.
- Full fog/misinformation/feed-state layer.
- Full crisis-clock system.
- Full campaign persistence across scenarios.
- Map editor.
- Advanced logistics/supply.
- Advanced Champion progression trees.
- Final save/load format, unless separately approved by ADR/story.
- Complex combat AI personalities beyond functional tactical decision-making.

## 6. Core Loop Contract

1. Scenario initializes faction states, Champions, armies, sites, map topology, starting ownership, resources, and victory conditions.
2. Active faction begins its strategic turn.
3. Active faction selects its Champion.
4. Champion moves along the map according to movement rules.
5. Champion interacts with a site.
6. If the site is guarded or enemy-contested, the strategic layer creates a tactical `BattleSetup`.
7. Tactical combat resolves and returns a `BattleResult`.
8. Strategic layer applies the result: losses, site control, rewards, recruitment availability, victory progress, and turn-state changes.
9. Active faction may continue until movement/actions are exhausted or the player ends turn.
10. Turn passes to the next faction.
11. Scenario ends when victory/loss criteria are met.

## 7. Data and State Contract Draft

The exact schemas remain a later packet, but implementation stories should expect these concepts:

| Concept | Static Definition? | Runtime State? | Notes |
|---|---|---|---|
| Scenario | Yes | Yes | Defines map, factions, starts, sites, objectives; runtime tracks progress. |
| Faction | Yes | Yes | Definition owns identity; runtime tracks resources, ownership, controller. |
| Controller | Yes/config | Runtime assignment | `HumanLocal` for hotseat MVP; future strategic AI should fit without rewriting faction model. |
| Champion | Yes | Yes | Definition owns identity/archetype; runtime tracks position, army, movement, state. |
| Army | Possibly template | Yes | Runtime stack collection; must hand off to tactical battle. |
| Site | Yes | Yes | Definition owns type/rewards/guards; runtime tracks owner/cleared/visited/state. |
| Route/Map Link | Yes | Maybe | Movement cost/topology. |
| Resource | Yes | Yes | Stockpile and rewards. |
| BattleSetup | DTO | Per battle | Generated by strategy, consumed by tactics. |
| BattleResult | DTO | Per battle | Generated by tactics, consumed by strategy. |

All runtime state must be serializable even before final save/load format is approved.

## 8. UX / Readability Requirements Draft

The first playable strategic map must make these visible:

- active faction and current controller;
- active Champion;
- movement range or reachable sites;
- site ownership/control/guarded state;
- expected interaction type before committing, such as visit, battle, recruit, collect, or contest;
- resource stockpiles and reward changes;
- whose turn is next;
- victory condition progress;
- clear transition into tactical battle and clear return summary after battle.

## 9. Strategic Map Topology

### Packet C Decision: C/D Hybrid

Approved direction: use an authored node-route graph for MVP rules, presented over a visual Greenland map. Keep the data model abstract enough that a later tile/grid or richer spatial layer is not blocked.

This is a hybrid of:

- **C: authored nodes over visual terrain** — the player sees a geographic/terrain map, but gameplay decisions happen at discrete sites and routes.
- **D: phased node-route now, richer map later** — MVP implementation uses node-route rules first, without pretending this is the final full-vision map model.

Rules:

1. The MVP strategic map is a graph of authored nodes connected by authored routes.
2. Nodes represent meaningful strategic places: hubs, sites, infrastructure, route junctions, objective points, or encounter locations.
3. Routes represent viable travel corridors: roads, ice roads, air/sea links, maintenance corridors, Treaty Net logistics links, or local wilderness paths.
4. The visual layer may draw terrain, geography, coastlines, roads, weather, and infrastructure, but rules read from graph topology unless a later packet promotes richer spatial rules.
5. Movement, reachability, site interaction, and strategic battle triggers operate on node/route state.
6. The graph model must not hardcode a single visual layout. Nodes need stable IDs and map/presentation coordinates.
7. The domain model should distinguish graph rules from presentation coordinates.
8. A future tile/grid/region model should be possible by adding another topology representation or route-generation layer, not by rewriting faction/Champion/site ownership rules.

MVP data implications:

| Concept | Required Fields / Behavior |
|---|---|
| StrategicNodeDefinition | stable node ID, node type, display/localization key, presentation position, optional site ID, optional owner/start state. |
| StrategicRouteDefinition | stable route ID, from node ID, to node ID, movement cost, route type, traversal flags/requirements if any. |
| StrategicMapDefinition | stable map ID, node list, route list, starting faction placements, optional visual map reference. |
| ChampionStrategicState | champion ID, faction ID, current node ID, movement points/state. |
| NodeRuntimeState | owner/control/cleared/visited/guarded state as defined by later site packet. |
| RouteRuntimeState | open/blocked/contested state if later needed; default route state is open. |

MVP movement contract draft:

1. A Champion occupies exactly one strategic node at a time.
2. A Champion moves along connected routes.
3. Route movement cost spends movement points or movement allowance, to be finalized in the Champion/turn packet.
4. MVP does not require free positioning between nodes.
5. MVP does not require continuous pathfinding over terrain.
6. Route blocking, weather, local guide bonuses, and movement-type differences are supported as future route modifiers, not first-pass requirements unless promoted by a later packet.

Why this fits the first scenario:

- B1 duel structure is easy to author as two start hubs connected through neutral site clusters and a central objective.
- B2 race pacing is easy to tune by route costs and site placement.
- Playtests can quickly reveal whether map choices, timing, and tactical handoffs are fun.
- Implementation can start with deterministic pure C# graph logic and simple visual adapters.

Out of scope for MVP topology:

- hex/square strategic tile movement;
- freeform map movement;
- complex terrain pathfinding;
- elevation/terrain simulation;
- procedural map generation;
- route construction/destruction systems;
- final map editor format.

## 10. Open Design Packets

| Packet | Topic | Why It Blocks Implementation |
|---|---|---|
| Packet D | Site and infrastructure states, rewards, ownership, guards. | Required for site interaction and battle trigger stories. |
| Packet E | Resources, Intel, recruitment/reinforcement minimum. | Required for reward and spending loop. |
| Packet F | Champion/army strategic state and movement allowance. | Required for movement, army handoff, losses, and growth. |
| Packet G | Turn/scenario/victory structure. | Required for hotseat and win/loss loop. |
| Packet H | Strategy-to-tactical DTOs. | Required before implementation connects map and combat. |

## 10. Acceptance Criteria Draft

This GDD is implementation-ready only when later packets define enough detail that stories can test:

- [ ] A scenario can initialize two factions, one Champion per faction, starting hubs, neutral sites, resources, and victory conditions.
- [ ] Local hotseat turn order is deterministic and visible.
- [ ] A Champion can move according to approved map topology and movement rules.
- [ ] A Champion can interact with guarded, neutral, owned, and enemy-contested sites.
- [ ] Site interaction can create a tactical `BattleSetup` without mutating strategy state prematurely.
- [ ] Tactical `BattleResult` can update losses, ownership/control, rewards, and victory progress.
- [ ] Resource and recruitment/reinforcement changes are observable and testable.
- [ ] All strategic runtime state is serializable.
- [ ] No production story requires strategic AI, networking, simultaneous turns, or unapproved full economy systems.

## 11. Next Packet

Next decision packet: **Packet D — Site and Infrastructure States**.

It should decide the MVP site model:

- what site categories exist;
- which states a site can be in;
- how ownership/control works;
- how guarded neutral sites differ from enemy-contested sites;
- what rewards and interactions are allowed in the first hotseat scenario.
