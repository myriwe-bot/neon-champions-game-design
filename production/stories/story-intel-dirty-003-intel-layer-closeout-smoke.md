---
title: STORY-INTEL-DIRTY-003 Intel Layer Closeout Smoke
type: story
status: done
phase: production
owner: shared
created: 2026-06-30
updated: 2026-07-01
source_lore: [digital-net, greenland, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-012-intel-leads-and-verification,
    production/stories/story-intel-dirty-001-intel-lead-and-verification-on-ramp,
    production/stories/story-intel-dirty-002-stale-intel-readability,
    design/gdd/intel-resource,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-INTEL-DIRTY-003 Intel Layer Closeout Smoke

## Status

DONE / merged. Unity PR #124 merged 2026-07-01 as `a94f83b651bf181fa85dd23165e4ae7a9a1b5b93`. Exact-head PR CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28527741768 after a whitespace evidence fix; post-merge `main` CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28528869421. Unity pointer cleanup PR #125 merged as `362a407bf8a6f3c1955544981ad38d25950904ec`; post-cleanup `main` CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28529985831.

## Story type

Strategic UX + connected integration smoke / closeout-readiness pass with PlayMode evidence.

## Parent / context

Parent: `EPIC-VSLICE-MVP-012 Intel Leads and Verification`.

`STORY-INTEL-DIRTY-001` proved an actionable `Intel Lead` can become `Verified` through active-Champion Intel spend. `STORY-INTEL-DIRTY-002` added deterministic `Stale Lead` readability without implementing false or contested information. The next safe step is not a broader dirty-information system; it is one connected smoke proving the Intel layer is coherent enough for human closeout review, while naming any remaining gaps.

## Player/design value

As a player/tester, I need one visible sequence that shows normal Intel Leads, Stale Leads, verification, already-verified behavior, and ordinary strategic actions still working together, so EPIC-012 can be judged as a readable information layer rather than isolated UI states.

## Source authority

Required sources:

- `production/epics/epic-vslice-mvp-012-intel-leads-and-verification.md`.
- `production/stories/story-intel-dirty-001-intel-lead-and-verification-on-ramp.md` and merged Unity evidence.
- `production/stories/story-intel-dirty-002-stale-intel-readability.md` and merged Unity evidence.
- `production/planning/next-implementation-direction-brief-2026-06-30.md` for approved EPIC-012 direction/defaults.
- `design/gdd/intel-resource.md` for Intel as actionable secrets and no-subtypes-for-MVP guidance. Narrow source-authority exception: this GDD remains draft/pending; only the cited framing is approved for this story.
- `design/gdd/strategic-map.md` §§1-8, §§9-10, and current site/guarded interaction boundaries.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, `docs/architecture/ci-build-automation.md`.

## In scope

- Add or refine exactly one connected PlayMode/evidence path across the existing Intel-layer states:
  1. show at least one normal `Intel Lead` before verification;
  2. verify it into `Verified` using the active Champion and existing Intel rules;
  3. show at least one `Stale Lead` before verification;
  4. verify the stale lead into a clearer `Verified` defender-strength / tactical-risk preview;
  5. prove repeat/already-verified attempts spend 0 extra Intel and do not mutate unrelated site state;
  6. prove a normal strategic interaction remains visibly usable after the Intel markers exist.
- Add only minimal HUD/status/evidence-label adjustments if the connected evidence is unclear.
- Add or update focused tests only where needed to cover connected state flow and regressions from stories 001/002.
- Produce PlayMode/generated PNG or text evidence under Unity `production/evidence/STORY-INTEL-DIRTY-003/`.
- Add a concise EPIC-012 closeout recommendation in implementation evidence: close epic, defer named gaps, or prepare exactly one more candidate if a real blocker remains.

## Out of scope

- New Intel Lead types beyond the existing `Intel Lead`, `Stale Lead`, and `Verified` prototype states.
- `Contested Lead` gameplay, false information, random lying, hidden truth tables, counter-intel, probabilistic misinformation, or active deception.
- Full fog-of-war or hidden map reveal.
- Public PR, legitimacy, scandal feed, blackmail, social graph, or dirty-information campaign systems.
- Strategic AI information valuation.
- New resources, Intel subtypes, recurring income, economy rebalance, markets, or exchanges.
- New map topology, routes, sites, objectives, tactical combat rules, victory rules, final art/audio/VFX/icons/localization/accessibility framework.
- Full Champion operation loadouts, cooldowns, inventory, or progression.

## Acceptance criteria

- [x] Connected evidence shows a normal `Intel Lead` before verification and `Verified` after active-Champion verification.
- [x] Connected evidence shows a `Stale Lead` before verification and a clearer `Verified` defender-strength / tactical-risk preview after verification.
- [x] The sequence makes the difference between `Intel Lead`, `Stale Lead`, and `Verified` readable without introducing false/contested information.
- [x] Repeat/already-verified attempts spend 0 additional Intel and do not mutate unrelated site markers/state.
- [x] At least one normal strategic interaction remains visibly usable after the Intel markers exist.
- [x] Existing story-001 and story-002 focused tests/evidence expectations continue to pass or are updated with equivalent stronger coverage.
- [x] Evidence under Unity `production/evidence/STORY-INTEL-DIRTY-003/` includes lead-before, lead-verified, stale-before, stale-verified, repeat/already-verified, surrounding-loop-unbroken, and omissions/deferred-work notes.
- [x] Exact-head Unity Foundation CI passes before merge.
- [x] EPIC-012 closeout recommendation is documented in Unity evidence and returned in the PR summary.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- Focused EditMode/domain tests for any changed Intel Lead / Stale Lead / Verified behavior, repeat no-spend, unrelated-state preservation, and baseline story-001/story-002 regression.
- PlayMode smoke or generated PNG/text evidence for lead-before, lead-verified, stale-before, stale-verified, repeat/already-verified, and surrounding-loop-unbroken states.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge and post-merge main CI after merge.

## Ambiguity Check

Status: PASS. Implementation authority granted for a connected smoke/closeout-readiness packet only.

Human-approved answers / assumptions:

- The next implementation packet after `STORY-INTEL-DIRTY-002` is the planned `STORY-INTEL-DIRTY-003 Intel Layer Closeout Smoke`.
- The story may make minimal HUD/status/evidence-label adjustments only if the connected evidence is unclear.
- No new dirty-information mechanics are approved: `Contested Lead`, false information, active deception, fog, PR, AI valuation, and broad economy systems remain deferred.
- If implementation already satisfies part of the story, Codex should focus on tests/evidence/closeout recommendation rather than inventing UI scope.

## Branch / PR requirements

- Branch name: `story/STORY-INTEL-DIRTY-003-intel-layer-closeout-smoke`.
- PR title: `STORY-INTEL-DIRTY-003 intel layer closeout smoke`.
- Required linked story ID: `STORY-INTEL-DIRTY-003`.
- Required evidence path: `production/evidence/STORY-INTEL-DIRTY-003/` in Unity.
- Required omissions section: explicitly list deferred contested/false/fog/PR/AI/economy systems or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent/context.
- [x] User/player/system value is clear.
- [x] Source authority and narrow source-authority exception are explicit.
- [x] In-scope and out-of-scope are bounded.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Ambiguity Check is PASS.
- [x] Human implementation approval has been recorded.

## Verdict

DONE / merged. The connected EPIC-012 Intel-layer smoke passed review, exact-head PR CI, and post-merge `main` CI. Evidence recommends closing EPIC-012 for the approved MVP slice, with contested/false/fog/PR/AI/economy systems explicitly deferred.
