---
title: STORY-INTEL-DIRTY-002 Contested or Stale Intel Readability
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-30
updated: 2026-06-30
source_lore: [digital-net, greenland, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-012-intel-leads-and-verification,
    production/stories/story-intel-dirty-001-intel-lead-and-verification-on-ramp,
    design/gdd/intel-resource,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-INTEL-DIRTY-002 Contested or Stale Intel Readability

## Status

READY-candidate / approval pending. `STORY-INTEL-DIRTY-001` is DONE / merged, so the next narrow Intel-layer question is now reviewable. This story is not Unity implementation authority until explicitly promoted to READY / approved.

## Story type

Strategic UX + Information-state readability + PlayMode Evidence.

## Parent / context

Parent: `EPIC-VSLICE-MVP-012 Intel Leads and Verification`.

`STORY-INTEL-DIRTY-001` proved a true-for-now `Intel Lead` can become `Verified` through active-Champion Intel spend. The next narrow step is to show that not all useful Intel has the same freshness/certainty, without implementing deception, hidden information, or a full dirty-information campaign system.

## Player/design value

As a player, I want the strategic map to tell me when an Intel Lead is stale or contested, so I understand that verification improves confidence rather than simply toggling a generic marker.

## Source authority

Required sources:

- `production/epics/epic-vslice-mvp-012-intel-leads-and-verification.md`.
- `production/stories/story-intel-dirty-001-intel-lead-and-verification-on-ramp.md` for the existing Lead -> Verified baseline.
- `production/planning/next-implementation-direction-brief-2026-06-30.md` for approved EPIC-012 direction/defaults.
- `design/gdd/intel-resource.md` for Intel as actionable secrets and no-subtypes-for-MVP guidance. Narrow source-authority exception: this GDD is draft/pending; only the cited framing is approved for this story.
- `design/gdd/strategic-map.md` §§1-8, §§9-10, and current site/guarded interaction boundaries.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, `docs/architecture/ci-build-automation.md`.

## In scope

- Add one prototype information-freshness/readability state for an existing Intel Lead, using either `Stale Lead` or `Contested Lead` language.
- Keep the state deterministic and authored/runtime-visible; no random deception or probabilistic truth model.
- Show the stale/contested state in the same strategic site/HUD surfaces used by story 001.
- Let verification resolve the state into a clearer `Verified` presentation using existing Intel and active Champion flow.
- Make the result text explain what changed: stale/contested lead resolved, cost paid, and defender risk preview confirmed.
- Repeat/already-verified attempts still spend 0 Intel and do not mutate unrelated site state.
- Prove existing `Intel Lead` story-001 behavior remains valid for a normal non-stale/non-contested lead.
- Add focused EditMode/domain coverage and PlayMode evidence under Unity `production/evidence/STORY-INTEL-DIRTY-002/`.

## Out of scope

- Full fog-of-war or hidden map reveal.
- Actual false information, random lying, hidden truth tables, counter-intel, or probabilistic misinformation.
- Public PR, legitimacy, scandal feed, blackmail, social graph, or dirty-information campaign systems.
- Strategic AI information valuation.
- New resources, Intel subtypes, recurring income, economy rebalance, market/exchange systems.
- New map topology, new sites/routes/objectives, tactical combat rules, victory rules, final art/audio/VFX/icons/localization/accessibility framework.
- Full Champion operation loadouts, cooldowns, inventory, or progression.

## Acceptance criteria

- [ ] At least one existing guarded site or approved current strategic site can present a stale/contested Intel Lead state before verification.
- [ ] The stale/contested state is visibly distinct from the story-001 `Intel Lead` and `Verified` states.
- [ ] The active Champion can verify the stale/contested lead using existing Intel, with clear feedback naming the prior state and the resolved/verified result.
- [ ] Verification changes presentation to `Verified` or equivalent prototype language and confirms defender strength / tactical risk preview.
- [ ] Repeat verification spends 0 additional Intel and does not mutate unrelated site markers/state.
- [ ] Baseline story-001 Lead -> Verified behavior remains intact for a non-stale/non-contested lead.
- [ ] At least one normal strategic interaction remains visibly usable after verification.
- [ ] Evidence under Unity `production/evidence/STORY-INTEL-DIRTY-002/` includes stale/contested-before, verified-after, repeat/already-verified, baseline-lead-regression, and surrounding-loop-unbroken screenshots/notes plus omissions/deferred-work notes.
- [ ] Exact-head Unity Foundation CI passes before merge.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- Focused EditMode/domain tests for stale/contested state, verification resolution, Intel spend, repeat no-spend, unrelated-state preservation, and baseline Lead -> Verified regression.
- PlayMode smoke or generated PNG/text evidence for stale/contested-before, verified-after, repeat/already-verified, baseline-lead-regression, and surrounding-loop-unbroken states.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge and post-merge main CI after merge.

## Ambiguity Check

Status: PASS for candidate review; NOT implementation authority.

Recommended defaults for approval review:

- Vocabulary: prefer `Stale Lead` unless the user wants the stronger `Contested Lead` implication.
- Model: deterministic readability state only; no false information.
- Actor: active Champion.
- Cost: existing Intel, same cost scale as story 001 unless the user changes it.
- Target: existing guarded site/current strategic site.
- Payoff: clearer Verified defender strength / tactical risk preview.

Open approval question:

- Should story 002 use the softer `Stale Lead` label or the stronger `Contested Lead` label?

## Branch / PR requirements

- Branch name: `story/STORY-INTEL-DIRTY-002-stale-intel-readability` unless the approved label changes to contested.
- PR title: `STORY-INTEL-DIRTY-002 stale intel readability` unless the approved label changes to contested.
- Required linked story ID: `STORY-INTEL-DIRTY-002`.
- Required evidence path: `production/evidence/STORY-INTEL-DIRTY-002/` in Unity.
- Required omissions section: explicitly list deferred fog/false-info/PR/AI/economy systems or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent/context.
- [x] User/player/system value is clear.
- [x] Source authority and narrow source-authority exception are explicit.
- [x] In-scope and out-of-scope are bounded.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Ambiguity Check is PASS for candidate review.
- [ ] Human implementation approval has been recorded.
- [ ] Stale vs Contested label choice has been recorded.

## Verdict

READY-candidate / approval pending. Do not run Codex implementation or update the Unity current-task pointer until human approval promotes this story to READY / approved and resolves the Stale vs Contested label choice.
