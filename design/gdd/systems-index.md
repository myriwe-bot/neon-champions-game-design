     1|---
     2|title: Systems Index
     3|type: system-gdd
     4|status: draft
     5|phase: systems-design
     6|owner: shared
     7|created: 2026-05-22
     8|updated: 2026-05-22
     9|source_lore: []
    10|related: [design/gdd/game-concept, design/gdd/game-pillars]
    11|approval: pending
    12|---
    13|
    14|# Systems Index
    15|
    16|> Status: Draft. Do not use for implementation yet.
    17|
    18|## Dependency Layers
    19|
    20|| Order | System | Layer | Priority | Depends On | Why This Priority | Status | GDD |
    21||---:|---|---|---|---|---|---|---|
    22|| 1 | Data Registry | Foundation | MVP | None | Prevents inconsistent terms, entities, formulas. | Draft | TBD |
    23|| 2 | Turn / Time Structure | Foundation | MVP | Data Registry | Defines the strategy cadence. | Draft | TBD |
    24|| 3 | Strategic Map | Core | MVP | Turn / Time Structure | Main player decision surface. | Draft | TBD |
    25|| 4 | Site / Infrastructure Control | Core | MVP | Strategic Map | Makes map objectives meaningful. | Draft | TBD |
    26|| 5 | Resources | Core | MVP | Strategic Map, Sites | Drives expansion, tradeoffs, and constraints. | Draft | TBD |
    27|| 5.1 | Intel Resource | Core | MVP | Resources, Champions, Strategic Map, Tactical Combat | Special upgrade resource based on Olden Era Alchemical Dust; required for asset empowerment and later recruitment/operation upgrades. | Draft | design/gdd/intel-resource |
    28|| 6 | Champions | Core | MVP | Strategic Map, Resources | Core identity/commander fantasy. | Draft | TBD |
    29|| 7 | Factions | Core | MVP | Champions, Resources | Differentiates strategies and worldview. | Draft | TBD |
| 7.1 | Faction Unit Rosters | Core | MVP | Factions, Champions, Tactical Combat, Resources | Defines recruitable unit identities and tactical roles for the first campaign. | Draft | design/gdd/faction-unit-rosters |
    30|| 8 | Information / Feed State | Feature | Vertical Slice | Strategic Map | Differentiates the setting from generic strategy. | Draft | TBD |
    31|| 9 | Crisis Clocks | Feature | Vertical Slice | Strategic Map, Sites | Creates campaign pressure and consequences. | Draft | TBD |
    32|| 10 | Tactical Combat | Core | MVP | Champions, Units, Strategic Map, Resources | Full tactical battles are required for the intended HoMM-like experience and MVP fun test. | Draft | TBD |
    33|| 11 | UX / HUD | Presentation | MVP | All player-facing MVP systems | Needed for comprehension and playtest. | Draft | TBD |
    34|| 12 | Save / Load | Foundation | Vertical Slice | Data Registry | Needed beyond throwaway prototypes. | Draft | TBD |
    35|
    36|## Bottlenecks and Risks
    37|
    38|| System | Risk | Mitigation |
    39||---|---|---|
    40|| Tactical Combat | Could explode scope. | Build the smallest full tactical battle slice: few unit types, clear grid/arena, basic abilities, and guarded-site integration. |
    41|| Information / Feed State | Can feel unfair if false info is not source-tagged/counterable. | Use explicit provenance states and verification actions. |
    42|| Champions | Can collapse into generic heroes. | Tie abilities to command, legitimacy, body, interface, death/Echo states. |
    43|
    44|## Deferred / Explicitly Out of Scope
    45|
    46|Pending concept approval.
    47|