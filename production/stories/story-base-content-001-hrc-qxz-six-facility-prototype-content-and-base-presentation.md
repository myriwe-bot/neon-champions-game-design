---
title: STORY-BASE-CONTENT-001 HRC/QXZ Six-Facility Prototype Content and Base Presentation
type: story
status: done
phase: production
owner: shared
created: 2026-07-14
updated: 2026-07-15
approval: approved
related: [production/epics/epic-016-accelerated-playable-product-foundation, design/gdd/prototype-faction-contracts, design/gdd/strategic-map, design/ux/player-shell, design/art/prototype-visual-target-and-asset-ledger, production/stories/story-base-001-base-definition-and-facility-construction-core, production/stories/story-base-002-administration-income-chain-and-recruitment-dwellings]
---

# STORY-BASE-CONTENT-001 HRC/QXZ Six-Facility Prototype Content and Base Presentation

## Value

As an HRC or QXZ player, I want my base to present six faction-specific, understandable facility choices whose construction visibly changes income, recruitment, or existing Champion support, so that the proof build demonstrates meaningful faction identity and base progression rather than placeholder facility IDs.

## Story type and estimate

Content + Strategic Economy Integration + UI/Presentation. Medium story: one bounded implementation packet, expected to reuse existing base/effect/player-shell boundaries rather than introduce a new system.

Performance budget: no measurable regression to the current strategic-shell frame or input responsiveness; facility state is evaluated at base-panel refresh, construction, or active-faction turn boundaries rather than every frame. Existing standalone-build and PlayMode smoke timing is the acceptance baseline.

## Source authority

- `design/gdd/prototype-faction-contracts.md` is authoritative for the approved-provisional HRC/QXZ facility names, functions, contrasts, six-choice breadth, and three-to-four-affordable proof target.
- `design/gdd/strategic-map.md` §§12-16 and completed `STORY-BASE-001` / `STORY-BASE-002` remain authoritative for one build per base per cycle, recurring resources, recruitment offers, runtime state, validation, and strategic/tactical boundaries.
- `design/ux/player-shell.md` governs the normal base-inspection/build flow.
- `design/art/prototype-visual-target-and-asset-ledger.md` governs presentation assets and provenance.

## Proposed prototype mapping and tuning

These implementation values were human-approved on 2026-07-14. They are prototype tuning, not final balance.

| Faction | Facility | Candidate effect | Candidate cost / prerequisite |
|---|---|---|---|
| HRC | Council Office | Starting/prebuilt administration; +5 Credits at active-faction turn start | prebuilt baseline |
| HRC | Repair Cooperative | +5 Materials at active-faction turn start | 25 Credits + 10 Materials; Council Office |
| HRC | Watch Muster | Unlock Settlement Watch recruitment offer | 20 Credits + 5 Materials; Council Office |
| HRC | Scout Relay | Unlock Hunter-Scouts recruitment offer | 25 Credits + 8 Materials; Council Office |
| HRC | Witness Mesh | +1 Intel at active-faction turn start | 20 Credits + 2 Intel; Council Office |
| HRC | Operations Garage | Apply an authored 10 Credits / 5 Materials discount to the existing starting-hub reinforcement/support action | 35 Credits + 15 Materials; Repair Cooperative |
| QXZ | Concession Office | Starting/prebuilt administration; +7 Credits at active-faction turn start | prebuilt baseline |
| QXZ | Climate Fabricator | +6 Materials at active-faction turn start | 25 Credits + 1 Intel; Concession Office |
| QXZ | Mandate Barracks | Unlock Meridian Security recruitment offer | 20 Credits + 1 Intel; Concession Office |
| QXZ | Stratospheric Lab | Unlock existing Strato Sensor Swarm recruitment offer; this fills the provisional Aerosol Techs line role without renaming the unit | 25 Credits + 2 Intel; Concession Office |
| QXZ | Risk Analytics Cell | +1 Intel at active-faction turn start | 25 Credits + 2 Intel; Concession Office |
| QXZ | Continuity Suite | Apply an authored 10 Credits / 2 Intel discount to the existing starting-hub reinforcement/support action | 35 Credits + 3 Intel; Climate Fabricator |

The scenario economy must make roughly three or four facilities per faction realistically constructible during the proof, not all six. If current scenario length or resource rewards make that impossible, adjust only prototype costs/rewards and document the tuning; do not expand the economy system.

## Preflight clarification: reinforcement pricing and legacy migration

The first implementation preflight found that both existing starting-hub fixed offers were free and that the old facility IDs did not have an authoritative migration table. The following correction is binding implementation authority:

### Starting-hub fixed-offer prices

| Faction | Undiscounted fixed-offer cost | Support facility | Effective cost after support |
|---|---|---|---|
| HRC | 20 Credits + 10 Materials | Operations Garage: −10 Credits and −5 Materials | 10 Credits + 5 Materials |
| QXZ | 20 Credits + 4 Intel | Continuity Suite: −10 Credits and −2 Intel | 10 Credits + 2 Intel |

- Apply discounts per resource, clamped at zero; never create resources from an over-discount.
- Preview, affordability, resource deduction, and result summaries must use the same effective-cost calculation.
- The discount applies only when the relevant support facility is constructed at the active faction's owned starting base.
- Preserve current fixed-offer stock and major-interaction rules; this clarification does not authorize additional stock or refresh behavior.

### Facility-gated recruitment offers

The four recruitment facilities use the following exact prototype offers:

| Facility | Offer ID | Existing unit ID / display | Stack | Initial stock | Refresh / active-faction turn | Cost |
|---|---|---|---:|---:|---:|---|
| Watch Muster | `offer_home_rule_base_dwelling_settlement_watch` | `settlement_watch` / Settlement Watch | 8 | 1 | 1 | 15 Credits |
| Scout Relay | `offer_hrc_scout_relay_hunter_scouts` | `hunter_scouts` / Hunter-Scouts | 6 | 1 | 1 | 20 Credits + 5 Materials |
| Mandate Barracks | `offer_qxz_base_dwelling_meridian_security` | `meridian_security` / Meridian Security | 8 | 1 | 1 | 15 Credits |
| Stratospheric Lab | `offer_qxz_stratospheric_lab_strato_sensor_swarm` | `strato_sensor_swarm` / Strato Sensor Swarm | 5 | 1 | 1 | 20 Credits + 2 Intel |

- All four are normal existing-unit recruitment offers and use the existing recruitment service.
- `strato_sensor_swarm` is the authorized implementation mapping for the provisional Aerosol Techs tactical-line role. Retain its current ID, display name, stats, role, and sensor-lock behavior; do not create or rename a tactical unit in this story.
- Preserve the two existing offer IDs for Settlement Watch and Meridian Security to avoid unnecessary compatibility churn. The Hunter-Scouts and Strato Sensor Swarm offer IDs above are new stable IDs.
- Each offer requires its row's facility stable ID below. Preview/apply, stock decrement, active-faction refresh, affordability, and resource deduction follow existing recruitment rules.

### Stable new facility IDs

| Faction | Facility | Stable ID |
|---|---|---|
| HRC | Council Office | `facility_hrc_council_office` |
| HRC | Repair Cooperative | `facility_hrc_repair_cooperative` |
| HRC | Watch Muster | `facility_hrc_watch_muster` |
| HRC | Scout Relay | `facility_hrc_scout_relay` |
| HRC | Witness Mesh | `facility_hrc_witness_mesh` |
| HRC | Operations Garage | `facility_hrc_operations_garage` |
| QXZ | Concession Office | `facility_qxz_concession_office` |
| QXZ | Climate Fabricator | `facility_qxz_climate_fabricator` |
| QXZ | Mandate Barracks | `facility_qxz_mandate_barracks` |
| QXZ | Stratospheric Lab | `facility_qxz_stratospheric_lab` |
| QXZ | Risk Analytics Cell | `facility_qxz_risk_analytics_cell` |
| QXZ | Continuity Suite | `facility_qxz_continuity_suite` |

### Legacy facility-ID migration

| Legacy ID | New stable ID |
|---|---|
| `facility_home_rule_admin_core` | `facility_hrc_council_office` |
| `facility_home_rule_admin_uplink` | `facility_hrc_repair_cooperative` |
| `facility_home_rule_regional_command` | `facility_hrc_operations_garage` |
| `facility_home_rule_sensor_annex` | `facility_hrc_watch_muster` |
| `facility_qxz_admin_core` | `facility_qxz_concession_office` |
| `facility_qxz_admin_uplink` | `facility_qxz_climate_fabricator` |
| `facility_qxz_regional_command` | `facility_qxz_continuity_suite` |
| `facility_qxz_signal_annex` | `facility_qxz_mandate_barracks` |

Migration rules:

1. Replace each known legacy constructed-facility ID with the corresponding stable new ID before normal runtime use.
2. A migrated facility remains constructed even if imported state conflicts with a new prerequisite. Do not auto-construct a missing prerequisite and do not delete or roll back the migrated facility.
3. Emit a non-fatal migration/validation diagnostic for grandfathered prerequisite inconsistency. Normal prerequisite enforcement applies to future construction only.
4. Collapse duplicate old/new IDs to one constructed entry deterministically.
5. Unknown removed facility IDs must not be silently discarded: preserve the source state, emit a blocking migration diagnostic, and stop loading/applying that state until explicitly resolved.
6. Scout Relay, Witness Mesh, Stratospheric Lab, and Risk Analytics Cell have no legacy equivalents and start unbuilt.

## In scope

- Replace generic/placeholder facility presentation in the proof scenario with exactly the six approved-provisional facilities for each faction.
- Preserve stable IDs and scenario-authored/localization-key-driven display data; no player-facing raw IDs.
- Extend existing facility effect metadata only as narrowly required for:
  - recurring Credits, Materials, or Intel income at the already-authorized turn boundary;
  - facility-gated recruitment offers using existing recruitment services;
  - an authored cost discount on the existing starting-hub reinforcement/support action.
- Keep effect resolution data-driven. Do not hardcode HRC/QXZ branches in UI or command services.
- Show the full six-facility catalog in the normal base panel with readable built, available, affordable, prerequisite-blocked, and already-built states.
- Show facility name, short function, cost, prerequisite, and expected effect before construction.
- After construction, visibly show resource change, constructed state, and the effect unlocked or improved.
- Preserve the merged White Sky presentation and use faction-appropriate shape/material accents for the base panel or facility markers where practical.
- Use only existing/project-authored presentation assets unless a separately justified asset passes the approved provenance contract.
- Add migration/compatibility handling if existing saves or scenario fixtures reference the old placeholder facility IDs; no silent state loss.
- Produce current 1920×1080 evidence for HRC and QXZ base panels plus one constructed/effect-result state.

## Out of scope

- New base capture, siege, garrison, marketplace, trading, logistics, weather, fog, strategic AI, editor UI, or topology systems.
- A full HoMM town tree, upgrades, mutually exclusive branches, or more than six facilities per faction.
- New tactical unit-line behavior; the next EPIC-016 story owns the three-line tactical identity pass.
- New Champion progression or Operations mechanics. The support facilities may only alter the existing reinforcement/support action through authored cost metadata.
- Final facility art, animation, audio, icons, faction canon, or final balance.
- Broad refactoring of the strategic economy, player shell, render pipeline, or asset architecture.

## Acceptance criteria

- [ ] The proof scenario exposes exactly six named HRC and six named QXZ facilities matching `prototype-faction-contracts.md`.
- [ ] No player-facing base panel, build result, or evidence capture shows placeholder localization text or raw facility IDs.
- [ ] Facility definitions and effects are scenario-authored, serializable, validated, and resolved without faction-specific UI/service branches.
- [ ] Credits, Materials, and Intel recurring effects apply once at the active-faction turn boundary, only from owned constructed facilities, with visible feedback and no preview/failed-turn mutation.
- [ ] Watch Muster, Scout Relay, Mandate Barracks, and Stratospheric Lab gate exactly the four authored offer IDs, existing unit IDs, stack sizes, costs, initial stock, and refresh values in the binding recruitment table.
- [ ] Stratospheric Lab recruits `strato_sensor_swarm` displayed as `Strato Sensor Swarm`; this story does not add an Aerosol Techs unit or rename/re-stat the existing unit.
- [ ] Operations Garage and Continuity Suite visibly change the cost/affordability of the existing starting-hub reinforcement/support action through authored effect metadata.
- [ ] Undiscounted/effective starting-hub costs are exactly HRC `20 Credits + 10 Materials` → `10 Credits + 5 Materials` and QXZ `20 Credits + 4 Intel` → `10 Credits + 2 Intel`; preview and apply use identical clamped calculations.
- [ ] Every known legacy facility ID migrates according to the binding table; duplicate IDs collapse, grandfathered prerequisite conflicts remain constructed with a non-fatal diagnostic, and unknown removed IDs fail closed without state loss.
- [ ] One build per base per strategic cycle, affordability, prerequisites, duplicate protection, and no-partial-mutation behavior remain green.
- [ ] The base panel communicates all six choices and built/available/blocked states at 1920×1080 in the normal player shell.
- [ ] Prototype scenario tuning allows approximately three or four facilities per faction to be constructed during the proof but does not make all six routine purchases.
- [ ] Existing strategic movement, site interaction, objective pressure, AI, tactical handoff, recruitment, and battle-result smoke behavior remain green.
- [ ] Asset validation passes; every visible external/generated non-code asset is source-identifiable, ledgered where required, and replaceable. AI-generated assets, if any, obey the literal `ai-generated__` naming/path/provenance contract.
- [ ] EditMode, PlayMode, validator, standalone-build, exact-head PR CI, and post-merge main CI pass.

## Verification and evidence

- EditMode tests for definition/effect validation, resource timing, ownership filtering, support-discount calculation, migration, and no partial mutation.
- PlayMode tests for HRC and QXZ base-panel states, build/result flow, gated recruitment, support discount, normal-shell readability, and preserved connected-loop smoke.
- PNG evidence under `production/evidence/STORY-BASE-CONTENT-001/`:
  - HRC six-facility base panel at 1920×1080;
  - QXZ six-facility base panel at 1920×1080;
  - constructed facility with visible effect/result at 1920×1080.
- PR body lists prototype tuning, old-ID migration/compatibility, assets/provenance, omissions, placeholders, evidence, and exact-head CI.

## Ambiguity gate

PASS. On 2026-07-14 the human explicitly approved `STORY-BASE-CONTENT-001 as proposed`, including the facility mapping, prototype values, prerequisites, three-to-four-affordable target, recruitment gates, and reinforcement/support discounts. The first Codex preflight then correctly stopped because current fixed offers were free and legacy migration was underspecified. A clarification request timed out with explicit instruction to use best judgment, so the bounded recommended correction now authorizes the exact fixed-offer prices and migration rules above. A second preflight found no existing Aerosol Techs unit; the same use-best-judgment fallback authorizes `strato_sensor_swarm` / `Strato Sensor Swarm` without rename or re-stat and locks the exact four-offer table above. These values remain tunable prototype balance rather than final canon. If implementation would require a new Champion system or tactical unit behavior rather than the bounded existing-system extensions above, stop and return the blocker.

## Proposed branch

`story/STORY-BASE-CONTENT-001-six-facility-content-and-presentation`

## Completion evidence

- Unity PR: https://github.com/myriwe-bot/neon-champions-unity/pull/152
- Final PR head: `a4a5d1d824142c7d0ae968ce2ebec84f1a4431f0`
- Exact-head PR CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29393301644
- Squash merge commit: `d0fcc4d4921c398e52993794ac067d6e439d580d`
- Post-merge `main` CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29393833902
- Evidence: `production/evidence/STORY-BASE-CONTENT-001/` in the Unity repository, including sharp current 1920×1080 HRC, QXZ, and construction-result captures.
- Independent closure review passed after null imported-facility migration and active-render-state layout/readability blockers were repaired.

## Verdict

DONE / merged on 2026-07-15. The six-facility HRC/QXZ content, migration, recruitment/economy effects, normal-shell presentation, exact-head CI, and post-merge `main` CI passed.
