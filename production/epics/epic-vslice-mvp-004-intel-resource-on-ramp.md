---
title: EPIC-VSLICE-MVP-004 Intel Resource On-Ramp
type: epic
status: approved
phase: production
owner: shared
created: 2026-06-12
updated: 2026-06-12
source_lore: [digital-net, greenland, blue-monday]
related:
  [
    design/gdd/game-pillars,
    design/gdd/intel-resource,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes,
    production/stories/story-intel-001-faction-intel-and-data-cache-pickup,
    production/stories/story-intel-002-first-intel-spending-sink-field-upgrade,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-004 Intel Resource On-Ramp

## Status

APPROVED for production story train. Human approved next-step implementation prep on 2026-06-12 after accepting EPIC-VSLICE-MVP-003 closeout.

This epic is the next recommended vertical-slice spine because the prior slice proved HoMM-like movement/capture/tactical stakes, while the remaining core pillar gap is Intel as secrets turned into power. It started with a tiny visible earning/display loop in INTEL-001 and now continues with exactly one narrow first spend sink in INTEL-002 before any broader upgrade tree, fog, dirty information, or economy depth.

## Priority tier

Vertical Slice / MVP.

## Phase

Production.

## Owner

Shared.

## Related systems

- Strategic Map.
- Resources.
- Intel Resource.
- Site interaction / map rewards.
- UI/HUD/readability.
- Data/content validation.

## Capability goal

Give the player the first visible Intel resource loop: a faction can discover and claim a data cache, gain Intel as a strategic resource, see the result in the HUD/status text, spend it once on a placeholder field upgrade, and retain that state across turns.

## Player / design value

The previous slice made combat matter. This slice starts making secrets matter.

Relevant pillars:

- [x] Cyberpunk strategy/RPG.
- [x] Infrastructure-first conflict.
- [x] Intel as secrets turned into power.
- [x] HoMM-like exploration, capture, and tactical escalation.
- [ ] Dirty information.
- [ ] Champions as legitimacy and force projection.

## Source requirements

- GDDs:
  - `design/gdd/intel-resource.md` §§19-24, 51-78, 79-91, 103-118, 156-164 for Intel fantasy, MVP rules, acquisition modes, prototype values, and acceptance criteria.
  - `design/gdd/strategic-map.md` §§6, 8, 10, 11, 12, 13 for sites, control, resources, recruitment/reinforcement context, and turn persistence.
  - `design/gdd/game-pillars.md` for Intel as secrets turned into power and cyberpunk strategy/RPG pillars.
- ADRs / architecture docs / control-manifest sections:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Parent milestone:
  - `EPIC-VSLICE-MVP-003` DONE / closed.

Implementation authority note: the broader Intel GDD remains draft/pending for later systems. Human approval on 2026-06-12 authorizes only the bounded child story scopes in this epic: INTEL-001 earning/display and INTEL-002 one placeholder field-upgrade spend. Broader Intel systems remain unapproved unless later stories are separately approved.

## Scope

### In scope

- Faction-level Intel resource state for the current scenario.
- A single deterministic map data cache source.
- One-time Intel award from claiming that cache.
- Visible HUD/status feedback for faction Intel and the cache claim.
- Tests and PNG evidence that prove the on-ramp works.
- One narrow first Intel spending sink: a one-time placeholder Champion field upgrade costing 5 Intel.

### Out of scope

- General Intel spending systems, upgrade trees, operations, hacks, doctrine, asset inventory, or site upgrades beyond the single INTEL-002 placeholder field upgrade.
- Intel subtypes such as HUMINT/SIGINT/Research/Proof.
- Fog of war, hidden information, dirty-information spoofing, counter-intel cleanup, or reveal layers.
- Reverse-engineering/dismantling assets.
- Recurring weekly income, Intel Exchanges, Analysis Cells, market trading, or full economy balancing.
- Tactical optional objectives that award Intel.
- Final content names, lore copy, art, icons, accessibility, or broad UI redesign.

### Deferred

- Guarded data vaults and tactical Intel rewards.
- Dirty information / polluted-feed mechanics.
- Champion skills that modify Intel income or cost.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-INTEL-001 Faction Intel and Data Cache Pickup](../stories/story-intel-001-faction-intel-and-data-cache-pickup.md) | DONE / merged | Strategic Logic + UI/Integration + Data/Smoke | EPIC-003 DONE | Intel state tests, data-cache interaction tests, PlayMode smoke, PNG evidence, CI |
| [STORY-INTEL-002 First Intel Spending Sink — Field Upgrade](../stories/story-intel-002-first-intel-spending-sink-field-upgrade.md) | DONE / merged | Strategic Economy + UI/Integration + Smoke | INTEL-001 DONE | Spend preview/commit tests, insufficient/duplicate rejection, PlayMode smoke, PNG evidence, CI |
| [STORY-INTEL-003 Guarded Data Site Intel Reward](../stories/story-intel-003-guarded-data-site-intel-reward.md) | DONE / merged | Tactical/Strategic Integration | INTEL-001/002 DONE | Guarded reward tests, battle-result gating, duplicate rejection, PlayMode smoke, PNG evidence, CI |
| [STORY-INTEL-004 Intel On-Ramp Closeout Smoke](../stories/story-intel-004-intel-on-ramp-closeout-smoke.md) | DONE / merged | Connected Smoke + UX/QA + Evidence | INTEL-001/002/003 DONE | Connected cache -> placeholder Field Upgrade spend -> guarded Intel reward smoke, PNG evidence, CI |
| [STORY-UX-001 Strategic Map Readability and Action Clarity Pass](../stories/story-ux-001-strategic-map-readability-action-clarity-pass.md) | DRAFT / READY-candidate; approval pending | UI / Visual-Feel / Playability Smoke | INTEL-001/002/003/004 DONE; human decision required | TBD |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - `EPIC-VSLICE-MVP-003` DONE / closed.
- Required GDDs:
  - Intel resource draft accepted only for the bounded `STORY-INTEL-001` and `STORY-INTEL-002` subsets.
  - Strategic map MVP GDD.
- Required technical decisions:
  - Existing Unity technical scheme and control manifest.
- Required testing/evidence strategy:
  - Strict layered tests, PlayMode smoke, PNG evidence, CI.
- Required CI/build automation:
  - Existing Unity Foundation CI.
- Required agent instruction scopes / AGENTS.md updates:
  - Unity root and scoped AGENTS.md at implementation time.
- Required data/assets:
  - Placeholder IDs and text only.

## Risks

| Risk | Type | Impact | Mitigation / Owner |
| --- | --- | --- | --- |
| Intel expands into full economy too early | Scope | Story becomes unmergeable or design-heavy | INTEL-001 creates earning/display; INTEL-002 permits one placeholder field-upgrade spend only / shared |
| Data cache becomes final content/lore | Content | Placeholder hardens into canon | Use placeholder IDs and neutral labels / shared |
| Resource schema churn | Technical | Later economy work constrained by premature schema | Keep minimal faction resource state and validators; no subtypes / shared |
| UI readability regresses | UX | Player cannot see what changed | Require PlayMode assertions and PNG evidence / reviewer |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Relevant GDD sections exist for the bounded first story.
- [x] Relevant technical decisions exist or are explicitly N/A.
- [x] Required test/evidence layers are known for expected child story types.
- [x] Required CI/build checks are known.
- [x] Required agent instruction scopes / AGENTS.md updates are known.
- [x] Scope and out-of-scope are explicit.
- [x] Child stories are identified.
- [x] Dependencies are known.
- [x] Major risks are documented.
- [x] At least one child story can pass the Story Readiness Standard: `STORY-INTEL-002`.

## Epic DONE gate

- [ ] Required child stories are DONE or explicitly deferred by human closeout.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, PlayMode/smoke evidence, and manual/PNG evidence are complete or accepted as documented exceptions.
- [ ] Unresolved omissions are documented.
- [ ] Docs have been updated in the correct source-of-truth layer.
- [ ] Playtest/QA evidence exists if required.
- [ ] No open blocker remains hidden.
- [ ] Human review accepts the epic as complete.

## Anti-pattern check

Invalid epic behavior:

- [ ] This epic authorizes production implementation directly.
- [ ] This epic replaces READY stories.
- [ ] This epic hides ambiguous design decisions.
- [ ] This epic bundles unrelated work for convenience.
- [ ] This epic asks agents to figure out missing details.

## Verdict

APPROVED for production as the active Intel vertical-slice capability container. `STORY-INTEL-001` and `STORY-INTEL-002` are DONE / merged; `STORY-INTEL-001`, `STORY-INTEL-002`, `STORY-INTEL-003`, and `STORY-INTEL-004` are DONE / merged. EPIC-004 now awaits human closeout/playtest review; `STORY-UX-001` is a DRAFT / READY-candidate follow-up if readability/action clarity should be improved before deeper gameplay expansion. `field_upgrade_alpha` / “Field Upgrade” remains a temporary placeholder.
