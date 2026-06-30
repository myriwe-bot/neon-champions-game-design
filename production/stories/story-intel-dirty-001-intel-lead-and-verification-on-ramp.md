---
title: STORY-INTEL-DIRTY-001 Intel Lead and Verification On-Ramp
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
    production/epics/epic-vslice-mvp-011-champion-assets-and-operations-depth,
    design/gdd/intel-resource,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-INTEL-DIRTY-001 Intel Lead and Verification On-Ramp

## Status

READY-candidate / approval pending. Human approved the EPIC-012 direction and defaults on 2026-06-30, but this story is not Unity implementation authority until explicitly promoted to READY / approved.

## Story type

Strategic UX + Domain/Presentation + PlayMode Evidence.

## Parent / context

Parent: `EPIC-VSLICE-MVP-012 Intel Leads and Verification`.

EPIC-011 proved the active Champion can present and use a prototype Intel-spending Operation. The next narrow step is to make Intel point at concrete strategic uncertainty: a guarded-site Intel Lead that can be verified into a readable risk preview.

## Player/design value

As a player, I want Intel to identify and verify useful strategic information, so that spending Intel feels like turning a lead into operational certainty before I commit to a site or battle.

## Source authority

Required sources:

- `production/epics/epic-vslice-mvp-012-intel-leads-and-verification.md`.
- `production/planning/next-implementation-direction-brief-2026-06-30.md`.
- `design/gdd/intel-resource.md` for Intel as actionable secrets and existing MVP source/sink language. Narrow source-authority exception: this GDD is draft/pending, but the cited Intel framing is approved for this story only by the 2026-06-30 human approval.
- `design/gdd/strategic-map.md` §§1-8, §§9-10, and current site/guarded interaction boundaries.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, `docs/architecture/ci-build-automation.md`.

## In scope

- Add a minimal `Intel Lead` state/presentation for an existing guarded site or equivalent current strategic site.
- Show the pre-verification state as `Lead` or equivalent non-final prototype label.
- Let the active Champion verify the lead using existing Intel resource language and existing strategic-map/HUD surfaces.
- First payoff: reveal or confirm guarded-site defender strength / tactical risk preview.
- After verification, show the site as `Verified` or equivalent non-final prototype label.
- Deny repeat verification or report already-verified state without spending extra Intel or mutating unrelated site state.
- Prove at least one normal strategic interaction remains usable after verification: movement, site interaction, or guarded-site tactical handoff.
- Add focused EditMode/domain coverage plus PlayMode evidence under Unity `production/evidence/STORY-INTEL-DIRTY-001/`.

## Out of scope

- Full fog-of-war or hidden map reveal.
- Actual false/contested/stale Intel behavior in this story.
- Public PR, legitimacy, scandal feed, blackmail, social graph, or dirty-information campaign systems.
- Strategic AI information valuation.
- New resources, Intel subtypes, recurring income, economy rebalance, or market/exchange systems.
- New map topology, new sites/routes/objectives, tactical combat rules, victory rules, final art/audio/VFX/icons/localization/accessibility framework.
- Full Champion operation loadouts, cooldowns, inventory, or progression.

## Acceptance criteria

- [ ] At least one existing guarded site can present an `Intel Lead` / unverified state before verification.
- [ ] The active Champion can verify that lead using existing Intel, with clear feedback naming what was verified and how much Intel was spent.
- [ ] Verification changes the site presentation from `Lead` to `Verified` or equivalent prototype language.
- [ ] The verified payoff reveals/confirms defender strength or tactical risk preview without adding full fog-of-war or false information.
- [ ] Repeat verification on the same site spends 0 additional Intel and does not mutate unrelated site markers/state.
- [ ] At least one normal strategic interaction remains visibly usable after verification.
- [ ] Existing EPIC-011 Champion Operation behavior continues to pass unless a story-authorized integration adjustment is explicitly documented.
- [ ] Evidence under Unity `production/evidence/STORY-INTEL-DIRTY-001/` includes before-lead, verified, repeat-denied/already-verified, and surrounding-loop-unbroken screenshots/notes plus omissions/deferred-work notes.
- [ ] Exact-head Unity Foundation CI passes before merge.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- Focused EditMode/domain tests for Lead -> Verified state, Intel spend, repeat no-spend, and no unrelated state mutation.
- PlayMode smoke or generated PNG/text evidence for before-lead, verified, repeat/already-verified, and surrounding-loop-unbroken states.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge and post-merge main CI after merge.

## Ambiguity Check

Status: PASS for candidate review; NOT implementation authority.

Human-approved defaults:

- Vocabulary: `Lead` -> `Verified`.
- Actor: active Champion.
- Target: guarded site.
- Cost: existing Intel.
- First payoff: defender strength / tactical risk preview.
- Leads are true-for-now; false/contested/stale information is deferred.
- UI says Intel Lead / Verified, not dirty-info yet.

Candidate assumptions:

- Prototype labels are acceptable and not final canon terminology.
- If an existing Champion Operation surface is the narrowest place to expose verification, it may be reused, but this story must not add full operation loadouts/cooldowns or a second operation suite.
- If the implementation cannot reveal exact defender details cleanly, it should reveal a bounded risk tier using existing defender/site state rather than inventing new tactical rules.

## Branch / PR requirements

- Branch name: `story/STORY-INTEL-DIRTY-001-intel-lead-verification-on-ramp`.
- PR title: `STORY-INTEL-DIRTY-001 intel lead verification on-ramp`.
- Required linked story ID: `STORY-INTEL-DIRTY-001`.
- Required evidence path: `production/evidence/STORY-INTEL-DIRTY-001/` in Unity.
- Required omissions section: explicitly list deferred fog/false-info/PR/AI/economy systems or state `No known omissions`.

## Human approval

Epic direction and defaults approved 2026-06-30. This story still requires explicit implementation approval before READY promotion.

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

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required evidence exists.
- [ ] Required tests/CI pass, or human-approved exceptions are documented.
- [ ] PR/code review is complete if a Unity PR is opened.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY-candidate / approval pending. Do not run Codex implementation or update the Unity current-task pointer until human approval promotes this story to READY / approved.
