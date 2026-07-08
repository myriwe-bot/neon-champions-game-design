---
title: Determinism and RNG ADR
type: adr
status: in-review
phase: production
owner: shared
created: 2026-07-05
updated: 2026-07-05
source_lore: []
related:
  [
    production/stories/story-determinism-001-determinism-and-rng-decision-record,
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    production/planning/post-audit-foundation-pivot-2026-07-03,
    docs/architecture/data-scenario-save-format-adr,
    docs/architecture/testing-strategy,
    docs/architecture/control-manifest,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
  ]
approval: pending
---

# Determinism and RNG ADR

## Decision

Near-term MVP gameplay is deterministic by default.

Neon Champions should not add random damage, hit/crit rolls, randomized rewards, procedural generation, AI randomness, hidden information rolls, or other save/replay-affecting random behavior until a separate READY story approves an explicit seeded RNG service and its test, save, replay, debug, data, and CI rules.

This chooses the first branch left open by the data/scenario/save ADR: embrace deterministic runtime behavior for MVP and move uncertainty into authored state, player knowledge, and dirty/source-tagged information instead of implicit numeric randomness.

## Context

The post-audit pivot identified determinism as a deliberate design decision, not an accidental test artifact. The data/scenario/save ADR already requires static definitions, scenario data, runtime state, and save data to remain separate, serializable, and validated. The testing strategy requires deterministic rule tests and explicit coverage for deterministic random behavior if random behavior exists.

The approved strategic MVP is a two-faction local hotseat contest with deterministic turn order, authored scenario data, deterministic strategic movement and site interaction, tactical battle setup/result DTOs, and no strategic AI in the first MVP. Tactical combat already asks for repeatable, data-driven rules and states that can be saved, tested, and replayed/debugged.

Read-only Unity context for this story found no obvious `UnityEngine.Random`, `System.Random`, `Random.Range`, `RNG`, or `random` usage under `Assets`, `Packages`, or `ProjectSettings`.

## What Deterministic Means For MVP

Given the same static definitions, scenario data, runtime state, command sequence, and approved build, the same rule result should occur.

Examples:

- the same strategic command should produce the same movement, site interaction, reward, ownership, and victory state;
- the same battle setup and tactical command sequence should produce the same battle result;
- AI-like behavior that exists in MVP, such as tactical guard behavior, should choose from deterministic rules unless a future story authorizes seeded randomness;
- tests should not need timing, frame order, wall-clock time, collection iteration accidents, or unseeded random sources to pass.

Determinism does not require the player to know every fact. It means the game state and rule transitions are reproducible.

## Dirty Information Is Not Numeric Randomness

Dirty/source-tagged uncertainty is a knowledge model. It describes what the player, faction, Champion, UI, or Intel system believes about an underlying state and where that belief came from.

Examples include confirmed, estimated, stale, unverified, source-tagged, partial, or contested information. Those labels can be authored, derived from deterministic game events, or updated by explicit Intel rules.

Numeric randomness is a resolution model. It changes the underlying game result by sampling from a random source.

For MVP, uncertainty should prefer source-tagged facts over dice. A player may see an estimated enemy army, stale site reward, or unverified scouting lead, but the underlying state transition should still be deterministic unless a future story explicitly introduces seeded RNG.

This ADR does not design the final dirty-information, fog, false-intel, or PR/social graph systems. It only prevents those future systems from being treated as permission for hidden random rolls.

## Stop Conditions For Future Stories

Stop and request a seeded RNG service story or ADR update before implementation if a story wants any of the following:

- random damage variance, hit chance, crit chance, scatter, proc chance, morale roll, rout roll, or status application roll;
- randomized rewards, loot tables, recruitment offers, site contents, event outcomes, or resource payouts;
- procedural map, site, route, terrain, tactical layout, deployment, objective, encounter, or campaign generation;
- strategic AI, tactical AI, neutral guard, or operation choice randomness;
- hidden-information rolls, fog rolls, false-intel rolls, scouting roll tables, or deception odds;
- save/load, replay, undo, debug, telemetry, or CI behavior that depends on any random source;
- use of `UnityEngine.Random`, `System.Random`, GUID/time-based entropy, unordered collection iteration as choice behavior, or package/library randomness in gameplay code.

A future random behavior story is not READY unless it states:

- why deterministic authored behavior is insufficient;
- the seed source and ownership boundary;
- whether the RNG stream is global, per-system, per-scenario, per-battle, or per-command;
- how seeds and RNG cursor/state are serialized;
- how replay/debug logs expose random draws;
- exact fixed-seed tests and cross-run reproducibility checks;
- data/schema validation for any random tables or weighted choices;
- player-facing preview/UX rules for odds if the random result affects player decisions.

## Testing Implications

Domain and application tests should assume deterministic results. They should build state from explicit fixtures, execute commands, and assert exact outcomes.

If seeded randomness is later approved, tests must cover:

- fixed seed produces exact expected sequence;
- same seed plus same command log reproduces the same state;
- different seeds are intentionally different where the story requires that;
- invalid random tables fail validation;
- no unseeded random source is reachable from production rules.

Until then, adding tests that rely on probability, repeated sampling, timing, or "eventually passes" behavior is out of scope.

## Replay And Debug Implications

For MVP, deterministic replay/debug can be modeled as initial state plus command/event history. A full replay tool is not approved by this ADR, but future code should avoid hidden mutable state that would prevent it.

If RNG is later approved, replay/debug evidence must include random draw logs or enough serialized RNG stream state to reproduce results exactly.

## Save Implications

Save data should remain a serialized runtime-state snapshot plus references to static/scenario data identity and version, as defined by the data/scenario/save ADR.

No current save/load feature is approved here. Future save work must not add random initialization, random migration, or nondeterministic restore behavior. If approved RNG exists later, save data must include the seed and stream state needed to continue the same playthrough exactly.

## Data And Scenario Implications

Static definitions and scenario data may include authored values, authored rewards, authored enemy setups, authored uncertainty labels, and authored future extension fields when approved.

They may not introduce random tables, weighted reward pools, procedural generation parameters, or hidden roll definitions until a story approves the schema, validators, and seeded RNG service boundary.

Validation should fail or explicitly block random-looking fields that are not approved by a schema story.

## CI Implications

CI should treat determinism as part of correctness. Relevant checks should be stable across repeated runs on the same inputs.

Future CI expansion may add reproducibility checks for scenario import, strategic command sequences, tactical battle command sequences, and seeded RNG streams if RNG is later approved.

CI failures caused by timing sensitivity, random order, or unseeded gameplay randomness should be treated as defects unless a human-approved exception is documented.

## Follow-Up Stories

Compact follow-ups if future scope needs them:

- `STORY-RNG-001 Seeded RNG Service Contract` - define an explicit RNG service, seed ownership, serialization, logging, and tests before any random mechanic.
- `STORY-REPLAY-001 Deterministic Command Replay Debug Contract` - define minimal command/event replay evidence after save/load or replay work becomes active.
- `STORY-DIRTY-INFO-001 Source-Tagged Uncertainty Rules Packet` - design the first dirty-information rules without defaulting to hidden random rolls.
- `STORY-DATA-RANDOM-001 Random Table Schema And Validators` - only if randomized rewards/procedural content are later approved.

## Non-Goals

- Unity runtime code.
- RNG service implementation.
- Save/load implementation.
- Replay/debug tooling implementation.
- Random damage, hit/crit rolls, AI randomness, procedural generation, randomized rewards, or hidden-info rolls.
- Final dirty-information, fog-of-war, false-intel, PR, or social graph system design.

## Gate

This ADR is ready for story PR review when:

- it records deterministic-by-default as the near-term MVP policy;
- it separates dirty/source-tagged uncertainty from numeric randomness;
- it names future randomness stop conditions;
- it records testing, replay/debug, save, data/scenario, and CI implications;
- it does not authorize Unity runtime changes.
