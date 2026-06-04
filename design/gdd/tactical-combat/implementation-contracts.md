---
title: Tactical Combat — Implementation Contracts
type: system-gdd
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

# Tactical Combat — Implementation Contracts

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Tactical Combat MVP Cut / Implementation Readiness
- Tactical Implementation Contracts
- Ability / Effect Schema Primitives
- Status Schema and Resolution
- Tactical Information Model
- Objective System Schema
- Tactical Data / Save / Replay Contracts

---

## Tactical Combat MVP Cut / Implementation Readiness

This section defines the first playable tactical slice. The goal is to test whether the core HoMM-like stack combat, AP economy, morale pressure, objectives, deployment, and army-slot constraints work together before expanding into the full tactical vision.

Approved direction:

1. MVP tactical battles include **field battles plus control-zone and extraction/pickup objectives**.
2. MVP status scope includes **all drafted tactical statuses**, implemented in lean, data-driven forms rather than bespoke one-off scripts.
3. Champion/Operation MVP scope uses a **C-to-D path**: the first playable version must include one +AP ability, one Rally/morale ability, and one Signal/Intel ability, while the architecture should support expansion into the full Operation channel system.
4. MVP deployment includes **reorder/formation slots plus scouting preview**.
5. MVP army management includes **7 active slots, duplicate stacks, and stack splitting**.

MVP battle-type contract:

- **Straight field battle** remains the baseline combat test.
- **Control-zone objectives** add positional pressure without requiring full siege/raid systems.
- **Extraction/pickup objectives** test movement, stack splitting, sacrifice, and tiny-stack exploit rules.
- Ambush, siege, raid, multi-stage battles, and highly authored scenario battle types are deferred until the baseline proves stable.

MVP status contract:

- All drafted statuses may appear in MVP, but each status must have:
  - a clear owner/source;
  - visible UI state;
  - deterministic resolution order;
  - bounded duration or clear removal condition;
  - data-driven tuning values.
- Suppressed, Marked/Sensor Lock, and Routed are the minimum readability anchors.
- Jammed, Hacked, morale, network, damage-over-time, disable, and other drafted statuses must not become separate minigames in MVP unless explicitly promoted by a later packet.

Champion / Operation implementation contract:

- First playable tactical Champion/Operation content must include:
  - one **+AP / tempo** ability;
  - one **Rally / morale recovery** ability;
  - one **Signal / Intel** ability.
- These abilities should be authored as early representatives of the broader Operation channel model, not as hardcoded exceptions.
- Full Operation channel breadth is a supported direction, but it should scale after the minimum AP/morale/Signal triad is playable and understandable.

Deployment MVP contract:

- Players can reorder stacks into formation slots before battle.
- Scouting preview can reveal enemy formation/objective information according to scouting/intel rules.
- Full Tactics-skill progression, advanced deployment zones, hidden deployment, decoys, and initiative manipulation remain later-scope unless needed for the MVP slice.

Army-management MVP contract:

- The active army has **7 active slots**.
- Duplicate stacks of the same unit type are allowed if they consume separate active slots.
- Stack splitting is allowed and should be tested early because it interacts with objectives, Zone of Control, retaliation, scouting, and exploit prevention.
- Reserve benches, full garrison logistics, hostile-territory constraints, and storage UX are deferred from the first playable tactical slice.

Implementation readiness gates:

- A battle can be completed with field, control-zone, and extraction/pickup objectives.
- A player can deploy up to 7 active stacks, including duplicate/split stacks.
- Scouting preview affects deployment decisions.
- All MVP statuses have visible icons/tooltips and deterministic turn resolution.
- The AP/morale/Signal ability triad is implemented through a reusable ability/effect framework.
- Tiny-stack objective, ZOC, retaliation, and AP edge cases have automated tests or explicit QA scenarios.

## Tactical Implementation Contracts

This section turns MVP tactical scope into implementation-safe data contracts. The intent is to let the first tactical slice validate design risk while avoiding hardcoded one-offs that would block later Operation, status, and objective expansion.

Approved direction:

1. Abilities are authored as **data-driven ability records using reusable effect primitives and event hooks**.
2. Status effects resolve by **priority tier, then source order inside each tier**.
3. Objectives use **generic objective components plus scenario-specific overrides**.
4. Tactical test content follows a **C-to-D path**: MVP validation requires three core battles plus exploit/regression scenarios, then expands toward a full campaign slice.
5. Operation-channel architecture follows a **C-to-D path**: MVP includes shared ability schema plus channel fields/counterplay hooks, then expands toward the full Operation channel system.

Ability authoring contract:

- Each ability should be represented by a data record, not a bespoke class per ability.
- Ability records should compose reusable primitives such as:
  - grant AP;
  - spend Command/resource;
  - apply status;
  - remove status;
  - modify morale;
  - reveal/mark/sensor-lock;
  - move/push/pull;
  - deal damage;
  - trigger reaction/event hook;
  - check channel/counterplay condition.
- Custom code is allowed for new primitives or hooks, not for every individual ability.
- Ability records must expose tuning values for cost, cooldown, charges, target rules, range, duration, tags/channels, and UI text.

Status resolution contract:

- Statuses resolve in deterministic priority tiers.
- Within the same priority tier, statuses resolve by source/application order.
- Each status must define:
  - priority tier;
  - duration or removal condition;
  - stacking/refresh rule;
  - owner/source;
  - visible UI state;
  - save/load representation;
  - whether it can be cleansed, resisted, suppressed, or countered.
- Resolution order must be testable with explicit regression scenarios for AP grants, morale/rout, Jammed/Hacked/Signal interactions, and death/removal edge cases.

Objective implementation contract:

- Core objective behavior should use reusable components for capture zones, contesting, extraction, pickup, escort/carry, timers, and victory/failure checks.
- Scenario-specific overrides are allowed when a mission needs authored behavior, but overrides must declare which generic rule they replace or extend.
- Objective components must define eligibility rules for tiny/split stacks, summons/decoys/drones/Echo projections, routed units, disabled units, and hidden/scouted units.
- Objective state must be serializable and visible enough for player planning.

MVP tactical validation content:

- Required first validation set:
  - one straight field battle;
  - one control-zone battle;
  - one extraction/pickup battle;
  - exploit/regression scenarios for stack splitting, tiny stacks, Zone of Control, retaliation, AP grants/refunds, objective eligibility, status resolution, and morale/rout.
- After this validation set is stable, expand toward a **full campaign slice** that demonstrates battle selection, army management, deployment, Champion/Operation use, post-battle consequences, and progression context.

Operation-channel architecture contract:

- MVP abilities should use the shared ability schema.
- The schema should include channel fields and counterplay hooks even if most channels are inactive in the first tactical slice.
- Channel/counterplay fields should support later Signal, Covert, Media, Logistics, Fire Support, Medical/Recovery, Psychological Warfare, and faction-specific Operations without rewriting the ability model.
- Full channel breadth is a target state, not a blocker for the first three tactical validation battles.

Implementation readiness gates:

- Designers can author the MVP AP, Rally/morale, and Signal/Intel abilities from data records.
- Status interactions produce deterministic logs suitable for tests/debugging.
- Objective logic can run field, control-zone, and extraction/pickup battles without custom battle-mode classes for each case.
- Regression scenarios cover the known exploit surfaces before the tactical MVP is considered stable.
- The ability schema can represent inactive/future Operation channel metadata without changing save format or ability identity.

## Ability / Effect Schema Primitives

This section defines the minimum reusable ability/effect schema needed for tactical MVP and later Operation-channel expansion. The design should keep ordinary ability authoring data-driven while leaving a path toward deeper rules-engine behavior for rare or full-vision effects.

Approved direction:

1. Base ability structure follows a **C-to-D path**: ability record + trigger conditions + ordered effect blocks + costs/cooldowns now, with a path toward fuller card/stack-like rules behavior later if needed.
2. Effect blocks resolve in **listed order**, but each effect can declare a **timing phase**.
3. Primitive effect set follows a **C-to-D path**: MVP includes the extended primitive set needed for AP, morale, statuses, resources, summoned/created entities, objectives, and reactions, with room to grow toward a larger full-vision library.
4. Targeting follows a **C-to-D path**: MVP uses structured target-query records, with later support for scripted/custom predicates for rare abilities.
5. Future Operation channels follow a **C-to-D path**: ability data includes channel tags, counterplay tags, visibility/noise fields, and later expands toward the full Operation channel subsystem.

Base ability record contract:

- Ability identity:
  - stable id;
  - display name;
  - source type: unit, Champion, faction, objective, asset, scenario, or system;
  - tags/channels;
  - tooltip/UX text;
  - animation/VFX/SFX hooks.
- Conditions:
  - trigger condition: active use, passive, on turn start, on turn end, on kill, on damaged, on routed, on objective event, on status event, etc.;
  - target query;
  - source eligibility;
  - battle/objective/scenario restrictions;
  - channel/counterplay conditions.
- Costs and limits:
  - AP cost;
  - Command/resource cost;
  - cooldown;
  - charges;
  - per-turn/per-battle caps;
  - once-per-stack/per-source restrictions where needed.
- Effects:
  - ordered effect blocks;
  - optional timing phase per block;
  - rollback/fizzle behavior if a block fails;
  - logging/debug metadata.

Effect resolution contract:

- Effects resolve in listed order by default.
- Each effect block may declare a timing phase, such as pre-cost, cost, targeting, pre-effect, main effect, post-effect, reaction, cleanup, or objective check.
- Timing phases are deterministic and inspectable in combat logs.
- Interrupts/reactions should be represented through declared hooks and reaction phases, not arbitrary hidden execution.
- Full event-queue/interrupt-stack behavior is deferred unless later complexity proves it necessary.

MVP primitive effect set:

- Required primitive categories:
  - damage / healing / recovery;
  - grant/spend/refund AP;
  - modify morale / trigger Rally / affect rout state;
  - apply/remove/refresh status;
  - reveal, mark, sensor-lock, hide, or alter visibility;
  - move, push, pull, reposition, or restrict movement;
  - spend/refund Command or other tactical resources;
  - summon/create temporary entity, drone, decoy, Echo projection, mine, turret, relay, or similar explicitly authored entity;
  - objective interaction: pickup, drop, carry, contest, capture, extract, score progress, reset progress;
  - trigger reaction/event hook.
- The full-vision primitive library can expand later, but new primitives should be justified by multiple abilities or a signature faction/system need.

Targeting contract:

- MVP targeting uses structured target-query records rather than hardcoded per-ability targeting.
- Query fields should support:
  - side: self, ally, enemy, neutral, any;
  - target type: stack, Champion, tile, objective, created entity, drone, decoy, Echo projection, terrain feature;
  - range and distance metric;
  - line of sight / line of effect requirements;
  - status filters;
  - AP/morale/rout filters;
  - size/stack-count filters where needed for tiny-stack and split-stack rules;
  - objective eligibility filters;
  - visibility/scouting filters;
  - channel/counterplay filters.
- Later scripted predicates may be added for rare abilities, but the default authoring path should remain query composition, not arbitrary scripts.

Operation metadata contract:

- Ability records should include future-facing Operation metadata even when most Operation channels are inactive in MVP:
  - operation/channel tags;
  - counterplay tags;
  - visibility/noise profile;
  - traceability/detectability;
  - jamming/hacking/interference hooks;
  - UI disclosure level;
  - faction or Champion doctrine tags.
- These fields should not force full Operation-channel simulation in the first playable slice.
- They should prevent schema churn when the design expands from the AP/morale/Signal triad into broader Operations.

Implementation readiness gates:

- The MVP +AP, Rally/morale, and Signal/Intel abilities can be authored as data records using this schema.
- At least one objective interaction uses ability/effect primitives rather than custom battle code.
- Combat logs can show trigger, targeting, cost, effect order, status application, reaction, and cleanup.
- Save/load preserves stable ability ids, status ids, cooldowns, charges, channel metadata, and created-entity ownership.
- Regression tests cover effect ordering, fizzle behavior, AP caps/refunds, target filters, status priority, and objective eligibility.

## Status Schema and Resolution

This section defines the minimum status-effect contract for deterministic tactical play while preserving Neon Champions' emphasis on Signal, deception, hidden information, morale, hacking, and counterplay.

Approved direction:

1. Base status structure uses **status id + duration/removal + priority tier + stacking rule + owner/source + visible UI**.
2. Stacking uses **per-status stacking modes**: refresh, replace-if-stronger, stack count, unique-per-source, or similar bounded modes.
3. Status visibility uses a **full fog-of-war / information model**, because hidden state, deception, scouting, and Signal/Intel are core to the game.
4. Cleanse/resist/counterplay uses **typed counterplay tags**: cleanse, resist, immunity, suppression, jamming, hacking, morale recovery, etc.
5. MVP status resolution requires at least the full tactical phase set: battle start, turn start, pre-action, on-hit/on-damage, post-action, objective check, morale/rout check, death/removal, and turn end.

Base status record contract:

- Identity:
  - stable status id;
  - display name;
  - status family/category;
  - tooltip/UX text;
  - icon/VFX/SFX hooks.
- State:
  - duration or removal condition;
  - priority tier;
  - resolution phase hooks;
  - stacking mode;
  - owner/source;
  - target entity;
  - intensity/count/value fields if applicable.
- Rules:
  - effect primitives or modifiers applied by the status;
  - refresh/replace/expire behavior;
  - cleanse/resist/immunity/counterplay tags;
  - save/load representation;
  - combat log visibility.
- Presentation:
  - visibility level by observer;
  - UI disclosure rules;
  - revealed/identified/decoded state;
  - preview text for known effects and uncertainty text for unknown effects.

Stacking contract:

- Each status declares one bounded stacking mode rather than freeform stacking code.
- Required stacking modes:
  - **refresh** — reapplication extends or resets duration;
  - **replace-if-stronger** — stronger application replaces weaker application;
  - **stack count** — applications increment a capped count/intensity;
  - **unique-per-source** — separate instances can coexist only if their source differs;
  - **non-stacking** — reapplication has no effect or only updates source metadata.
- Each status must declare maximum stack count/intensity where relevant.
- Stacking behavior must be visible or explainable enough that players can predict important outcomes.

Information / visibility contract:

- Status visibility is part of the tactical information model, not just UI polish.
- A status may have different disclosure levels for owner, opponent, neutral observer, scouted observer, and revealed/decoded observer.
- Required visibility states:
  - public and fully identified;
  - visible but values/remaining duration hidden;
  - owner-only;
  - hidden until triggered;
  - suspected/anomaly state;
  - scouted/revealed/decoded;
  - false/decoy status if later deception systems require it.
- Signal, Intel, scouting, jamming, hacking, stealth, and Media/Psychological effects may alter what status information is visible.
- Hidden statuses still need deterministic server/simulation state and replay/debug visibility for QA.
- The player-facing model must avoid unfairness: hidden status effects should be either inferable, scoutable, or deliberately framed as deception/uncertainty.

Counterplay contract:

- Statuses declare typed counterplay tags instead of bespoke hardcoded counter rules.
- Required counterplay tags include:
  - cleanse;
  - resist;
  - immunity;
  - suppression;
  - jamming;
  - hacking;
  - morale recovery;
  - reveal/decode;
  - dispel/remove;
  - armor/biotech/network/firewall/faction-specific resistance tags as needed.
- Abilities, faction traits, Champion skills, and Operations can reference these tags for broad counterplay.
- Counterplay should distinguish prevention, mitigation, removal, concealment, and information revelation.

Resolution phase contract:

- MVP status hooks must support at least:
  - battle start;
  - turn start;
  - pre-action;
  - on-hit / on-damage;
  - post-action;
  - objective check;
  - morale/rout check;
  - death/removal;
  - turn end.
- Within a phase, statuses resolve by priority tier, then source/application order.
- Status resolution should produce deterministic combat log entries, including hidden debug logs for QA/replay when player-facing information is concealed.
- Arbitrary hook/event-queue behavior is deferred until the bounded phase model fails a real design need.

Implementation readiness gates:

- Suppressed, Marked/Sensor Lock, Routed, Jammed, Hacked, morale modifiers, and objective-affecting statuses can all be represented by the status schema.
- Status stacking behavior is testable per status mode.
- Hidden/partial status information can be represented separately from true simulation state.
- Cleanse/resist/counterplay abilities can target status tags instead of specific status ids only.
- Automated or explicit QA scenarios cover phase order, hidden visibility, reveal/decode, cleanse/removal, stacking, rout/death interactions, and save/load.

## Tactical Information Model

This section defines how hidden, partial, suspected, false, and revealed tactical information works. The goal is to support Signal/Intel, scouting, deception, hidden statuses, traps, mines, created entities, and later Operation-channel play without making tactical outcomes feel arbitrary.

Approved direction:

1. MVP information states use the **full layered model**: true state, observed state, suspected state, false/decoy state, and revealed/decoded state.
2. Tactical object coverage follows a **C-to-D path**: MVP applies the information model to statuses, hidden units, objectives, traps/mines, and created entities, then expands toward all tactical objects including abilities, intent, cooldowns, resources, channels, and objective rules.
3. Suspected/anomaly information uses **type family, confidence, and last-known location/turn**.
4. False/decoy information can mimic known object categories but must have discoverability and counterplay rules.
5. Debug/replay follows a **C-to-D path** now, with full timeline inspector as the eventual target: MVP needs player-visible, opponent-visible, and all-truth debug modes; later tooling should inspect visibility-state changes per observer over time.

Information-state contract:

- **True state** — authoritative simulation state used by rules, tests, save/load, and all-truth debug tools.
- **Observed state** — what a given observer currently knows and can act on.
- **Suspected state** — incomplete information that marks an anomaly, likely object, or last-known fact without confirming exact details.
- **False/decoy state** — deliberately misleading information created by abilities, decoys, spoofing, stealth, Media/Psychological effects, or scenario rules.
- **Revealed/decoded state** — information promoted from hidden/suspected/false/partial into confirmed knowledge by scouting, Signal, Intel, detection, hacking, or scripted reveal.

Object coverage contract:

- MVP information-model objects include:
  - hidden or partially identified statuses;
  - hidden units/stacks;
  - objectives and objective state where uncertainty is intended;
  - traps, mines, relays, sensors, turrets, drones, Echo projections, decoys, and other created entities;
  - pickup/extraction objects if scenario rules hide, mask, or misidentify them.
- Full-vision expansion may include:
  - ability intent;
  - cooldowns and charges;
  - tactical resources;
  - Operation channels;
  - counterplay hooks;
  - objective rules;
  - hidden faction/Champion traits;
  - AI plans or predicted actions where appropriate.
- The design default is not "hide everything." Hidden information must create meaningful decisions, not random punishment.

Suspected/anomaly contract:

- Suspected information should carry:
  - type family, such as unit, status, trap, mine, objective, signal source, relay, decoy, or unknown anomaly;
  - confidence level;
  - last-known location or affected entity;
  - last-known turn/phase;
  - source of suspicion, such as scouting, sensor ping, attack trace, movement noise, objective interaction, or counterintel warning.
- Suspected markers should be readable enough to support planning but incomplete enough to preserve uncertainty.
- Confidence should be discrete/bounded for MVP, not a deep probabilistic belief simulation.

False/decoy contract:

- Decoys and false information may mimic known categories such as units, statuses, objectives, mines, relays, signals, or created entities.
- Each false/decoy object must declare:
  - what category it mimics;
  - what observers can see;
  - what interactions reveal, decode, or disprove it;
  - whether it can block movement, contest objectives, draw attacks, trigger reactions, or only mislead UI/targeting;
  - what happens when revealed or destroyed.
- Decoy gameplay must remain counterplayable through scouting, Signal/Intel, proximity, attacks, reveal effects, or faction-specific counters.
- False information should be used as a signature tactical layer, not as constant UI noise.

Debug / replay contract:

- MVP replay/debug modes must include:
  - player-visible view;
  - opponent-visible view;
  - all-truth debug view.
- Later tooling should expand into a timeline inspector that shows visibility-state changes per observer, including when information became suspected, observed, false, revealed, decoded, expired, or invalidated.
- Hidden-state bugs are high risk; every hidden/false/revealed transition should be loggable with true-state and observer-state records.
- QA needs all-truth visibility even when normal replays preserve player-facing uncertainty.

Implementation readiness gates:

- A hidden status, suspected trap/mine, hidden unit, decoy entity, and revealed objective state can all be represented without bespoke per-case UI state.
- Scouting/Signal/Intel effects can promote information from hidden/suspected/false/partial to revealed/decoded.
- False/decoy objects have explicit reveal and counterplay rules.
- Combat logs/replay can display player-visible, opponent-visible, and all-truth views.
- The model avoids unfair hidden outcomes by ensuring major hidden threats are inferable, scoutable, revealable, or deliberately framed as deception.

## Objective System Schema

This section defines objective components so field battles, control zones, extraction/pickup missions, exploit tests, and later campaign-slice objectives do not become isolated custom scripts.

Approved direction:

1. Base objective structure follows a **C-to-D path**: objective id + component list + state machine + victory/failure conditions + UI/logging now, with a path toward fuller mission scripting if campaign-slice needs justify it.
2. Reusable objective components follow a **C-to-D path**: MVP includes capture zones, extraction points, pickup/carry, timers, contesting, score/progress, ownership, and eligibility filters; later expands toward escort, sabotage, defense waves, multi-stage missions, and branching outcomes.
3. Objective eligibility uses **eligibility query records** with stack size, unit type, status, routed/disabled state, created-entity type, visibility, and faction/objective tags.
4. Scenario-specific overrides are allowed only as **declared overrides/extensions of generic components**.
5. Objective information visibility follows a **C-to-D path**: objective existence, state, and rules have separate visibility levels now, with later support for false objectives, hidden objectives, spoofed progress, and masked rules.

Base objective record contract:

- Identity:
  - stable objective id;
  - display name;
  - objective family: field battle, capture/control, extraction, pickup/carry, survival, elimination, scenario, etc.;
  - scenario/map owner;
  - UI/logging text.
- Components:
  - reusable objective components;
  - eligibility queries;
  - progress/scoring rules;
  - visibility rules;
  - reward/consequence hooks.
- State machine:
  - inactive;
  - active;
  - contested;
  - progressing;
  - completed;
  - failed;
  - expired;
  - revealed/decoded if hidden information applies.
- Outcomes:
  - victory conditions;
  - failure conditions;
  - partial-success conditions if later scenario design needs them;
  - post-battle consequence hooks.

MVP reusable component set:

- **Capture/control zone** — tracks eligible units contesting or controlling an area.
- **Extraction point** — checks whether eligible entities exit, survive, or deliver carried objects.
- **Pickup/carry object** — supports pickup, drop, transfer if allowed, carrier death/drop behavior, and extraction delivery.
- **Timer** — turn/round/phase counters for deadlines, escalation, scoring, or expiry.
- **Contesting** — determines how opposing eligible entities pause, reverse, or block progress.
- **Score/progress** — supports accumulated progress, threshold completion, per-turn scoring, and reset/decay rules.
- **Ownership/control** — tracks faction/side/controller and transfer rules.
- **Eligibility filter** — queries which stacks/entities can interact, contest, carry, score, or extract.

Full-vision component expansion may include escort, sabotage, defense waves, multi-stage objectives, branching outcomes, deception objectives, scripted campaign consequences, and special scenario setpieces.

Eligibility contract:

- Objective eligibility is data-driven through query records, not hardcoded per objective.
- Query fields should support:
  - stack size / tiny-stack thresholds;
  - unit type and unit tags;
  - Champion, stack, drone, decoy, Echo projection, summoned/created entity, relay, mine, turret, or objective object;
  - routed, disabled, suppressed, jammed, hidden, revealed, or other status filters;
  - visibility/scouting state;
  - faction/side/controller;
  - objective-specific tags such as can-carry, can-contest, can-score, can-extract, can-trigger, can-block.
- Eligibility rules must explicitly handle split stacks and created entities because they are high-risk exploit surfaces.

Scenario override contract:

- Scenario-specific behavior is allowed only as a declared override or extension of a generic component.
- Each override must declare:
  - the generic component it modifies;
  - which rule is replaced or extended;
  - why generic behavior is insufficient;
  - visibility/logging behavior;
  - test or QA scenario coverage.
- Overrides should be rare for MVP validation battles and more common only in authored campaign-slice missions.
- Custom scripts must not silently bypass eligibility, visibility, objective-state, or logging contracts.

Objective visibility contract:

- Objective information has separable visibility layers:
  - existence: whether the player knows an objective exists;
  - location: where the objective is;
  - state/progress: current control, progress, timer, carrier, or contested state;
  - rules: how the objective scores, fails, or can be interacted with;
  - reward/consequence: what happens after completion or failure.
- MVP should support hidden or partial objective information when tied to scouting, Signal/Intel, deception, or scenario design.
- Full-vision expansion may support false objectives, hidden objectives, spoofed progress, masked rules, and decoy pickups, but each must have discoverability and counterplay.

Implementation readiness gates:

- Field battle, control-zone, and extraction/pickup objectives can be built from the objective schema.
- Tiny-stack, split-stack, routed, disabled, hidden, decoy, drone, and Echo-projection eligibility are all explicit and testable.
- Objective progress and contesting are deterministic and loggable.
- Objective visibility integrates with the tactical information model.
- Scenario overrides cannot bypass generic component contracts without declaring and testing the exception.

## Tactical Data / Save / Replay Contracts

This section defines what tactical state must be serializable, replayable, and testable so hidden information, statuses, objectives, ability effects, and AP/morale/Signal interactions remain debuggable.

Approved direction:

1. Tactical MVP save granularity is **battle start, turn boundaries, and after each stack activation**.
2. MVP replay model stores **initial state + player commands + RNG seeds + periodic checkpoints**.
3. Hidden-information save state follows a **C-to-D path**: true state + observer-visible states + suspected/false/revealed metadata now, with full visibility timeline per observer later.
4. Combat log detail follows a **C-to-D path**: structured logs now, expanding toward full causal event graphs as tooling matures.
5. Schema/versioning follows a **C-to-D path**: stable ids + schema version fields + migration hooks now, with a fuller formal migration framework later if save/replay longevity demands it.

Save granularity contract:

- Tactical saves/checkpoints must support:
  - battle start;
  - turn boundaries;
  - after each stack activation.
- Stack activation checkpoints should capture all state needed to resume without replaying the entire battle.
- Atomic event/effect reconstruction is not required for MVP save granularity, but the data model should not block later event-sourced debugging.
- Save/checkpoint state must include AP state, status state, objective state, visibility state, ability cooldowns/charges, RNG state or seed cursor, created entities, and battle phase/turn/activation index.

Replay model contract:

- MVP replay stores:
  - initial battle state;
  - player commands / AI commands;
  - RNG seeds or deterministic RNG stream state;
  - periodic checkpoints.
- Replay must be deterministic enough to reproduce tactical outcomes during QA.
- Checkpoints reduce replay fragility and make mid-battle debugging practical.
- Full event-sourced replay of every atomic effect is deferred, but structured logs should preserve enough causal data to diagnose common issues.

Hidden-information persistence contract:

- Saves and replays must preserve:
  - true simulation state;
  - observer-visible state for each side/observer;
  - suspected/anomaly metadata;
  - false/decoy metadata;
  - revealed/decoded metadata;
  - stale/last-known information where relevant.
- Later tooling should expand to a full visibility timeline per observer, tracking when information became hidden, suspected, observed, false, revealed, decoded, expired, or invalidated.
- Hidden information must survive save/load without leaking to the wrong observer or losing QA all-truth visibility.

Structured combat log contract:

- MVP structured logs should include:
  - turn/phase/activation index;
  - trigger/event type;
  - source id;
  - target id/query result;
  - costs paid;
  - effect blocks resolved;
  - AP changes;
  - status applications/removals/refreshes;
  - morale/rout changes;
  - objective state/progress changes;
  - visibility state changes;
  - RNG rolls/seed references where relevant;
  - fizzle/failure reasons.
- Player-facing logs may hide or summarize hidden information, but debug/all-truth logs must preserve the real causal data.
- Later tooling may promote this into a full event graph with causal links between commands, triggers, effects, reactions, statuses, objective changes, and visibility transitions.

Schema and versioning contract:

- Data records, saves, and replays must use stable ids for units, abilities, statuses, objectives, effects, created entities, and scenario objects.
- Tactical data must include schema version fields.
- Migration hooks should exist for saves, replays, and data records when ids/fields change.
- MVP does not require a heavy formal migration framework, but schema changes must not silently corrupt tactical saves/replays.
- Versioning is especially important for data-driven abilities, status definitions, objective components, and hidden-information metadata.

Implementation readiness gates:

- A battle can be saved and resumed at battle start, turn boundary, and after stack activation.
- A replay can reproduce a tactical battle from initial state, commands, RNG seed/state, and checkpoints.
- Hidden/suspected/false/revealed information persists correctly per observer.
- Structured logs expose enough detail to debug AP grants/refunds, status resolution, objective eligibility/progress, morale/rout, and visibility changes.
- Schema versions and stable ids exist for tactical data records before broad content authoring begins.
