---
title: EPIC-VSLICE-MVP-012 Intel Leads and Verification
type: epic
status: approved
phase: production
owner: shared
created: 2026-06-30
updated: 2026-06-30
source_lore: [digital-net, greenland, white-sky]
related:
  [
    design/gdd/game-pillars,
    design/gdd/strategic-map,
    design/gdd/intel-resource,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/planning/next-implementation-direction-brief-2026-06-30,
    production/epics/epic-vslice-mvp-011-champion-assets-and-operations-depth,
    production/stories/story-intel-dirty-001-intel-lead-and-verification-on-ramp,
    production/stories/story-intel-dirty-002-stale-intel-readability,
    production/stories/story-intel-dirty-003-intel-layer-closeout-smoke,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-012 Intel Leads and Verification

## Status

APPROVED / IN PROGRESS. `STORY-INTEL-DIRTY-001` and `STORY-INTEL-DIRTY-002 Stale Intel Readability` are DONE / merged. `STORY-INTEL-DIRTY-003 Intel Layer Closeout Smoke` is READY / approved as the current Unity implementation packet.

Approved defaults:

1. First vocabulary: `Lead` -> `Verified`.
2. First actor: active Champion.
3. First target: guarded site.
4. First payoff: reveal/confirm defender strength or tactical risk preview.
5. First model: leads are true-for-now; contested/false information is deferred.
6. UI should use `Intel Lead` / `Verified`, not dirty-information terminology yet.
7. Story sizing: medium-batched epic with three planned stories.
8. Story 002 label: `Stale Lead`; `Contested Lead` remains deferred.

## Capability goal

Turn Intel from a stockpiled spend resource into a visible information layer. The player should see an actionable Intel Lead, use existing Intel through the active Champion to verify it, and understand the before/after certainty change before committing movement or battle.

## Player / design value

Intel should feel like operational knowledge, not abstract dust. The player should think: "I found a lead; I can spend Intel to verify the risk before I commit." This creates the first step toward Neon Champions' dirty-information pillar while staying below full fog-of-war or misinformation systems.

## Source requirements

- `production/planning/next-implementation-direction-brief-2026-06-30.md` for approved next direction and defaults.
- `design/gdd/intel-resource.md` for Intel as actionable secrets and existing MVP source/sink language. Narrow source-authority exception: this file is `draft` / `approval: pending`, but the cited Intel framing and no-subtypes-for-MVP guidance are accepted for this epic only by the 2026-06-30 human approval. This does not approve the full Intel economy.
- `design/gdd/strategic-map.md` §§1-8, §§9-10, and site/guarded interaction rules for strategic map, Champion, site, route, HUD, and tactical handoff boundaries.
- `docs/architecture/control-manifest.md` §§1, 2, 5, 6, 7, 8, 9, 10.
- `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md` for evidence and CI gates.

## Scope

### In scope

- Minimal Intel Lead state for one or more existing guarded sites.
- Readable `Lead` -> `Verified` state transition.
- Active-Champion verification action using existing Intel resource language.
- First payoff: reveal or confirm guarded-site defender strength / tactical risk preview.
- Repeat/invalid verification handling with no extra Intel spend.
- Focused EditMode tests and PlayMode evidence for each implementation story.

### Out of scope

- Full fog-of-war.
- Actual false information or probabilistic misinformation in the first story.
- Public PR, legitimacy, scandal feed, blackmail networks, or social graph systems.
- Strategic AI reacting to hidden/verified information.
- New resources, Intel subtypes, recurring income, or broad economy rebalance.
- New map topology, route rules, tactical combat rules, victory rules, final art/audio/VFX/icons/localization/accessibility framework.
- Full Champion operation loadouts, cooldowns, inventory, or progression.

### Deferred

- Contested or false leads.
- Counter-intel cleanup.
- Dirty-information operations beyond verification.
- PR/hearts-and-minds warfare.
- Strategic AI information valuation.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-INTEL-DIRTY-001 Intel Lead and Verification On-Ramp](../stories/story-intel-dirty-001-intel-lead-and-verification-on-ramp.md) | DONE / merged | Strategic UX + Domain/Presentation + PlayMode Evidence | EPIC-012 approved; EPIC-011 DONE | Unity PR #117; exact-head and post-merge CI passed |
| [STORY-INTEL-DIRTY-002 Stale Intel Readability](../stories/story-intel-dirty-002-stale-intel-readability.md) | DONE / merged | Strategic UX + Information-state readability | STORY-INTEL-DIRTY-001 DONE | Unity PR #120; exact-head and post-merge CI passed |
| [STORY-INTEL-DIRTY-003 Intel Layer Closeout Smoke](../stories/story-intel-dirty-003-intel-layer-closeout-smoke.md) | READY / approved | Integration smoke + closeout recommendation | STORY-INTEL-DIRTY-002 DONE | Pending Unity PR/evidence |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Risks

| Risk | Type | Impact | Mitigation |
| --- | --- | --- | --- |
| Intel verification becomes full fog-of-war | Scope | Large hidden-info system before core is ready | First story only uses Lead -> Verified on existing guarded site |
| Dirty-info framing becomes fake/deceptive too early | Design | Confusing player with false info before UI has trust language | First story keeps leads true-for-now; false/contested deferred |
| Verification duplicates Champion Operation forecast | UX/System | Mechanic feels redundant after EPIC-011 | Verification should reveal defender strength/risk, not simply repeat site forecast marker |
| Draft Intel GDD status blocks agents | Process | Codex stops correctly | Epic and story record narrow human-approved source exception |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Human approved direction and defaults.
- [x] Relevant design sources and narrow source-authority exception are explicit.
- [x] Scope and out-of-scope are bounded.
- [x] First child story is identified.
- [x] Required test/evidence layers are known.
- [x] No Unity implementation is authorized by the epic alone.

## Epic DONE gate

- [ ] Required child stories are DONE or explicitly deferred by human closeout.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, PlayMode/smoke evidence, and visual/readability evidence are complete or accepted as documented exceptions.
- [ ] Unresolved omissions are documented.
- [ ] Docs have been updated in the correct source-of-truth layer.
- [ ] No open blocker remains hidden.

## Verdict

APPROVED / IN PROGRESS. `STORY-INTEL-DIRTY-001` and `STORY-INTEL-DIRTY-002 Stale Intel Readability` are DONE / merged. `STORY-INTEL-DIRTY-003 Intel Layer Closeout Smoke` is READY / approved as the current implementation packet; it must produce a closeout recommendation before EPIC-012 is closed.
