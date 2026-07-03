---
title: Post-Audit Foundation Pivot Brief — 2026-07-03
type: decision-brief
status: approved
phase: production
owner: shared
created: 2026-07-03
updated: 2026-07-03
related:
  - production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation
  - docs/architecture/data-scenario-save-format-adr
  - production/planning/next-implementation-direction-brief-2026-07-02
  - design/gdd/strategic-map
  - design/gdd/tactical-combat
  - design/registry/entities
  - design/registry/formulas
  - design/registry/terms
approval: approved
---

# Post-Audit Foundation Pivot Brief — 2026-07-03

## Approval

Human approval recorded 2026-07-03: "Approved" in response to the recommended post-audit mini-epic.

This approval authorizes the planning/control pivot. It does not silently approve broad Unity implementation beyond READY child stories.

## Audit-derived state

The full cross-repo audit found that Neon Champions has a strong world, mature agent governance, and a clean deterministic Unity rules foundation, but several control surfaces are hollow: no approved hard-canon setting slice, empty registry files, an empty faction-brief bridge, unapproved tactical depth articles used by implementation, a placeholder validator that always passes, and a hardcoded C# scenario standing in for data.

The production risk is differentiation inversion: the implemented build proves a generic HoMM-like loop, while Neon Champions' distinctive pillars — dirty information, Intel-as-secrets, Champion legitimacy/publicness, Echo consequences, wilderness logistics, and maintenance-as-power infrastructure — remain under-proven.

## Approved pivot

Before more generic loop expansion, run a short foundation/reconciliation track that turns audit findings into project behavior.

Approved outputs:

1. Data/scenario/save-format ADR.
2. Current scenario extraction path from hardcoded C# toward data.
3. Dumb strategic AI plan/story for single-player-valid playtests.
4. Playtest journal artifact and gate hook.
5. Determinism ADR/decision record.
6. Hollow-gate and source-of-truth reconciliation sweep.

## Scope guard

This pivot is not a content expansion and not a new feature buffet. It should reduce future drift and make the next differentiator experiments cheaper.

In scope:

- architecture/source-of-truth decisions;
- data/scenario/save direction;
- playtest evidence workflow;
- gate honesty;
- reconciliation of stale statuses/open questions/faction-pair assumptions;
- first implementation story only when source authority is explicit and READY.

Out of scope unless separately approved:

- full map/scenario editor;
- full save/load UI;
- strategic AI sophistication beyond dumb legal opponent;
- full dirty-information/fog/PR systems;
- broad tactical redesign;
- world canon approvals inside the design repo;
- final art/audio/VFX/localization/accessibility.

## Default source-of-truth corrections

- Barents vs Janus-Kestrel remains a systems-validation pair unless the owner explicitly promotes it to campaign-one canon.
- Home Rule Coalition vs QXZ remains the stronger campaign-one narrative pair unless overruled.
- Determinism should be treated as a deliberate design decision pending ADR finalization, not an accidental test artifact.
- Empty registries and always-green validators must be filled with enforceable checks or demoted/deleted.
- Playtest notes must become production inputs, not only informal memory.

## First child story recommendation

Create `STORY-DATA-001 Static/Scenario Data Contract and Scenario Extraction Prep` as the first implementation-facing packet, after the ADR exists. It should inspect the Unity hardcoded scenario and extract the smallest data contract needed to represent the current scenario without changing gameplay.

## Verdict

APPROVED. Create `EPIC-VSLICE-MVP-015 Post-Audit Foundation Pivot and Reconciliation` and use its READY/READY-candidate child stories for execution.
