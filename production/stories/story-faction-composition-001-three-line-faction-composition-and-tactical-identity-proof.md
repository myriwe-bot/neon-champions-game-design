---
title: STORY-FACTION-COMPOSITION-001 Three-Line Faction Composition and Tactical Identity Proof
type: story
status: ready
phase: production
owner: shared
created: 2026-07-15
updated: 2026-07-15
approval: approved
related: [production/epics/epic-016-accelerated-playable-product-foundation, design/gdd/prototype-faction-contracts, design/gdd/faction-unit-rosters, design/gdd/tactical-combat, design/ux/player-shell, production/stories/story-base-content-001-hrc-qxz-six-facility-prototype-content-and-base-presentation, production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed, production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock]
---

# STORY-FACTION-COMPOSITION-001 Three-Line Faction Composition and Tactical Identity Proof

## Value

As an HRC or QXZ player, I want my starting force, base recruitment choices, army summary, encounter setup, and tactical board to expose three visibly distinct faction lines, so that composition decisions replace placeholder infantry and produce readable faction-specific fights.

## Story type and estimate

Scenario Content + Existing Army/Recruitment Integration + Tactical Presentation. Medium story. Reuse existing unit definitions, fixed recruitment, tactical role behavior, Sensor Lock, player-shell, and six-facility boundaries; do not add a new combat or army system.

Performance budget: no measurable regression to the current strategic or tactical frame/input baseline. Composition summaries refresh only when army, selection, recruitment, or encounter state changes.

## Source authority

- `design/gdd/prototype-faction-contracts.md` governs the approved-provisional three-line faction contrast.
- Existing stable runtime unit IDs and completed ARMY-001/002 remain authoritative for this bounded proof; this story does not rename, re-stat, or replace tactical definitions.
- `STORY-BASE-CONTENT-001` governs the four facility-gated recruitment offers.
- `design/ux/player-shell.md` governs normal-shell army, recruitment, encounter, and tactical readability.

## Binding prototype mapping

These six existing runtime lines are the bounded implementation mapping for this proof:

| Faction | Stable unit ID | Player-facing line | Existing role | Proof access |
|---|---|---|---|---|
| HRC | `settlement_watch` | Settlement Watch | defensive infantry | Watch Muster recruitment |
| HRC | `hunter_scouts` | Hunter-Scouts | recon skirmisher | Scout Relay recruitment |
| HRC | `sled_logistics_team` | Sled Logistics Team | support mobility | starting Champion stack |
| QXZ | `meridian_security` | Meridian Security | disciplined infantry | Mandate Barracks recruitment |
| QXZ | `strato_sensor_swarm` | Strato Sensor Swarm | ranged recon / Sensor Lock | Stratospheric Lab recruitment |
| QXZ | `climate_bulwark` | Climate Bulwark | heavy defender | starting Champion stack |

For this implementation slice, Sled Logistics Team is the existing mobility/support proxy for the approved-provisional HRC rescue/support line, and Strato Sensor Swarm remains the already-authorized proxy for the provisional QXZ Aerosol technical/control line. Preserve all six stable IDs, current display names, stats, role tags, and behavior. Final line names and canon remain deferred.

## Scenario composition contract

- Replace the proof scenario's player-facing starting `unit_placeholder_infantry` stack for the HRC Champion with one `sled_logistics_team` stack at its existing default count of 5.
- Replace the corresponding QXZ Champion starting placeholder stack with one `climate_bulwark` stack at its existing default count of 7.
- Preserve current Watch Muster, Scout Relay, Mandate Barracks, and Stratospheric Lab recruitment offers, counts, costs, stock, refresh, and prerequisites from STORY-BASE-CONTENT-001.
- The proof route must allow each faction to field all three lines by combining its starting line with its two facility-gated recruited lines.
- Do not silently rewrite unrelated historical fixtures whose explicit purpose is placeholder compatibility. Update player-facing proof fixtures and tests whose authority is superseded, while retaining narrowly named legacy/placeholder tests where they still prove compatibility.

## In scope

- Remove player-facing Placeholder Infantry from the current HRC/QXZ proof scenario's starting Champion armies.
- Ensure the starting stack and both facility-gated recruits persist through strategic army state, encounter setup, tactical stack creation, losses, and return summary.
- Show stable player-facing unit names, counts, and concise readable role/decision hints in:
  - selected Champion army summary;
  - recruitment preview/result;
  - encounter/guarded-site setup;
  - tactical stack labels and selected-stack detail;
  - post-battle return summary.
- Preserve and visibly expose existing role differences: durable infantry/defender, mobile or ranged recon, mobility/support, retaliation where authored, and Strato Sensor Lock.
- Ensure the normal proof loop can demonstrate at least one meaningful three-line decision, such as defender anchoring plus recon positioning plus support/control, without requiring a guaranteed win/loss balance result.
- Use existing/project-authored procedural faction markers and the merged White Sky/player-shell presentation. Any external/generated non-code asset must satisfy the provenance contract.
- Add scenario validation and compatibility handling required by the starting-army replacement; no silent loss of imported army state.

## Out of scope

- New unit definitions, final line names, final faction canon, upgrades, tech trees, additional recruitment facilities, random recruitment, weekly growth redesign, or final balance.
- New damage, cover, LOS, morale, action-point, initiative, status, AI, or pathfinding systems.
- New Sensor Lock behavior or broad tactical-role rewrites.
- New tactical shell, strategic topology, base economy, Champion progression, Operations, audio, final models, or animation.
- Broad removal of placeholder definitions still required for legacy tests or compatibility.

## Acceptance criteria

- [ ] The HRC proof Champion starts with `sled_logistics_team` count 5 and no player-facing Placeholder Infantry.
- [ ] The QXZ proof Champion starts with `climate_bulwark` count 7 and no player-facing Placeholder Infantry.
- [ ] HRC can field exactly the mapped three-line proof composition by combining Sled Logistics Team with Watch Muster's Settlement Watch and Scout Relay's Hunter-Scouts.
- [ ] QXZ can field exactly the mapped three-line proof composition by combining Climate Bulwark with Mandate Barracks' Meridian Security and Stratospheric Lab's Strato Sensor Swarm.
- [ ] All six stable IDs, display names, stats, role tags, recruitment values, and existing tactical behaviors remain unchanged.
- [ ] Strategic army summary, recruitment result, encounter setup, tactical labels/details, losses, and return summary preserve correct names/counts without raw IDs or unresolved localization keys.
- [ ] The tactical proof visibly distinguishes all three lines through current role behavior and presentation; Strato Sensor Lock remains usable and readable.
- [ ] Imported/legacy army state is preserved or fails closed with a controlled diagnostic; no partial mutation or silent stack deletion.
- [ ] Existing strategic movement, base construction/effects, recruitment, objective pressure, AI, tactical handoff, battle result, and save/runtime smoke remain green.
- [ ] Existing placeholder-compatibility tests remain only where explicitly scoped; superseded player-facing proof assertions no longer require Placeholder Infantry.
- [ ] Asset/provenance validation passes; no hidden or untracked generated/external non-code asset enters scope.
- [ ] EditMode, PlayMode, validator, standalone build, exact-head PR CI, and post-merge main CI pass.

## Verification and evidence

- EditMode coverage for exact starting compositions, six-line stable mapping, scenario validation, runtime persistence, and no silent migration/state loss.
- PlayMode coverage for both factions completing starting-army plus two-recruit composition, encounter setup, tactical selection/use, losses, and return summary.
- Current PNG evidence under `production/evidence/STORY-FACTION-COMPOSITION-001/`:
  - HRC normal-shell three-line army/recruitment state at 1920×1080;
  - QXZ normal-shell three-line army/recruitment state at 1920×1080;
  - tactical three-line composition with readable roles and selected-stack detail at 1920×1080;
  - QXZ Sensor Lock state only if not already clear in the tactical composition capture.
- Automated evidence assertions must validate the active 1920×1080 render target, UI bounds/non-overlap/text fit, player-facing names/counts/roles, and absence of raw unit IDs or placeholder text in the story-owned captures.

## Ambiguity gate

PASS. The existing six-line mapping is the lowest-risk way to execute EPIC-016's approved next capability without inventing final names or new mechanics. On 2026-07-15 the human decision prompt timed out with explicit instruction to use best judgment, so the recommended bounded mapping is approved: retain Sled Logistics Team as the HRC rescue/support proxy and Strato Sensor Swarm as the QXZ Aerosol technical/control proxy for this proof. Exact SAR Drone Crew and Aerosol Techs implementations remain deferred. If implementation requires a new unit definition, rename, re-stat, or new tactical mechanic, stop and return the blocker.

## Proposed branch

`story/STORY-FACTION-COMPOSITION-001-three-line-identity-proof`

## Verdict

READY / approved through the explicit use-best-judgment fallback on 2026-07-15. Codex may implement only this bounded existing-line composition proof from the activated checked-in prompt.
