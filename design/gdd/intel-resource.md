---
title: Intel Resource System
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-22
updated: 2026-05-30
source_lore: [digital-net, greenland, blue-monday, blue-week]
related: [design/gdd/game-concept, design/gdd/game-pillars, design/gdd/systems-index]
approval: pending
---

# Intel Resource System

> Status: Draft. Direction based on *Heroes of Might and Magic: Olden Era* Alchemical Dust, but translated diegetically into Neon Champions.

## Summary

Intel is Neon Champions' special cross-system upgrade resource. Like Olden Era's Alchemical Dust, it links map exploration, Champion inventory, hub development, ability progression, and asset empowerment. Unlike magic dust, Intel represents actionable secrets: stolen research, blackmail, model leaks, schematics, field reports, proof packets, defectors, and reverse-engineered assets.

> Quick reference — Layer: Core · Priority: MVP/Vertical Slice · Key deps: Strategic Map, Resources, Champions, Hubs, Tactical Combat, Information / Feed State

## Design Reference: Alchemical Dust

Olden Era's Alchemical Dust is acquired by:
- trading rare resources in Alchemical Labs;
- disenchanting items in hero inventory;
- finding it in the wild;
- unlocking certain subskills;
- likely weekly map objects and guarded reward sites, based on community reports.

It is spent on:
- upgrading town dwellings;
- leveling up spells;
- empowering artifacts.

Neon Champions translation:
- Alchemical Labs -> Intel Exchanges / Analysis Cells.
- Disenchanting items -> debriefing, reverse-engineering, burning, or leaking assets.
- Wild pickups -> data caches / field dossiers / dead drops.
- Subskills -> Analyst / Fixer / Signals / HUMINT specializations.
- Dwelling upgrades -> recruitment-site / unit-line upgrades.
- Spell levels -> hack / doctrine / operation levels.
- Artifact empowerment -> asset upgrades.

## Player Fantasy

Intel should feel like turning secrets into operational superiority.

The player should think:
- “I stole their research, so my gear improves.”
- “I burned an asset for what it taught me.”
- “I know how this site works now, so my units can be upgraded.”
- “I can spend this scandal as a weapon, or keep it for development.”

## Core Rules

1. Intel is a strategic resource stored globally by faction, with some Champion-local modifiers and temporary caches.
2. Intel is rarer than Credits/Energy and should not be required for every basic action.
3. Intel has three main sinks:
   - asset/artifact empowerment;
   - doctrine/hack/operation leveling;
   - recruitment-site or elite-unit upgrade.
4. Intel has four main source types:
   - map discovery and guarded data sites;
   - conversion of other rare resources through analysis structures;
   - dismantling / reverse-engineering assets;
   - Champion/faction skills or site control producing recurring Intel.
5. Intel sources must be visible enough that scarcity feels strategic, not arbitrary.
6. Intel spending should create opportunity cost between stronger Champions, stronger troops/sites, and stronger operations.
7. Intel should never be named or presented as magic energy. It is always documents, models, proofs, secrets, schematics, credentials, people, or captured process knowledge.

## Acquisition Modes

| Mode | Olden Era Analogue | Neon Champions Implementation | Renewable? |
|---|---|---|---|
| Data cache | wild dust pile | map pickup, dead drop, black box, leaked archive | No |
| Guarded data site | guarded reward object | server bunker, wrecked convoy, archive, dark-net mirror | Usually no |
| Intel Exchange | Alchemical Lab | trade Compute/Proof/Credits/rare resources for Intel | Yes if inputs renewable |
| Analysis Cell | Alchemical Dust Storage | weekly Intel from controlled analysis site | Yes, weekly |
| Reverse-engineering | disenchant artifact | dismantle asset, burn contact, debrief captured gear | No, converts item to Intel |
| Specialist skill | subskill generation | Analyst/Fixer/Signals Champion produces Intel/day | Yes |
| Tactical outcome | battle reward | capture VIP, hack tactical objective, recover prototype | Event-based |
| Public scandal | unique cyberpunk source | convert Proof/legitimacy win into Intel or damage rival | Event-based |

## Spending Modes

| Sink | Olden Era Analogue | Neon Champions Translation | Notes |
|---|---|---|---|
| Asset empowerment | artifact empowerment | upgrade Champion gear/assets | Core MVP use |
| Operation leveling | spell leveling | upgrade hacks, media ops, legal strikes, climate-system actions | Vertical Slice |
| Recruitment-site upgrade | town dwelling upgrade | upgrade drone depot, clinic, hunter council, merc lodge, animal-control station | Vertical Slice |
| Elite unit unlock | dwelling/unit upgrade | unlock advanced squad variants | Alpha unless MVP needs it |
| Map-layer reveal | none/direct adaptation | reveal hidden Digital-Net/proof/route state | Use sparingly |
| Counter-intel cleanup | none/direct adaptation | remove spoofed/polluted info from region | Supports dirty-info pillar |

## Prototype Values

Use placeholder values until playtested:
- Small cache: 5 Intel.
- Standard guarded cache: 10 Intel.
- Major data vault: 25 Intel.
- Dismantle common asset: 5 Intel.
- Dismantle rare asset: 10 Intel.
- Dismantle elite asset: 20 Intel.
- Basic asset upgrade: 10 Intel.
- Major asset upgrade: 25 Intel.
- Basic operation/hack level-up: 15 Intel.
- Recruitment-site upgrade: 20 Intel.

These are intentionally lower-granularity than Olden Era until the resource economy is proven.

## Tactical Combat Integration

Full tactical battles are in scope.

Intel can enter tactical battles through optional objectives:
- capture a server rack before destroying defenders;
- prevent enemy data wipe for +Intel;
- extract a VIP alive;
- scan prototype units during combat;
- hack a tactical node instead of using an attack action;
- win without using destructive weapons to preserve evidence.

This makes Intel more interesting than post-battle loot and reinforces the cyberpunk theme.

## Edge Cases

| Scenario | Expected Behavior | Rationale |
|---|---|---|
| Player spends all Intel early | Core map remains playable; high-end upgrades slow down | Avoid hard fail through experimentation |
| Player hoards Intel | Unspent Intel has no passive value by default | Encourage use |
| Map lacks recurring Intel | Scenario UI should show it is a scarcity map | Avoid hidden frustration |
| Asset is dismantled | Asset is permanently destroyed unless scenario marks it as recoverable | Preserve opportunity cost |
| Captured Intel exceeds storage cap | No cap in MVP | Avoid bookkeeping until needed |
| Intel from local community | Should require consent/trust, not extraction-only framing | Avoid colonial resource logic |

## Tuning Knobs

| Parameter | Current Value | Safe Range | Effect of Increase | Effect of Decrease |
|---|---:|---:|---|---|
| Basic asset upgrade cost | 10 | 5-20 | Slower Champion growth | Faster experimentation |
| Major asset upgrade cost | 25 | 15-50 | More specialization | More frequent power spikes |
| Analysis Cell weekly yield | 10 | 5-25 | More renewable Intel | More map scarcity |
| Specialist daily yield | 1 | 0-3 | Stronger economy builds | Less snowball |
| Dismantle common asset yield | 5 | 0-10 | More salvage economy | More attachment to assets |

## Acceptance Criteria

- [ ] Intel has at least one map pickup source, one guarded-site source, one conversion source, and one dismantling source in the vertical slice.
- [ ] Intel can upgrade at least one Champion asset in the MVP.
- [ ] Intel costs and rewards are data-driven.
- [ ] Full tactical battles can award Intel through at least one optional objective.
- [ ] UI labels Intel sources as secrets/proofs/research/contacts rather than abstract dust.
- [ ] A player can recover from an early bad Intel spend without campaign failure.

## Open Questions

| Question | Owner | Deadline | Resolution |
|---|---|---|---|
| Should Intel be stored globally, Champion-local, or hybrid? | Human/shared | Before resource implementation | Recommended: global pool plus Champion-local discounts/special caches. |
| Should Intel have subtypes, e.g. HUMINT/SIGINT/Research/Proof? | Human/shared | After MVP | Recommended: no for MVP. |
| Can Intel be traded on markets? | Human/shared | Before economy GDD | Recommended: only through controlled Intel Exchanges, not open market. |
