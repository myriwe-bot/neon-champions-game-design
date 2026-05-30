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

## 9. Open Design Packets

| Packet | Topic | Why It Blocks Implementation |
|---|---|---|
| Packet C | Strategic map topology: node-route vs tile/grid, movement cost, reachability. | Required for movement/domain stories. |
| Packet D | Site and infrastructure states, rewards, ownership, guards. | Required for site interaction and battle trigger stories. |
| Packet E | Resources, Intel, recruitment/reinforcement minimum. | Required for reward and spending loop. |
| Packet F | Champion/army strategic state. | Required for movement, army handoff, losses, and growth. |
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

Next decision packet: **Packet C — Strategic Map Topology**.

It should decide whether the MVP strategic map is:

- node-route graph;
- square/hex tile grid;
- hybrid authored nodes over a visual map;
- or a phased approach.
