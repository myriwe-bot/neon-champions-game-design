---
title: Systems Index
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-22
updated: 2026-05-22
source_lore: []
related: [design/gdd/game-concept, design/gdd/game-pillars]
approval: pending
---

# Systems Index

> Status: Draft. Do not use for implementation yet.

## Dependency Layers

| Order | System | Layer | Priority | Depends On | Why This Priority | Status | GDD |
|---:|---|---|---|---|---|---|---|
| 1 | Data Registry | Foundation | MVP | None | Prevents inconsistent terms, entities, formulas. | Draft | TBD |
| 2 | Turn / Time Structure | Foundation | MVP | Data Registry | Defines the strategy cadence. | Draft | TBD |
| 3 | Strategic Map | Core | MVP | Turn / Time Structure | Main player decision surface. | Draft | TBD |
| 4 | Site / Infrastructure Control | Core | MVP | Strategic Map | Makes map objectives meaningful. | Draft | TBD |
| 5 | Resources | Core | MVP | Strategic Map, Sites | Drives expansion, tradeoffs, and constraints. | Draft | TBD |
| 6 | Champions | Core | MVP | Strategic Map, Resources | Core identity/commander fantasy. | Draft | TBD |
| 7 | Factions | Core | MVP | Champions, Resources | Differentiates strategies and worldview. | Draft | TBD |
| 8 | Information / Feed State | Feature | Vertical Slice | Strategic Map | Differentiates the setting from generic strategy. | Draft | TBD |
| 9 | Crisis Clocks | Feature | Vertical Slice | Strategic Map, Sites | Creates campaign pressure and consequences. | Draft | TBD |
| 10 | Tactical Conflict / Combat | Core/Feature | TBD | Champions, Units | Scope must be decided: tactical battles vs abstract resolution. | Draft | TBD |
| 11 | UX / HUD | Presentation | MVP | All player-facing MVP systems | Needed for comprehension and playtest. | Draft | TBD |
| 12 | Save / Load | Foundation | Vertical Slice | Data Registry | Needed beyond throwaway prototypes. | Draft | TBD |

## Bottlenecks and Risks

| System | Risk | Mitigation |
|---|---|---|
| Tactical Conflict / Combat | Could explode scope. | Decide early whether MVP uses abstract, lightweight, or full tactical combat. |
| Information / Feed State | Can feel unfair if false info is not source-tagged/counterable. | Use explicit provenance states and verification actions. |
| Champions | Can collapse into generic heroes. | Tie abilities to command, legitimacy, body, interface, death/Echo states. |

## Deferred / Explicitly Out of Scope

Pending concept approval.
