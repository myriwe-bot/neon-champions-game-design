---
title: Prototype Strategic Save and Resume ADR
type: adr
status: approved
phase: technical-setup
owner: shared
created: 2026-07-16
updated: 2026-07-16
approval: approved
related: [docs/architecture/data-scenario-save-format-adr, docs/architecture/unity-technical-scheme, docs/architecture/control-manifest, production/epics/epic-017-fully-playable-prototype-continuity-and-opponent-pressure, production/stories/story-save-001-prototype-strategic-save-and-resume]
---

# Prototype Strategic Save and Resume ADR

## Decision

Implement a versioned JSON save envelope around the existing plain-C# strategic runtime state. The first prototype supports one user-managed continue slot plus one protected previous-valid backup, saves only at stable strategic boundaries, and resumes through the normal title/player shell.

## Save boundary

Version 1 may save only when all of these are true:

- the normal strategic map is active;
- no tactical battle, transition, result application, modal decision, or command is pending;
- the runtime has a valid scenario ID and active faction;
- the current state passes save validation.

Tactical mid-battle save is explicitly not supported. The UI must explain why Save is unavailable rather than silently doing nothing.

## Envelope

The persisted document must contain:

- `formatId`: literal `neon-champions-strategic-save`;
- `schemaVersion`: integer `1`;
- `scenarioId`;
- `scenarioContentVersion`: explicit version string supplied by the imported scenario contract;
- `payload`: a dedicated persistence DTO containing `scenarioId`, `scenarioContentVersion`, and the complete mutable strategic state required to resume without reconstruction drift;
- `integrity`: lowercase hexadecimal SHA-256 over the exact UTF-8 bytes produced by serializing `payload` alone with the fixed project serializer settings.

The writer serializes `payload` once, hashes those bytes, then writes the envelope. The reader deserializes the envelope, serializes its parsed `payload` with the same fixed settings, and compares the hash before runtime conversion. Persistence DTO member order is fixed by explicit data-contract ordering; collections retain authored/runtime list order; dictionary/object-property-order dependence is forbidden.

Do not persist display-only projections, Unity scene objects, cached UI labels, test timestamps, machine paths, credentials, or generated random values.

## Ownership and dependency direction

- Domain owns serializable runtime state and validation rules; it performs no file I/O.
- Application owns create-save / validate-save / restore-state use cases.
- Infrastructure owns UTF-8 JSON serialization, hashing, paths, atomic file replacement, and backup handling.
- Presentation owns Save/Continue affordances and readable errors.
- No third-party serialization package is introduced in this story. Reuse the existing `System.Runtime.Serialization.Json.DataContractJsonSerializer` path already used by scenario import, with explicit ordered persistence DTO contracts. A dedicated persistence DTO map is allowed and required; a second mutable gameplay model or parallel source of truth is not. If the existing serializer cannot represent the required state safely with these DTOs, stop and amend this ADR rather than changing serializer or dropping state.

## File and failure policy

- Platform path: Unity persistent data path under a project-owned `Saves` directory.
- Slot names: `continue-v1.json`, temporary `continue-v1.tmp`, backup `continue-v1.backup.json`.
- Write the complete temporary file, flush/close it, validate it by readback, then replace the continue slot atomically where the platform allows.
- Preserve the last valid continue file as backup before replacement.
- On interrupted write, malformed JSON, unsupported format/schema, scenario ID/version mismatch, integrity mismatch, missing required state, or runtime validation failure: do not enter gameplay and do not overwrite/delete the last valid save. Show a concise normal-shell error and retain diagnostics for debug mode.
- Prototype version 1 has no migration. Incompatible saves are rejected explicitly.

## Player flow

- Title shell shows `Continue` only when a valid compatible save exists; invalid data produces `Save unavailable` with a readable reason and leaves `New Scenario` usable.
- Pause/settings shell exposes `Save and Return to Title` only at the stable strategic boundary.
- Successful save returns to title; Continue restores the exact strategic state and normal shell.
- Starting a new scenario does not delete the existing continue slot until the first new valid save replaces it.

## Determinism and continuity

Round-trip equality is structural for all mutable runtime state needed by current gameplay: faction/controller/resources, Champion position/status/movement/army, base ownership/facilities/construction cadence, site ownership/guard/visit/consumed/recruitment stock, objective hold/victory, turn/round/order, pending strategic records permitted by the stable boundary, Intel/Lead state, and any story-owned Feed consequence state.

After restore, the same next legal command must produce the same domain result as it would from the pre-save state. This ADR does not make temporary full determinism permanent product design; it preserves the current baseline.

## Security and privacy

Treat save data as untrusted input. Validate lengths, IDs, ranges, references, schema/version, and integrity before creating active runtime state. Never deserialize arbitrary types or execute data-driven code.

## Deferred

- tactical mid-battle saves;
- multiple manual slots, profiles, save naming, thumbnails, cloud sync, compression, encryption, autosave cadence, migration framework;
- replay/command logs and seeded RNG continuation;
- campaign/meta progression;
- editor-authored migration tooling.

## Gate

APPROVED by the human owner on 2026-07-16 with `STORY-SAVE-001` as proposed. This ADR authorizes only `STORY-SAVE-001`. Any implementation discovery that changes serialization ownership, introduces a package, requires a second mutable gameplay model, or weakens atomic/validation behavior must stop for an ADR amendment.
