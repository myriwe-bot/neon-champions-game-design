---
title: Tactical Combat — Deferred Items and Open Questions
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-30
updated: 2026-05-30
source_lore: []
related: [design/gdd/tactical-combat, design/research/tactical-combat-deep-reference]
approval: pending
---

# Tactical Combat — Deferred Items and Open Questions

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Stack Action Principle
- Deferred: Elevation / High Ground
- Open Questions

---

## Stack Action Principle

Neon Champions uses HoMM-style stacks as the baseline tactical entities. Each stack acts as one tactical entity.

Example:

- A stack of 8 Corporate Riflemen has 2 AP total.
- The stack may Move + Shoot, Shoot + Shoot, Reload + Shoot, or Overwatch + Defend.
- The stack's size modifies output/survivability, not action count.
- If a Champion grants +1 AP, the same stack can perform a third action this turn.
- Tactical stack-splitting is allowed through army management, but every split consumes one of the 7 active army slots.
- Specific abilities/assets may also create decoys, drone detachments, swarm fragments, Echo projections, or similar exceptions by explicit rule.

This preserves the power fantasy of larger forces while making each additional tactical entity spend real active-army capacity.
## Deferred: Elevation / High Ground

Elevation is not part of MVP.

If revisited later, use a simple abstract rule before considering true vertical maps:

- High-ground tiles may grant +1 range, +damage, or improved hit/graze outcome for ranged attacks.
- Flying/jump units may ignore height penalties.
- Avoid multi-floor interiors and complex vertical pathfinding until proven necessary by playtests.
## Open Questions

| Question | Owner | Deadline | Resolution |
|---|---|---|---|
| Does Move consume AP, or is there separate free movement plus AP? | shared | TBD | Current draft assumes Move costs 1 AP. |
| Which AP abilities belong to Champions versus faction/unit traits? | shared | TBD | Current draft favors Champions/faction identity. |
| How often should normal battles occur on the strategy map? | shared | TBD | Impacts combat complexity budget. |
