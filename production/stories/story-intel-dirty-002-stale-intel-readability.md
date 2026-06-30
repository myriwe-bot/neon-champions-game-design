---
title: STORY-INTEL-DIRTY-002 Stale Intel Readability
type: story
status: done
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
approval: approved
---

# STORY-INTEL-DIRTY-002 Stale Intel Readability

## Status

DONE / merged. Human approval recorded 2026-06-30: "Okay, excellent, agreed." This approved the recommended `Stale Lead` label, not `Contested Lead`. Unity PR #120 merged to `main` as `e479fb92302255237f706a48041fbd327744b19a`; exact-head CI and post-merge CI passed.

## Story type

Strategic UX + Information-state readability + PlayMode Evidence.

## Parent / context

Parent: `EPIC-VSLICE-MVP-012 Intel Leads and Verification`.

`STORY-INTEL-DIRTY-001` proved a true-for-now `Intel Lead` can become `Verified` through active-Champion Intel spend. The next narrow step is to show that not all useful Intel has the same freshness/certainty, without implementing deception, hidden information, or a full dirty-information campaign system.

## Player/design value

As a player, I want the strategic map to tell me when an Intel Lead is stale, so I understand that verification improves confidence rather than simply toggling a generic marker.

## Source authority

Required sources:

- `production/epics/epic-vslice-mvp-012-intel-leads-and-verification.md`.
- `production/stories/story-intel-dirty-001-intel-lead-and-verification-on-ramp.md` for the existing Lead -> Verified baseline.
- `production/planning/next-implementation-direction-brief-2026-06-30.md` for approved EPIC-012 direction/defaults.
- `design/gdd/intel-resource.md` for Intel as actionable secrets and no-subtypes-for-MVP guidance. Narrow source-authority exception: this GDD is draft/pending; only the cited framing is approved for this story.
- `design/gdd/strategic-map.md` §§1-8, §§9-10, and current site/guarded interaction boundaries.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, `docs/architecture/ci-build-automation.md`.

## In scope

- Add one prototype information-freshness/readability state for an existing Intel Lead using the approved `Stale Lead` language.
- Keep the state deterministic and authored/runtime-visible; no random deception or probabilistic truth model.
- Show the stale state in the same strategic site/HUD surfaces used by story 001.
- Let verification resolve the state into a clearer `Verified` presentation using existing Intel and active Champion flow.
- Make the result text explain what changed: stale lead refreshed/resolved, cost paid, and defender risk preview confirmed.
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

- [x] At least one existing guarded site or approved current strategic site can present a stale Intel Lead state before verification.
- [x] The stale state is visibly distinct from the story-001 `Intel Lead` and `Verified` states.
- [x] The active Champion can verify the stale lead using existing Intel, with clear feedback naming the prior state and the resolved/verified result.
- [x] Verification changes presentation to `Verified` or equivalent prototype language and confirms defender strength / tactical risk preview.
- [x] Repeat verification spends 0 additional Intel and does not mutate unrelated site markers/state.
- [x] Baseline story-001 Lead -> Verified behavior remains intact for a non-stale/non-contested lead.
- [x] At least one normal strategic interaction remains visibly usable after verification.
- [x] Evidence under Unity `production/evidence/STORY-INTEL-DIRTY-002/` includes stale-before, verified-after, repeat/already-verified, baseline-lead-regression, and surrounding-loop-unbroken checked-in notes plus omissions/deferred-work notes. CI generated screenshot artifacts but GitHub artifact upload was blocked by storage quota; notes record exact PlayMode assertions and run URLs.
- [x] Exact-head Unity Foundation CI passes before merge.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- Focused EditMode/domain tests for stale state, verification resolution, Intel spend, repeat no-spend, unrelated-state preservation, and baseline Lead -> Verified regression.
- PlayMode smoke or generated PNG/text evidence for stale-before, verified-after, repeat/already-verified, baseline-lead-regression, and surrounding-loop-unbroken states.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge and post-merge main CI after merge.

## Ambiguity Check

Status: PASS. Implementation authority granted for the approved `Stale Lead` path only.

Human-approved answers / assumptions:

- Vocabulary: `Stale Lead` is approved. Do not use `Contested Lead` in this story except in deferred-work notes.
- Model: deterministic readability state only; no false information.
- Actor: active Champion.
- Cost: existing Intel, same cost scale as story 001 unless the user changes it.
- Target: existing guarded site/current strategic site.
- Payoff: clearer Verified defender strength / tactical risk preview.

## Branch / PR requirements

- Branch name: `story/STORY-INTEL-DIRTY-002-stale-intel-readability`.
- PR title: `STORY-INTEL-DIRTY-002 stale intel readability`.
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
- [x] Human implementation approval has been recorded.
- [x] Stale-vs-Contested label choice has been recorded: `Stale Lead`.

## Evidence

- Unity PR #120: https://github.com/myriwe-bot/neon-champions-unity/pull/120
- Merge commit: `e479fb92302255237f706a48041fbd327744b19a`
- Exact-head Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28452805652
- Post-merge Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28453767810
- Unity evidence path: `production/evidence/STORY-INTEL-DIRTY-002/`

## Verdict

DONE / merged. Scope remained the approved `Stale Lead` readability path only; `Contested Lead`, false information, and active deception remain deferred.
