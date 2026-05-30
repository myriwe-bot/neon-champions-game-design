---
title: Systems Index
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-22
updated: 2026-05-30
source_lore: []
related: [design/gdd/game-concept, design/gdd/game-pillars, design/gdd/tactical-combat, design/gdd/README]
approval: pending
---

# Systems Index

> Status: Draft. Use for system orientation and planning only; implementation still requires an approved GDD section or READY story.

## Dependency Layers

| Order | System | Layer | Priority | Depends On | Why This Priority | Status | GDD |
|---:|---|---|---|---|---|---|---|
| 1 | Data Registry | Foundation | MVP | None | Prevents inconsistent terms, entities, formulas. | Draft | TBD |
| 2 | Turn / Time Structure | Foundation | MVP | Data Registry | Defines the strategy cadence. | Draft | TBD |
| 3 | Strategic Map | Core | MVP | Turn / Time Structure | Main player decision surface. | Draft | TBD |
| 4 | Site / Infrastructure Control | Core | MVP | Strategic Map | Makes map objectives meaningful. | Draft | TBD |
| 5 | Resources | Core | MVP | Strategic Map, Sites | Drives expansion, tradeoffs, and constraints. | Draft | TBD |
| 5.1 | Intel Resource | Core | MVP | Resources, Champions, Strategic Map, Tactical Combat | Special upgrade resource based on Olden Era Alchemical Dust; required for asset empowerment and later recruitment/operation upgrades. | Draft | design/gdd/intel-resource |
| 6 | Champions | Core | MVP | Strategic Map, Resources | Core identity/commander fantasy. | Draft | TBD |
| 7 | Factions | Core | MVP | Champions, Resources | Differentiates strategies and worldview. | Draft | TBD |
| 7.1 | Faction Unit Rosters | Core | MVP | Factions, Champions, Tactical Combat, Resources | Defines recruitable unit identities and tactical roles for the first campaign. | Draft | design/gdd/faction-unit-rosters |
| 8 | Information / Feed State | Feature | Vertical Slice | Strategic Map | Differentiates the setting from generic strategy. | Draft | TBD |
| 9 | Crisis Clocks | Feature | Vertical Slice | Strategic Map, Sites | Creates campaign pressure and consequences. | Draft | TBD |
| 10 | Tactical Combat | Core | MVP | Champions, Units, Strategic Map, Resources, Intel, UI/HUD | Full tactical battles are required for the intended HoMM-like experience and MVP fun test; MVP complexity is constrained to a readable flat-grid stack battle with simple AP, limited statuses, explicit objectives, and data-driven contracts. | Draft | design/gdd/tactical-combat |
| 11 | UX / HUD | Presentation | MVP | All player-facing MVP systems | Needed for comprehension and playtest. | Draft | TBD |
| 12 | Save / Load | Foundation | Vertical Slice | Data Registry | Needed beyond throwaway prototypes. | Draft | TBD |

## Bottlenecks and Risks

| System | Risk | Mitigation |
|---|---|---|
| Tactical Combat | Could explode scope. | Active GDD now uses a concise first-read contract and keeps long packet history in research reference; build the smallest full tactical battle slice with few unit types, one non-kill objective, simple AP, limited statuses, and data-driven rules. |
| Information / Feed State | Can feel unfair if false info is not source-tagged/counterable. | Use explicit provenance states and verification actions. |
| Champions | Can collapse into generic heroes. | Tie abilities to command, legitimacy, body, interface, death/Echo states. |

## Deferred / Explicitly Out of Scope

No additional global exclusions recorded yet. Individual systems list their own MVP cuts, deferred items, and open questions.
