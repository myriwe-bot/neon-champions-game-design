---
title: Strategic Map
type: system-gdd
status: approved
phase: systems-design
owner: shared
created: 2026-05-30
updated: 2026-07-24
source_lore: [greenland, blue-monday, blue-week, white-sky, digital-net]
related:
  [
    design/gdd/game-concept,
    design/gdd/game-pillars,
    design/gdd/systems-index,
    design/gdd/tactical-combat,
    design/gdd/faction-unit-rosters,
    design/gdd/intel-resource,
    design/research/homm-town-building-reference,
  ]
approval: approved
---

# Strategic Map

> Status: Approved. Packet A/B direction is approved as the current MVP target: **C3-H two-faction hotseat strategy MVP**, using a **B1 duel map with B2 race-map pacing**. The sections cited by READY implementation stories are approved implementation sources; future packets still require exact READY stories before implementation.

## 1. Summary

The strategic map is the main HoMM-like decision surface for Neon Champions. The first playable product should prove that the game is not only a tactics demo: factions contest an unnamed fictional Arctic region through Champion movement, site control, resource gains, recruitment/reinforcement, and tactical battles. The region is internally grounded in Greenland research but is not publicly identified as Greenland.

Quick reference:

| Field                | Value                                                                                                                                                  |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Layer                | Core                                                                                                                                                   |
| Priority             | MVP                                                                                                                                                    |
| Player fantasy       | Command a public Champion across a contested cyberpunk Arctic map where infrastructure, routes, guarded sites, and faction pressure shape every fight. |
| MVP target           | C3-H: two-faction local hotseat strategy MVP.                                                                                                          |
| First scenario shape | B1 duel map with B2 pacing: direct contest plus early race for neutral sites/resources before the central clash.                                       |
| Main dependencies    | Data Registry, Turn/Time, Factions, Champions, Resources, Intel, Tactical Combat, UX/HUD.                                                              |
| Main risk            | Building a full strategy game before the core loop is playable.                                                                                        |

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

| Element                         |                             MVP Working Range | Purpose                                                            |
| ------------------------------- | --------------------------------------------: | ------------------------------------------------------------------ |
| Factions                        |                                             2 | Hotseat strategic contest.                                         |
| Champions                       |                                 1 per faction | Keep strategic control readable.                                   |
| Starting hubs                   |                                 1 per faction | Spawn, ownership anchor, possible recruitment/reinforcement point. |
| Neutral sites                   |                                          6-10 | Exploration, resources, recruitment, pacing choices.               |
| Guarded resource sites          |                                           2-3 | Tactical battle entry and resource reward test.                    |
| Recruitment/reinforcement sites |                                           1-2 | Army growth loop.                                                  |
| Central objective site          |                                             1 | Midgame contest and win-pressure anchor.                           |
| Tactical battle types           | Guarded site, faction-vs-faction site contest | Minimum proof that strategy hands off into combat.                 |

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

| Concept        | Static Definition? | Runtime State?     | Notes                                                                                         |
| -------------- | ------------------ | ------------------ | --------------------------------------------------------------------------------------------- |
| Scenario       | Yes                | Yes                | Defines map, factions, starts, sites, objectives; runtime tracks progress.                    |
| Faction        | Yes                | Yes                | Definition owns identity; runtime tracks resources, ownership, controller.                    |
| Controller     | Yes/config         | Runtime assignment | `HumanLocal` for hotseat MVP; future strategic AI should fit without rewriting faction model. |
| Champion       | Yes                | Yes                | Definition owns identity/archetype; runtime tracks position, army, movement, state.           |
| Army           | Possibly template  | Yes                | Runtime stack collection; must hand off to tactical battle.                                   |
| Site           | Yes                | Yes                | Definition owns type/rewards/guards; runtime tracks owner/cleared/visited/state.              |
| Route/Map Link | Yes                | Maybe              | Movement cost/topology.                                                                       |
| Resource       | Yes                | Yes                | Stockpile and rewards.                                                                        |
| BattleSetup    | DTO                | Per battle         | Generated by strategy, consumed by tactics.                                                   |
| BattleResult   | DTO                | Per battle         | Generated by tactics, consumed by strategy.                                                   |

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

Approved direction: use an authored node-route graph for prototype rules, presented over a visual Arctic-region map. Keep the data model abstract enough that a later tile/grid or richer spatial layer is not blocked.

Human correction, 2026-07-24: the authored graph is now a **temporary implementation substrate for the replacement vertical slice**, not an approved final movement model. The completed owner playtest still perceived the shipped surface as “a node and edge graph and very complicated.” The replacement slice may reuse graph legality to avoid rewriting proven domain systems, but permanent route lines/node controls are prohibited and the final graph/grid/freeform decision remains open until the isometric slice proves or disproves the need for richer spatial play.

### 9.1 Human playtest correction: physical corridor adventure map

Human-reaffirmed and sharpened on 2026-07-17 after the current polygon/node presentation blocked playtesting.

`Visual Arctic-region map` does not authorize a colored polygon quilt, permanent node circles, or luminous graph edges as the normal player-facing metaphor. The approved near-term presentation is a physical Arctic adventure map over the hidden authored graph:

1. The player reads continuous elevated or shallow-isometric terrain first and graph rules second.
2. Routes are embodied as roads, ice tracks, bridges, passes, maintenance corridors, coast/sea links, air links, or other believable infrastructure paths.
3. Nodes are embodied as recognizable bases, settlements, resource/recruitment sites, guarded infrastructure, archives, relays, and objective structures.
4. Champion travel may animate continuously along authored route splines while occupancy and legality remain node-route based.
5. Reachability, path cost, ownership, and objective pressure are contextual overlays that recede when not relevant.
6. Regions may remain metadata or optional overlays; physical geography must remain understandable with overlays off.
7. Full square-tile, hex, free-movement, province, terrain-cost, and terrain-pathfinding systems remain deferred.
8. Revisit richer topology only after a successful physical-map playtest proves arbitrary positioning, terrain occupancy, guard radius, or continuous path economy is missing strategic fun.

Research and human evidence: `design/research/physical-adventure-map-direction-2026-07-17.md` and `production/playtests/playtest-journal.md`.

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

| Concept                  | Required Fields / Behavior                                                                                                |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| StrategicNodeDefinition  | stable node ID, node type, display/localization key, presentation position, optional site ID, optional owner/start state. |
| StrategicRouteDefinition | stable route ID, from node ID, to node ID, movement cost, route type, traversal flags/requirements if any.                |
| StrategicMapDefinition   | stable map ID, node list, route list, starting faction placements, optional visual map reference.                         |
| ChampionStrategicState   | champion ID, faction ID, current node ID, movement points/state.                                                          |
| NodeRuntimeState         | owner/control/cleared/visited/guarded state as defined by later site packet.                                              |
| RouteRuntimeState        | open/blocked/contested state if later needed; default route state is open.                                                |

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

## 9.5 Strategic Terrain and Tactical Battle Context Contract

### EPIC-010 Direction: Strategic Terrain as Presentation/Data, Tactical Terrain as Gameplay

Approved direction 2026-06-27: because the next epic introduces terrain, the strategic map should also gain terrain identity. For this epic, strategic terrain is a readable scenario-authored context layer and tactical-layout bridge, not a strategic movement-rule system.

Rules:

1. Strategic map terrain/context tags describe what kind of place a region, node, route, site, or base-adjacent area represents.
2. Terrain/context tags may affect presentation, labels, iconography, evidence/debug output, and tactical layout family selection.
3. Terrain/context tags do **not** add strategic movement costs, movement-type rules, supply/logistics, weather, fog, scouting uncertainty, or strategic AI valuation in EPIC-010.
4. Current node-route movement, route costs, site interaction, objective flow, recruitment, base/facility behavior, and tactical handoff rules remain authoritative unless a later approved story explicitly changes them.
5. Strategic battle context should be data-driven and scenario-authored. Implementation must avoid hardcoded one-off map-to-battle switches.
6. Tactical layout family selection is the first bridge from strategic terrain to tactical play. The tactical board contents themselves are authored by later tactical terrain/layout stories.
7. Terrain/context tags are prototype/scenario metadata, not final canon geography. Labels should remain data/localization-key friendly for future editor workflows.

Prototype terrain/context tag examples:

| Tag | Use | Notes |
| --- | --- | --- |
| `urban_ruins` | ruined settlement / damaged infrastructure | Good for blocked lanes and cover later. |
| `corporate_facility_zone` | corporate campus, logistics compound, or secured worksite | Supports base-adjacent or facility fights. |
| `glacier_road` | open Arctic route / ice-road corridor | Good for exposed route clashes. |
| `data_center_perimeter` | data cache, server yard, sensor perimeter | Natural fit for Intel/data-cache encounters. |
| `white_sky_exposed_plain` | exposed open area under altered sky | Strong readability/lore tag; no weather mechanics yet. |
| `base_outskirts` | approach around owned or contested base | Supports fortified-approach tactical layouts. |
| `infrastructure_hub` | central objective / Treaty-Net / logistics node | Supports objective-heavy battle context. |

Prototype tactical layout family examples:

| Strategic context | Suggested layout family | Initial meaning |
| --- | --- | --- |
| Data cache / data-center perimeter | `server_yard` | Authored tactical layout family for data/cache fights. |
| Base-adjacent site / base outskirts | `fortified_approach` | Defensive approach with deployment clarity. |
| Route or open connector clash | `open_route_clash` | Exposed road/field fight with fewer blockers. |
| Central objective / infrastructure hub | `infrastructure_hub` | Objective-focused tactical layout family. |

Validation implications:

- Unknown terrain/context tag IDs should fail validation or be reported clearly.
- Unknown tactical layout family IDs should fail validation or be reported clearly.
- A battle context may have a default layout family only if the default is authored/data-visible, not a hidden hardcoded fallback.
- Evidence for EPIC-010 stories should show which strategic context selected which tactical layout family.

Explicitly out of scope for EPIC-010 strategic terrain:

- strategic terrain movement costs;
- movement-type modifiers;
- supply/logistics;
- weather/climate simulation;
- fog/stealth/scouting uncertainty;
- strategic AI terrain valuation;
- strategic topology rewrite or tile/hex/freeform movement.

## 10. Site and Infrastructure States

### Packet D Decision: D Hybrid Site Model

Approved direction: use HoMM-like mechanical site categories from Packet D option B, expressed through Neon-flavored infrastructure types from option C. For MVP, site mechanics stay simple and reusable; each site carries theme/type metadata so later systems can add richer infrastructure-specific rules.

This means MVP sites are designed in two layers:

1. **Mechanical category** — what the site does in the rules.
2. **Infrastructure theme/type** — what the place is in the world and UI.

Rules:

1. Every interactive strategic location with gameplay state is a `Site` attached to a strategic node.
2. A site has one primary mechanical category for MVP implementation.
3. A site also has one infrastructure/theme type for fiction, labels, icons, rewards, and later specialization.
4. Site mechanics must be reusable across many themes. Example: a `Resource Site` can be a mine, cold-chain fishery, compute outpost, or salvage cache.
5. MVP implementation must not hardcode one bespoke rule system per infrastructure theme.
6. Site definitions need stable IDs and localization keys.
7. Site runtime state tracks ownership/control/cleared/visited/guarded state separately from the static definition.
8. Site interactions must be previewable before commitment: the player should know whether the site will trigger battle, grant reward, recruit/reinforce, or contest ownership.

MVP mechanical site categories:

| Category             | MVP Purpose                                                                       | Typical Interaction                                                        |
| -------------------- | --------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Start Hub            | Faction anchor, starting position, safe/base identity.                            | Own from scenario start; may support reinforcement/recruitment if enabled. |
| Resource Site        | Provides one-time reward or recurring income, depending on later resource packet. | Defeat guards or control site, then gain/claim resource.                   |
| Recruitment Site     | Adds units/reinforcements to faction/Champion army.                               | Control or visit, then recruit/reinforce within approved limits.           |
| Upgrade / Intel Site | Gives Intel, operation unlock hooks, or asset-upgrade material.                   | Defeat guards/claim site, then gain Intel or upgrade currency.             |
| Neutral Guard Site   | Battle-focused encounter site, usually protecting reward/control.                 | Start tactical battle against neutral guard side.                          |
| Central Objective    | Main contested victory/score/pressure anchor.                                     | Control, hold, contest, or battle for scenario progress.                   |
| One-Shot Visit Site  | Single-use map reward, scouting, event, or utility.                               | Visit once, apply effect, mark visited/consumed.                           |

MVP infrastructure/theme types:

| Theme Type                               | Can Use Categories               | Notes                                                                    |
| ---------------------------------------- | -------------------------------- | ------------------------------------------------------------------------ |
| Mining / Extraction Site                 | Resource, Guard, Objective       | Good for material resources and faction conflict.                        |
| Fishery / Cold-Chain Site                | Resource, Objective, Visit       | Grounds the Arctic regional economy and logistics.                        |
| Sensor / White Sky Node                  | Intel, Objective, Guard, Visit   | Connects climate/geoengineering and information control.                 |
| Clinic / Bodytech Site                   | Recruitment, Upgrade, Visit      | Supports bodies, recovery, legitimacy, later Champion/army consequences. |
| Recruitment Contractor / Local Ally Site | Recruitment, Visit, Guard        | Provides units or reinforcement access without a full town system.       |
| Treaty-Net / Infrastructure Node         | Central Objective, Intel, Guard  | Strong first central-objective candidate.                                |
| Cache / Salvage / Black Site             | Resource, Intel, Guard, One-Shot | Flexible early reward site.                                              |
| Starting Hub                             | Start Hub, Recruitment, Resource | Faction base and scenario anchor.                                        |

MVP site runtime states:

| State                 | Meaning                                                                       | Notes                                                                             |
| --------------------- | ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| Hidden / Undiscovered | Site not yet revealed or not interactable in UI.                              | Optional for first MVP; can be omitted if no fog/scouting yet.                    |
| Revealed              | Site is visible but not necessarily controlled/visited.                       | Default for simple MVP maps.                                                      |
| Guarded               | Site has neutral guards or enemy defenders requiring battle before claim/use. | Generates tactical `BattleSetup`.                                                 |
| Uncontrolled          | Site has no faction owner.                                                    | Common after guards are defeated if control is not automatic.                     |
| Controlled            | Site is owned/controlled by a faction.                                        | Drives ownership, income, recruitment, objective progress.                        |
| Contested             | Site contains or is targeted by opposing faction presence.                    | Can trigger faction-vs-faction battle.                                            |
| Visited / Consumed    | One-shot reward or visit effect has already been used.                        | Prevents repeat farming.                                                          |
| Disabled / Locked     | Site exists but cannot currently be used.                                     | Reserved for future scenario conditions; not needed for first pass unless useful. |

Ownership/control contract draft:

1. Start hubs begin controlled by their assigned faction.
2. Neutral guarded sites begin uncontrolled and guarded.
3. Defeating neutral guards may either immediately control the site or leave it claimable; exact default is a later subdecision if needed.
4. Enemy-controlled sites can be contested by moving an opposing Champion onto/into the site interaction.
5. Site control changes only through explicit site interaction or battle result application.
6. Tactical combat must not directly mutate site state; it returns a `BattleResult`, and the strategic layer applies site consequences.

First scenario site mix target:

| Site                            | Count | Suggested Category/Theme                                        |
| ------------------------------- | ----: | --------------------------------------------------------------- |
| Faction start hubs              |     2 | Start Hub / Starting Hub                                        |
| Early resource sites            |   2-3 | Resource / Mining, Fishery, Cache                               |
| Recruitment/reinforcement sites |   1-2 | Recruitment / Contractor, Clinic, Local Ally                    |
| Intel/upgrade site              |     1 | Upgrade/Intel / Sensor, White Sky Node, Black Site              |
| Central contested site          |     1 | Central Objective / Treaty-Net or White Sky Infrastructure Node |
| Optional one-shot visit sites   |   1-2 | Visit / Cache, Sensor, Local Ally                               |

Out of scope for MVP site model:

- full town building trees;
- deep infrastructure maintenance simulation;
- unique bespoke rules for every infrastructure type;
- diplomacy/consent systems as separate mechanics;
- complex legal/provenance ownership states;
- full fog/feed misinformation around site identity;
- multi-turn construction or upgrades;
- final site editor UX.

## 11. Resources, Intel, and Recruitment/Reinforcement Minimum

### Packet E Decision: D Phased Hybrid Resource Model

Approved direction: use the simple mechanical resource set from Packet E option B for the first hotseat MVP, while keeping resource/theme metadata flexible enough for later infrastructure-flavored resources from option C.

This means the MVP economy has three active strategic resources:

1. **Credits** — payment, recruitment, contracts, and general operational spending.
2. **Materials** — equipment, reinforcement, repair, infrastructure-like growth, and future upgrade hooks.
3. **Intel** — special information power used for upgrade, operation, reveal, or unlock hooks; Intel is not generic money.

Future resource identities such as Compute, Medical Capacity, Energy, Legitimacy, Favors, or White Sky Access may appear as site flavor, tags, reward labels, or future expansion hooks, but they are not separate MVP stockpiles unless a later approved packet promotes them.

Rules:

1. Each faction has its own resource stockpiles.
2. MVP faction stockpiles must include `Credits`, `Materials`, and `Intel`.
3. Resource changes are applied by strategic-layer systems after site interaction, turn income, recruitment, or battle-result resolution.
4. Tactical combat must not directly mutate resource stockpiles; it returns a `BattleResult`, and the strategic layer applies rewards/losses.
5. Resource rewards and costs must be previewable before commitment where practical.
6. Resource definitions need stable IDs and localization keys.
7. Site definitions may carry future-facing economy tags, but MVP rules must ignore unsupported stockpile types rather than creating hidden currencies.

MVP resource roles:

| Resource  | MVP Role                      | Typical Sources                                                               | Typical Sinks                                                                   |
| --------- | ----------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Credits   | Broad spending resource.      | Start hub income, resource sites, one-shot caches, central objective rewards. | Recruitment, reinforcement, basic site actions, future operation costs.         |
| Materials | Growth and recovery resource. | Mining/extraction sites, salvage/black sites, guarded infrastructure sites.   | Reinforcement, equipment/upgrade hooks, future repair/build hooks.              |
| Intel     | Special strategic leverage.   | Sensor/White Sky nodes, Treaty-Net nodes, black sites, objective rewards.     | Upgrade/intel-site effects, reveal/operation hooks, future information actions. |

MVP income/reward contract:

1. The MVP supports both one-time rewards and recurring income, but first implementation stories may start with one-time rewards if recurring-income timing is not yet implemented.
2. Recurring income, when enabled, is evaluated at a deterministic strategic-turn timing selected in the turn/scenario packet.
3. Site definitions declare whether they grant one-time reward, recurring income, both, or neither.
4. One-shot visit sites mark their reward as consumed after successful application.
5. Guarded sites grant rewards only after guards are defeated and the strategic result is applied.
6. Enemy-faction site capture does not duplicate already-consumed one-shot rewards unless a site definition explicitly allows recapture rewards.

Recruitment/reinforcement minimum:

1. MVP recruitment/reinforcement uses predefined unit offers, not full town-building trees.
2. Recruitment Site definitions may expose one or more recruit/reinforcement offers.
3. Offers have stable IDs, unit/stack references, cost in Credits/Materials/Intel as needed, and availability/stock rules.
4. The first implementation may use fixed offers and fixed stock counts.
5. Recruitment adds units to the active Champion's army or faction reserve, depending on the approved Champion/army packet.
6. Reinforcement should be able to restore or add units after losses, but detailed casualty recovery rules are deferred to the Champion/army packet.

Implementation-facing data implications:

| Concept                    | Required Fields / Behavior                                                                |
| -------------------------- | ----------------------------------------------------------------------------------------- |
| ResourceDefinition         | stable resource ID, display/localization key, category, icon/color hint.                  |
| FactionResourceState       | faction ID, resource stockpile values for Credits, Materials, Intel.                      |
| ResourceDelta              | resource ID, signed amount, source reason, preview/apply mode.                            |
| SiteRewardDefinition       | one-time and/or recurring resource deltas, optional Intel reward, consumed/claim rules.   |
| RecruitmentOfferDefinition | stable offer ID, unit/stack reference, resource cost, stock/availability, source site ID. |
| RecruitmentRuntimeState    | remaining stock, claimed/available state, optional refresh timing.                        |

Out of scope for MVP economy:

- full HoMM-style multi-resource economy;
- separate Compute, Energy, Medical, Legitimacy, or Favor stockpiles;
- market exchange/trading;
- loans, debt, subscriptions, or upkeep simulation;
- complex supply chains;
- faction-specific economy rules;
- dynamic pricing;
- full town construction/building trees;
- population/workforce simulation;
- deep Intel operation deck/system.

## 12. Base Facilities and Simple Construction

### EPIC-009 Planning Decision: H3-Inspired Small Base Facility Model

Approved planning direction for the next strategic-map/base epic: add simple, resource-costed base facilities on top of the existing graph-map and site model. This is a production-planning extension to the approved MVP strategic-map GDD; exact implementation still requires a READY child story.

Reference basis:

- `design/research/homm-town-building-reference.md` records the Heroes 3 and Olden Era comparison used for this decision.
- Heroes 3 provides the hard reference shape: town halls produce gold, higher hall levels cost more and require prerequisite buildings, and creature dwellings unlock weekly recruitable growth.
- Olden Era provides modernization signals: cities construct buildings and recruit/upgrade units, external dwellings accumulate growth, faction-law/meta points can be generated by town halls, and map/editor-facing authored content matters.

Locked planning decisions:

1. The next base/building slice should use constructible facilities that cost resources.
2. Facility construction timing is **one build per base per turn**.
3. Starting bases are **not capturable** in the next epic.
4. Base/town/site names are scenario-authored data/localization keys, not hardcoded canon.
5. Future map-editor compatibility begins with data definitions and validation, not editor UI.
6. Income-chain size is **three levels total**: basic, mid, high.
7. Recruitment/dwelling scope is **one to two specific dwelling/facility offers per faction**, not a full per-unit-line town tree.

Base definition contract draft:

| Field | Meaning |
| --- | --- |
| baseId | Stable base definition/runtime reference. |
| nodeId | Strategic graph node hosting the base. |
| owningFactionId | Starting/current owning faction. Starting bases are locked from capture in the next epic. |
| displayNameKey | Scenario-authored localization/display key; no hardcoded town names. |
| visualThemeKey | Scenario-authored presentation theme/icon/map marker. |
| facilitySlots | Optional slot/group data if facilities need layout/category constraints. |
| startingFacilities | Facilities present at scenario start. |
| availableFacilityDefinitions | Facilities this base may construct in this scenario. |

Facility definition contract draft:

| Field | Meaning |
| --- | --- |
| facilityId | Stable facility definition ID. |
| facilityLane | Administration, Recruitment, Support, or future extension. |
| displayNameKey | Scenario-authored localization/display key. |
| level | Facility tier/level where relevant. |
| resourceCost | Credits/Materials/Intel costs; Intel should be rare/special, not generic construction money. |
| prerequisites | Required facilities, base state, faction state, or scenario flags. |
| effects | Income, recruitment offer, reinforcement, Intel hook, visibility hook, or future extension. |
| buildLimit | Whether facility is unique per base, upgrade-exclusive, or repeatable; MVP default is unique/upgrade-exclusive. |

MVP facility lanes:

| Lane | MVP Purpose | Approved Scale |
| --- | --- | --- |
| Administration / income | H3 Town Hall analogue; increases recurring Credits income. | Three levels total: basic, mid, high. |
| Recruitment / dwelling | Unlocks faction-specific recruitable unit offers and limited stock/growth. | One to two specific offers per faction. |
| Support / infrastructure | Small utility hook such as reinforcement, Sensor/Intel, clinic/repair, or supply. | At most one support facility in the first implementation unless explicitly approved. |

Administration/income chain draft:

| Level | Working Role | Effect |
| ---: | --- | --- |
| 1 | Basic base administration | Starting/default small Credits income. |
| 2 | Operations administration | Costs Credits + Materials; increases recurring Credits income; requires level 1. |
| 3 | Regional command / high administration | Higher Credits + Materials cost; increases recurring Credits income; requires level 2 plus one breadth prerequisite if useful for pacing. |

Recruitment/dwelling draft:

1. A recruitment facility unlocks one scenario-authored recruit/reinforcement offer or offer group.
2. The next epic should support one to two specific dwelling/facility offers per faction.
3. Offers use stable IDs, unit references, stock/growth/refresh rules, and resource costs.
4. Recruitment/dwelling stock may refresh on a deterministic turn/round timing; exact timing is story-scoped.
5. Full upgraded-unit dwellings and full 6-7 line town rosters are deferred.

Construction rules draft:

1. Each base may complete at most one facility construction per faction turn.
2. A construction command validates resource costs, prerequisites, base ownership, facility availability, and one-build-per-base timing before applying state.
3. Construction spends resources only on successful apply, not preview.
4. Facility effects must be previewable before construction.
5. Built facilities and remaining build availability are serialized runtime state.
6. Build choices should appear in a base panel/summary; final art and town-screen presentation are not required.

Out of scope for the next base/building epic:

- full Heroes-style town tree;
- full seven-tier dwelling model;
- upgraded unit dwellings;
- marketplace/resource trading;
- one-Capitol-per-kingdom special rule unless later approved;
- starting-base capture/siege;
- garrison management beyond existing Champion/army state;
- actual map editor UI;
- strategic AI construction planning.

## 13. Champion/Army Strategic State and Movement Allowance

### Packet F Decision: D Phased Hybrid Champion Movement Model

Approved direction: implement a HoMM-lite Champion model now, while keeping the data model ready for richer logistics later.

This is a phased hybrid of:

- **B: HoMM-lite now** — Champions have movement points, move along routes with costs, carry one army, and use one major site interaction per turn.
- **C: richer logistics later** — future route types, weather, supply, fatigue, faction modifiers, and movement-type differences should fit without rewriting core Champion/site/faction state.

Rules:

1. Each faction begins the first MVP scenario with one Champion.
2. A Champion belongs to exactly one faction.
3. A Champion occupies exactly one strategic node at a time.
4. A Champion has one attached army for MVP.
5. A Champion has movement points that reset at the start of that Champion's faction turn.
6. Moving along a route spends movement points equal to the route movement cost.
7. A Champion may move through multiple connected nodes in one turn if movement points allow.
8. A Champion cannot move along a route if remaining movement points are below that route's cost, unless a later rule explicitly allows partial/provisional movement.
9. A Champion has one major strategic interaction per turn for MVP.
10. Major strategic interactions include claiming a site, recruiting/reinforcing, collecting a guarded/owned reward, initiating a guarded battle, initiating an enemy-site contest, or using a one-shot visit effect.
11. Previewing movement, site effects, battle risk, and recruitment costs does not consume movement or interaction.
12. Tactical combat must not directly mutate Champion, army, or movement state; it returns a `BattleResult`, and the strategic layer applies consequences.
13. MVP implementation should keep fields for future logistics modifiers, but not implement supply/fatigue/weather as active rules yet.

Champion strategic state minimum:

| Field                        | MVP Meaning                                                           | Future-Proofing Note                                               |
| ---------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------ |
| championId                   | Stable runtime/definition reference.                                  | Supports multiple Champions later.                                 |
| factionId                    | Owning faction.                                                       | Controller remains separate from faction.                          |
| currentNodeId                | Current strategic graph node.                                         | Can later map to tile/region position adapter.                     |
| armyState                    | Attached stack collection.                                            | May later split into reserves/caravans/garrisons.                  |
| movementPointsRemaining      | Remaining movement this turn.                                         | Can later be modified by route/weather/status.                     |
| hasMajorInteractionAvailable | Whether the Champion can still perform a major interaction this turn. | Allows later action systems without hardcoding one action forever. |
| championStatusFlags          | Minimal status flags such as active, defeated, wounded, locked.       | Future logistics/status effects can extend this.                   |

Army strategic state minimum:

1. MVP armies are stack collections attached directly to Champions or defensive site/guard definitions.
2. A Champion army is the source for that faction's tactical battle side unless a specific site/encounter overrides it.
3. Neutral guards may use static army templates from site definitions.
4. Enemy-controlled site defenders may use the occupying/contesting Champion army for MVP; separate garrisons are future scope unless explicitly added later.
5. Battle losses return as stack deltas in `BattleResult` and are applied by the strategic layer.
6. If a Champion's army is defeated, the Champion enters a defeated/wounded/loss state to be finalized in the turn/scenario/victory packet.

Movement and interaction contract:

1. Start of faction turn resets that faction Champion's movement points and major interaction availability.
2. Route movement spends points and updates `currentNodeId` only after validation.
3. Moving onto a node does not automatically claim, recruit, collect, or start battle without an explicit interaction command, unless a later UX decision chooses auto-prompt/auto-trigger behavior.
4. Major site interaction consumes the Champion's major interaction availability.
5. A battle-triggering interaction consumes the major interaction when the battle is launched.
6. After battle, remaining movement may persist if the Champion survives and movement remains, but the major interaction is spent. This can be tuned later if playtests show cleanup movement feels wrong.
7. Recruitment adds to the active Champion army for MVP if the army has capacity and the offer is valid. Faction reserve/caravan recruitment is deferred.

Implementation-facing data implications:

| Concept                | Required Fields / Behavior                                                                                                               |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| ChampionDefinition     | stable champion ID, display/localization key, faction/archetype references, base movement allowance, starting army reference.            |
| ChampionStrategicState | champion ID, faction ID, current node ID, army state reference/value, movement points remaining, interaction availability, status flags. |
| ArmyStackState         | unit definition ID, current count, optional max/cap metadata.                                                                            |
| ArmyState              | owner reference, stack list, validation for empty/defeated state.                                                                        |
| MovementCommand        | champion ID, from node ID, to node ID or route/path, preview/apply mode.                                                                 |
| SiteInteractionCommand | champion ID, site ID, interaction type, preview/apply mode.                                                                              |
| BattleResultArmyDelta  | side/champion/site references, stack losses/survivors, defeated flags.                                                                   |

Out of scope for MVP Champion/army movement:

- multiple Champions per faction;
- freeform movement between nodes;
- strategic tile/hex movement;
- caravans, detached armies, and separate faction reserves;
- full garrison management;
- Champion equipment/progression trees;
- supply, fatigue, weather, route ownership taxes, and logistics attrition;
- faction-specific movement rules;
- complex retreat, capture, resurrection, or hospital systems;
- simultaneous Champion movement;
- strategic AI movement planning.

## 14. Turn/Scenario/Victory Structure

### Packet G Decision: D Phased Hybrid Scenario Structure

Approved direction: implement an objective-duel hotseat structure now, while keeping scenario data ready for later score/race victory modes.

This is a phased hybrid of:

- **B: objective duel now** — fixed alternating faction turns, start-of-turn refresh/income, and victory by defeating the enemy Champion or holding the central objective.
- **C: score/race later** — scenario data may include score values, turn limits, and objective counters, but these are not required active MVP rules unless a later packet promotes them.

Rules:

1. The first MVP scenario has exactly two active factions.
2. Strategic turns are sequential and local hotseat: Faction 1, then Faction 2, repeating.
3. There is no simultaneous turn resolution in MVP.
4. There is no strategic AI controller in MVP.
5. A faction turn begins with a deterministic start-of-turn phase.
6. A faction turn ends when the player manually ends turn, or when a future implementation chooses to auto-end after no legal movement/action remains.
7. The first implementation should support manual end turn as the reliable baseline.
8. Scenario state must track active faction, turn number/round number, objective hold state, victory state, and defeat state.

Start-of-faction-turn sequence:

1. Set active faction/controller.
2. Increment turn/round counters as defined by scenario state.
3. Reset the active Champion's movement points.
4. Reset the active Champion's major interaction availability.
5. Apply recurring income for sites controlled by the active faction, if recurring income is enabled.
6. Evaluate central-objective hold progress for the active faction.
7. Check victory/loss state before allowing actions, so objective wins resolve cleanly.
8. Present start-of-turn summary to the player.

End-of-faction-turn sequence:

1. Validate no modal interaction or battle is unresolved.
2. Apply any end-turn effects approved by scenario rules.
3. Check victory/loss state.
4. Advance active faction to the next faction in turn order.
5. If turn order wraps back to Faction 1, increment the round counter if using round tracking.

MVP victory conditions:

1. **Champion defeat victory** — if a faction's only Champion army is defeated and the Champion enters the approved defeated/loss state, the opposing faction wins unless a later rule explicitly allows recovery.
2. **Central objective hold victory** — if a faction controls the central objective for the required number of its own start-of-turn checks, that faction wins.
3. The working default for the first scenario is holding the central objective for **2 consecutive own turns**.
4. Scenario definitions should store the required hold count rather than hardcoding `2`.
5. If both victory conditions could resolve in one sequence, Champion defeat takes priority immediately after battle; objective hold resolves at start-of-turn checks.

Scenario state minimum:

| Field                  | MVP Meaning                                   | Future-Proofing Note                                |
| ---------------------- | --------------------------------------------- | --------------------------------------------------- |
| scenarioId             | Stable scenario definition reference.         | Supports multiple scenarios/campaign later.         |
| activeFactionId        | Faction whose strategic turn is active.       | Allows hotseat now, future strategic AI later.      |
| turnOrder              | Ordered faction IDs.                          | MVP length is two.                                  |
| turnNumber             | Count of faction turns taken.                 | Useful for logs/replays/tests.                      |
| roundNumber            | Count of full cycles through turn order.      | Useful for future turn limits/scoring.              |
| victoryState           | None, faction win, draw/abort if ever needed. | Must be explicit and serializable.                  |
| centralObjectiveSiteId | Site used for objective hold victory.         | Future scenarios may have multiple objective sites. |
| objectiveHoldFactionId | Faction currently building hold progress.     | Resets when control changes.                        |
| objectiveHoldProgress  | Consecutive own-turn checks held.             | Can generalize into objective score later.          |
| objectiveHoldRequired  | Required hold progress for victory.           | Working default: 2.                                 |

Champion defeat contract:

1. Tactical `BattleResult` reports whether an army was defeated.
2. The strategic layer applies army losses and then evaluates Champion defeat.
3. For MVP, a defeated only-Champion faction loses the scenario.
4. More complex outcomes such as wounded recovery, ransom, clinic revival, backup bodies, retreats, or Echo continuation are deferred.
5. Defeat handling should still use explicit state rather than deleting the Champion from runtime data.

Objective control contract:

1. The central objective is a Site with the Central Objective mechanical category.
2. Site control changes through site interaction or battle-result application.
3. Objective hold progress is checked at the start of the controlling faction's own turn.
4. If another faction controls or contests the objective before the check, prior hold progress resets or transfers according to scenario rules; MVP default is reset.
5. Objective hold progress and reset behavior must be visible in the UI.

Out of scope for MVP turn/scenario/victory:

- online multiplayer;
- simultaneous turns;
- strategic AI turns;
- diplomacy or alliances;
- more than two active factions;
- score-threshold victory as an active rule;
- turn-limit victory as an active rule;
- multiple central objectives;
- campaign persistence across scenarios;
- complex Champion recovery/revival systems;
- hidden victory conditions;
- crisis-clock/endgame systems.

## 15. Strategy-to-Tactical DTOs

### Packet H Decision: D Phased Hybrid Explicit DTO Model

Approved direction: use explicit boundary DTOs for the first implementation, but keep the result payload simpler than a full tactical event stream.

This is a phased hybrid of:

- **B: full explicit DTO now** — `BattleSetup` carries enough context for tactical combat to run without reading or mutating strategic world state; `BattleResult` returns clear outcome data for strategy to apply.
- **C: event stream later** — detailed tactical event logs, replays, morale chains, and granular causal interpretation can be added later without replacing the core setup/result boundary.

Boundary rule:

Tactical combat resolves battles. Strategic systems own world consequences.

Tactical combat may decide:

1. battle winner/loser/no-contest result;
2. surviving unit stacks;
3. unit losses;
4. defeated/routed flags;
5. optional retreat/cancel outcome if supported by the battle mode.

Tactical combat must not directly decide or mutate:

1. site ownership/control;
2. site consumed/visited state;
3. resource stockpiles;
4. recruitment offer state;
5. objective hold progress;
6. Champion movement/interactions beyond returned outcome flags;
7. turn advancement;
8. scenario victory state.

`BattleSetup` minimum:

| Field               | Meaning                                                                             |
| ------------------- | ----------------------------------------------------------------------------------- |
| battleId            | Stable ID for this battle instance.                                                 |
| scenarioId          | Scenario runtime/source reference.                                                  |
| sourceInteractionId | Strategic command/interaction that created the battle.                              |
| sourceSiteId        | Site that triggered the battle, if any.                                             |
| sourceNodeId        | Strategic node where the battle occurs.                                             |
| battleType          | GuardedSite, SiteContest, ChampionVsChampion, or future extension.                  |
| attackingFactionId  | Faction initiating the battle.                                                      |
| defendingFactionId  | Defending faction, neutral faction, or guard-side reference.                        |
| attackingChampionId | Attacking Champion if present.                                                      |
| defendingChampionId | Defending Champion if present; optional for neutral guards.                         |
| attackerController  | Tactical controller for attacking side: HumanLocal or CombatAI.                     |
| defenderController  | Tactical controller for defending side: HumanLocal or CombatAI.                     |
| attackingArmy       | Snapshot/copy of attacking army stacks.                                             |
| defendingArmy       | Snapshot/copy of defending army stacks or guard template.                           |
| tacticalObjectiveId | Tactical battle objective/mode reference.                                           |
| allowedOutcomeFlags | Which outcomes the strategy layer expects, such as canRetreat or canClaimSite.      |
| rewardContextId     | Optional reference to strategic reward context; tactics does not grant it directly. |

`BattleResult` minimum:

| Field                    | Meaning                                                                         |
| ------------------------ | ------------------------------------------------------------------------------- |
| battleId                 | Matches the setup battle ID.                                                    |
| battleOutcome            | AttackerWin, DefenderWin, Retreat, Cancelled, Draw, or Error/Invalid if needed. |
| winningSide              | Attacker, Defender, None.                                                       |
| attackerArmyResult       | Surviving/lost stacks and defeated flag for attacker.                           |
| defenderArmyResult       | Surviving/lost stacks and defeated flag for defender.                           |
| attackerChampionDefeated | Whether the attacking Champion is defeated by battle outcome.                   |
| defenderChampionDefeated | Whether the defending Champion is defeated by battle outcome.                   |
| retreatingSide           | Optional side if retreat exists.                                                |
| tacticalSummary          | Short player-facing summary text/key or structured summary facts.               |
| resultFlags              | Simple flags such as guardsClearedEligible, siteClaimEligible, rewardEligible.  |
| diagnostics              | Optional validation/debug info for tests and agent evidence.                    |

Strategic application contract:

1. The strategy layer creates `BattleSetup` from scenario, Champion, army, site, controller, and interaction state.
2. The tactical layer consumes `BattleSetup` as an input snapshot.
3. The tactical layer returns `BattleResult` without writing strategic runtime state.
4. The strategy layer validates that `BattleResult.battleId` matches an unresolved battle.
5. The strategy layer applies army losses/survivors to Champion or site/guard state.
6. The strategy layer evaluates Champion defeat and scenario loss.
7. The strategy layer applies site control/guard clearing/reward eligibility according to site and scenario rules.
8. The strategy layer applies resource/reward changes.
9. The strategy layer checks victory/loss state after applying battle consequences.
10. The strategy layer emits the player-facing strategic battle summary.

Minimum strategic loop test cases:

1. Guarded resource site creates `BattleSetup` with player Champion army vs neutral guard army.
2. Attacker victory against guards clears guard state and grants/marks eligible reward through strategy application.
3. Defender/guard victory damages or defeats attacking Champion army without granting the reward.
4. Enemy-controlled central objective contest creates faction-vs-faction `BattleSetup`.
5. Battle result can change site control only through strategic application, not tactical mutation.
6. Defeating the enemy only-Champion faction triggers scenario victory through strategy rules.
7. `BattleSetup` preview/generation does not consume site rewards or mutate resources before `BattleResult` is applied.

Out of scope for MVP DTOs:

- full tactical event stream;
- deterministic replay log as a required feature;
- granular per-action tactical audit beyond summary/results;
- multi-side battles beyond attacker/defender;
- diplomacy, alliances, or temporary coalitions;
- complex retreat/capture/ransom systems;
- direct tactical writes into strategic state;
- hidden battle outcome manipulation by feed/misinformation systems.

## 16. Acceptance Criteria Draft

This GDD is implementation-ready only when later packets define enough detail that stories can test:

- [ ] A scenario can initialize two factions, one Champion per faction, starting hubs, neutral sites, resources, and victory conditions.
- [ ] Local hotseat turn order is deterministic and visible.
- [ ] A Champion can move according to approved map topology and movement rules.
- [ ] A Champion can interact with guarded, neutral, owned, and enemy-contested sites.
- [ ] Site interaction can create a tactical `BattleSetup` without mutating strategy state prematurely.
- [ ] Tactical `BattleResult` can update losses, ownership/control, rewards, and victory progress.
- [ ] Resource and recruitment/reinforcement changes are observable and testable.
- [ ] Base facilities can be represented as scenario-authored data with stable IDs, display/localization keys, prerequisites, resource costs, effects, and serialized runtime build state.
- [ ] Facility construction validates one-build-per-base-per-turn, resource costs, prerequisites, and preview/apply separation.
- [ ] The approved three-level administration income chain and one-to-two faction-specific recruitment/dwelling offers per faction can be tested without hardcoded base/town names.
- [ ] All strategic runtime state is serializable.
- [ ] No production story requires strategic AI, networking, simultaneous turns, or unapproved full economy systems.

## 17. Next Step

The strategic-map GDD now has the minimum packet decisions needed to draft first implementation stories.

Next step: create READY-candidate stories for the first strategic MVP slice:

- `STORY-STRAT-001` scenario/map graph state;
- `STORY-STRAT-002` hotseat turn ownership;
- `STORY-STRAT-003` Champion movement;
- `STORY-STRAT-004` site interaction and guarded battle trigger;
- `STORY-TAC-001` battle setup/result DTO contracts;
- `STORY-LOOP-001` playable strategy-to-battle-to-result loop.
