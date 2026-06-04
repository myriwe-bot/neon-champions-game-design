---
title: Tactical Combat Section Map
type: agent-instructions
status: draft
phase: systems-design
owner: shared
created: 2026-05-30
updated: 2026-05-30
source_lore: []
related:
  [design/gdd/tactical-combat, design/research/tactical-combat-deep-reference]
approval: pending
---

# Tactical Combat Section Map

> Preservation check for the tactical-combat readability refactor. Every original top-level section from the long tactical-combat GDD is mapped to a smaller article below. The deep reference remains available as the raw packet-history backup.

## Coverage Summary

- Original top-level tactical sections mapped: 63
- Unmapped original top-level tactical sections: 0
- Raw backup: [[design/research/tactical-combat-deep-reference]]
- Active overview: [[design/gdd/tactical-combat]]

## Article Map

| Original Section                                          | Split Article                                                      |
| --------------------------------------------------------- | ------------------------------------------------------------------ |
| Summary                                                   | [[design/gdd/tactical-combat/overview-and-scope]]                  |
| Current Design Direction                                  | [[design/gdd/tactical-combat/overview-and-scope]]                  |
| MVP Scope Constraints                                     | [[design/gdd/tactical-combat/overview-and-scope]]                  |
| Tactical Entity Model                                     | [[design/gdd/tactical-combat/overview-and-scope]]                  |
| Army Composition and Battle Participation                 | [[design/gdd/tactical-combat/army-deployment-and-stacks]]          |
| Activation, Initiative, AP, Wait, and Defend              | [[design/gdd/tactical-combat/ap-actions-and-reactions]]            |
| Base Actions                                              | [[design/gdd/tactical-combat/ap-actions-and-reactions]]            |
| Defend / Brace Direction                                  | [[design/gdd/tactical-combat/ap-actions-and-reactions]]            |
| Counterattacks, Zone of Control, and Overwatch            | [[design/gdd/tactical-combat/ap-actions-and-reactions]]            |
| Line of Sight and Cover                                   | [[design/gdd/tactical-combat/targeting-damage-and-defense]]        |
| Range Bands and Minimum Range                             | [[design/gdd/tactical-combat/targeting-damage-and-defense]]        |
| Damage Types, Weapon Tags, and Defense Tags               | [[design/gdd/tactical-combat/targeting-damage-and-defense]]        |
| Status Effect Taxonomy                                    | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Suppression                                               | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Jammed                                                    | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Hacked                                                    | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Marked and Sensor Lock                                    | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Stealth and Reveal                                        | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Smoke and Vision Blocking                                 | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Terrain Hazards                                           | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Forced Movement                                           | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Tactical Objectives and Interactions                      | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Retreat, Surrender, and Tactical Loss Boundary            | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| Morale, Routing, and Stack Collapse                       | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| Global Morale Model                                       | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| Morale Scale, Thresholds, and Rout Checks                 | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| Morale Recovery and Rally Actions                         | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| Morale Event Sources and Strategic Links                  | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| Morale UI, Prediction, and Player Readability             | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| Morale Complexity Boundary and MVP Cut                    | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| End of Morale Block — Integration Check                   | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| Post-Battle Resolution: Outcome Categories                | [[design/gdd/tactical-combat/post-battle-resolution]]              |
| Post-Battle Losses and Preservation                       | [[design/gdd/tactical-combat/post-battle-resolution]]              |
| Post-Battle Rewards and Spoils                            | [[design/gdd/tactical-combat/post-battle-resolution]]              |
| Rare Capture, Resurrection, and Post-Battle Control       | [[design/gdd/tactical-combat/post-battle-resolution]]              |
| Rare Recovery, Resurrection, and Faction Return Mechanics | [[design/gdd/tactical-combat/post-battle-resolution]]              |
| Post-Battle Resolution Summary UI                         | [[design/gdd/tactical-combat/post-battle-resolution]]              |
| Post-Battle Block MVP Cut                                 | [[design/gdd/tactical-combat/post-battle-resolution]]              |
| End of Post-Battle Block — Integration Check              | [[design/gdd/tactical-combat/post-battle-resolution]]              |
| Ammo, Capacity, Cooldowns, and Logistics                  | [[design/gdd/tactical-combat/ammo-capacity-and-logistics]]         |
| Morale / Cohesion                                         | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| Champion Operations and Doctrine                          | [[design/gdd/tactical-combat/champion-operations-and-progression]] |
| Champion Progression Stats                                | [[design/gdd/tactical-combat/champion-operations-and-progression]] |
| AP Abilities Group                                        | [[design/gdd/tactical-combat/champion-operations-and-progression]] |
| Tactical Combat MVP Cut / Implementation Readiness        | [[design/gdd/tactical-combat/implementation-contracts]]            |
| Tactical Implementation Contracts                         | [[design/gdd/tactical-combat/implementation-contracts]]            |
| Ability / Effect Schema Primitives                        | [[design/gdd/tactical-combat/implementation-contracts]]            |
| Status Schema and Resolution                              | [[design/gdd/tactical-combat/implementation-contracts]]            |
| Tactical Information Model                                | [[design/gdd/tactical-combat/implementation-contracts]]            |
| Objective System Schema                                   | [[design/gdd/tactical-combat/implementation-contracts]]            |
| Tactical Data / Save / Replay Contracts                   | [[design/gdd/tactical-combat/implementation-contracts]]            |
| Tactical MVP Content Matrix                               | [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]     |
| MVP Faction Pair Selection Criteria                       | [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]     |
| First MVP Faction Pair Candidates                         | [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]     |
| Working Names for First MVP Faction Pair                  | [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]     |
| Barents Roster Role Skeleton                              | [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]     |
| Barents Unit-Line Skeleton                                | [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]     |
| Barents Unit Stat-Role Profiles                           | [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]     |
| Barents Unit Ability-Slot Contracts                       | [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]     |
| Barents First-Pass Unit Abilities                         | [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]     |
| Stack Action Principle                                    | [[design/gdd/tactical-combat/deferred-and-open-questions]]         |
| Deferred: Elevation / High Ground                         | [[design/gdd/tactical-combat/deferred-and-open-questions]]         |
| Open Questions                                            | [[design/gdd/tactical-combat/deferred-and-open-questions]]         |
