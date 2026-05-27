---
title: Data Authoring Direction
type: adr
status: approved
phase: technical-setup
owner: shared
created: 2026-05-27
updated: 2026-05-27
source_lore: []
related: [docs/architecture/unity-technical-scheme, docs/architecture/technical-decision-priorities]
approval: approved
---

# Data Authoring Direction

## Decision

Approved direction: Option D — Phased Hybrid.

Start with constrained ScriptableObjects for earliest prototype/MVP exploration, but design every data object around stable IDs, localization keys, serializable DTOs, validators, and a migration path to external canonical data.

This preserves prototype speed while protecting future map editors, scenario editors, balancing tools, datapacks, and modloaders.

## Purpose

Neon Champions will likely need more than simple Unity Inspector editing.

Expected needs:

- strategic map editor;
- scenario editor;
- balancing tools;
- datapacks;
- possible mod loading;
- localization from the start;
- validation of IDs, references, formulas, ranges, and content completeness;
- serializable runtime state and save data.

This document presents data-authoring architecture options for approval.

## Non-Negotiable Requirements

Regardless of option:

1. Static definitions, scenario data, runtime state, and save data must be separate.
2. Player-facing strings must be localizable through stable keys/IDs.
3. Production data must be validated.
4. IDs must be stable and human-readable where practical.
5. Tuning values must not be hardcoded in production gameplay code.
6. Data changes must be reviewable in Git.
7. Runtime state must be serializable.
8. Tools/editors may help author data, but generated data must remain inspectable and testable.
9. Mod/datapack goals must not be made impossible by early architecture.

## Data Categories

### Static Definitions

Examples:

- factions;
- unit types;
- Champion archetypes;
- tactical actions;
- resources;
- site types;
- technologies/upgrades;
- status effects;
- localization keys.

Static definitions should be immutable at runtime.

### Scenario Data

Examples:

- campaign/scenario metadata;
- map graph/grid;
- site placement;
- starting ownership;
- starting Champions/armies/resources;
- scripted crisis clocks;
- initial information visibility.

Scenario data is authored content, not save data.

### Runtime State

Examples:

- current turn;
- current resources;
- unit positions;
- damage/injury;
- site ownership;
- active effects;
- discovered/hidden Intel;
- tactical battle state.

Runtime state must be serializable and must not be stored only in scene objects.

### Save Data

Save data is a serialized snapshot/projection of runtime state plus references to static/scenario data versions.

Final format is a later ADR.

## Option A — Unity-First ScriptableObject Architecture

Summary:
Use ScriptableObjects as the primary production authoring format. Build Unity editor tools around them. Export/validate as needed.

How it works:

- Static definitions are ScriptableObjects.
- Scenario/map data may be ScriptableObjects or Unity assets.
- Custom Unity Editor windows author maps/scenarios/balance.
- Validators check references and ranges.
- Runtime state is separate C# serializable classes.

Pros:

- Fastest Unity-native iteration.
- Good Inspector/editor integration.
- Easy for small team and visual content editing.
- Strong fit for prefabs, VFX, UI, and scene-linked content.
- Less upfront tooling burden.

Cons:

- Git diffs can be noisy.
- Harder to support external datapacks/mods cleanly.
- Content may become Unity-project-bound.
- Requires discipline to avoid logic and state leaking into assets.
- External scenario/map editing is harder later.

Best if:

- MVP speed matters most.
- Modding/datapacks are later or limited.
- Editors are Unity Editor tools, not standalone tools.

Risk:

- This can become asset spaghetti without validators and strict data boundaries.

## Option B — External Data First

Summary:
Use JSON/YAML/TOML/CSV or similar external files as the canonical source for definitions, maps, scenarios, and localization. Unity imports/loads these files.

How it works:

- Static definitions live in text data files.
- Scenario/map files live in text or structured external format.
- Unity reads imported data into runtime/domain models.
- Editors/tools write external files.
- ScriptableObjects, if used, are generated/cache/presentation adapters rather than canonical truth.

Pros:

- Best Git diffs and reviewability.
- Strong basis for datapacks and mod loading.
- Easier non-Unity tools: balancers, scenario editors, map editors.
- Clear separation between data and Unity presentation.
- Easier automated validation outside Unity.

Cons:

- More upfront architecture.
- More importer/validator tooling required.
- Less convenient for Unity designers at first.
- Needs careful schema/versioning decisions early.
- Can slow prototype iteration.

Best if:

- Modding/datapacks are a serious production goal.
- Scenario/map/balance tools are central.
- Long-term content pipeline matters more than fastest Unity iteration.

Risk:

- Overengineering too early before systems are stable.

## Option C — Hybrid: External Canonical Data + Unity Authoring Adapters

Summary:
External files are the canonical data format for definitions/scenarios/localization, but Unity editor tools can author/edit them. ScriptableObjects are used for Unity-facing presentation references and optional generated caches.

How it works:

- Canonical definitions and scenarios live in external structured files.
- Unity custom editors provide friendly editing UI.
- Importers convert external files to runtime/domain objects.
- Optional generated ScriptableObjects/cache assets may exist but are not design authority.
- Prefabs/presentation assets reference stable IDs, not direct gameplay authority.
- Localization uses stable keys in external tables or Unity Localization tables mapped from keys.

Pros:

- Best long-term architecture for map/scenario editors, datapacks, modding, balancing, and Git review.
- Keeps gameplay data independent of Unity scenes/assets.
- Supports both Unity tooling and external tooling later.
- Strong fit for serializable runtime/save architecture.

Cons:

- Highest design complexity.
- Requires schema/versioning discipline.
- Requires building or adopting import/export tooling.
- More initial work before content iteration feels smooth.

Best if:

- Map/scenario tooling and future datapacks/modloaders are important.
- The game will have lots of authored, balanced, reviewable data.
- We want to avoid Unity asset lock-in.

Risk:

- Too much pipeline before the game systems are proven.

## Option D — Phased Hybrid

Summary:
Start with constrained ScriptableObjects for the earliest prototypes, but design every data object around stable IDs, serializable DTOs, validators, and a migration path to external canonical data.

How it works:

Phase 1: prototype/MVP exploration

- ScriptableObjects may author early static definitions.
- Runtime/domain logic consumes plain C# data structures, not ScriptableObjects directly.
- All definitions have stable IDs and localization keys.
- Data validators are required early.
- Scenario/map structure is designed as serializable DTOs even if edited through Unity first.

Phase 2: production pipeline

- Decide whether external files become canonical.
- Add import/export tools.
- Add map/scenario editor tools.
- Add balancing reports.
- Add datapack/mod package rules.

Phase 3: mod/datapack support

- Define package format.
- Define load order, override rules, validation, compatibility, and localization packaging.

Pros:

- Fast enough for prototypes.
- Avoids immediate overengineering.
- Keeps future map editors/datapacks/modloading viable.
- Strong balance between speed and long-term needs.

Cons:

- Requires discipline now.
- Migration may still hurt if early ScriptableObject usage leaks into domain logic.
- Some tooling will be duplicated or rewritten later.

Best if:

- We want real prototype speed without closing the door on serious content tools.

Risk:

- If not enforced, “temporary” ScriptableObjects become permanent architecture.

## Recommendation

Approved choice: Option D — Phased Hybrid.

Reason:

- The user wants map/scenario/balancing tools and likely datapacks/modloaders.
- A pure ScriptableObject-first approach is too Unity-bound for those goals.
- A fully external-data-first approach may be too much before core systems are proven.
- Phased Hybrid gives us prototype speed while enforcing the constraints that keep external tools possible.

## Recommended Early Rules If Option D Is Approved

1. Every definition has a stable string ID.

Examples:

- `faction.unp`
- `unit.unp.security_cadre`
- `resource.intel`
- `site.meridian_station`
- `action.suppress_feed`

2. Every player-facing name/description uses localization keys.

Examples:

- `faction.unp.name`
- `unit.unp.security_cadre.description`
- `resource.intel.tooltip`

3. Domain logic consumes plain C# definition/state objects.

Rule:

- Domain logic may not require ScriptableObject references.
- ScriptableObjects may adapt or author data, but should convert into domain-facing data models.

4. Runtime state is serializable from the start.

Rule:

- Runtime state stores stable IDs and primitive/serializable values.
- Runtime state does not store scene object references as canonical state.

5. Validators are early production infrastructure.

Validators should check:

- duplicate IDs;
- missing references;
- missing localization keys;
- invalid ranges;
- circular references where forbidden;
- scenario/map references to nonexistent definitions;
- placeholder data in production content;
- mod/datapack compatibility later.

6. Map/scenario data should be designed as DTOs before editor UI.

The editor should manipulate structured map/scenario data. It should not make the Unity scene the canonical map file unless explicitly approved.

7. Balance tooling should read the same data pipeline.

Balancers/reports should operate on definitions and scenario data, not scrape prefabs/scenes.

8. Datapack/modloader compatibility should be protected, not fully built now.

Early rule:

- no architecture choice may make external datapacks impossible without explicit approval.

Later ADR needed:

- package format;
- load order;
- override/merge rules;
- dependency/version rules;
- localization packaging;
- validation and rejection behavior;
- security/sandbox limits.

## Approval Decision

Option D — Phased Hybrid is approved.

Other options remain documented as rejected alternatives for now:

- Option A is too Unity-bound for expected map/scenario/modding needs.
- Option B is too heavy before core systems are proven.
- Option C is attractive long-term but too complex as the immediate starting point.

Future ADRs still needed:

- concrete data file/schema format;
- map/scenario DTO structure;
- validation command and test integration;
- Unity editor tooling plan;
- datapack/mod package format;
- localization table/package strategy.
