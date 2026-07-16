---
title: STORY-SAVE-001 Prototype Strategic Save and Resume
type: story
status: ready
phase: production
owner: shared
created: 2026-07-16
updated: 2026-07-16
approval: approved
related: [production/epics/epic-017-fully-playable-prototype-continuity-and-opponent-pressure, production/planning/full-project-review-and-completion-plan-2026-07-12, docs/architecture/prototype-strategic-save-resume-adr, docs/architecture/data-scenario-save-format-adr, docs/architecture/unity-technical-scheme, docs/architecture/control-manifest, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, design/ux/player-shell]
---

# STORY-SAVE-001 Prototype Strategic Save and Resume

## Status

READY / approved by the human owner on 2026-07-16 as proposed. The Unity README activation pointer merged through PR #160 with exact-head and post-merge CI passing; implementation is runnable.

## Story type

Architecture-sensitive Logic + Infrastructure + Player-Shell Integration.

## Parent epic

`production/epics/epic-017-fully-playable-prototype-continuity-and-opponent-pressure.md`.

## User/player/system value

As a prototype player, I want to leave a real strategic match and continue it later, so the game supports a 60–90 minute scenario without requiring one uninterrupted session or reconstructing progress manually.

## Source authority

Required on activation:

- `production/planning/full-project-review-and-completion-plan-2026-07-12.md` §§ Recommended eight-week prototype contract and Week 3 — strategic pressure and save/resume.
- `docs/architecture/prototype-strategic-save-resume-adr.md` — approved exact save boundary, envelope, ownership, failure, and player-flow contract.
- `docs/architecture/data-scenario-save-format-adr.md` §§ Runtime state and Save data.
- `docs/architecture/unity-technical-scheme.md` §§ Core Technical Principle, Project Layout, Assembly Boundary, and Data Authoring Policy.
- `docs/architecture/control-manifest.md` §§ 1, 4, 6, 9, and 10.
- `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.
- `design/ux/player-shell.md` normal title/pause/settings shell rules.

No draft campaign, roster, worldbuilding, or future editor document is implementation authority.

## In scope

- Add the ADR-approved version-1 save envelope and complete current strategic runtime-state DTO mapping without serializing Unity objects or display projections.
- Add domain/application validation and round-trip restore use cases.
- Add infrastructure JSON, SHA-256 integrity, persistent-data-path storage, temporary-write/readback, last-valid backup, and safe replacement behavior.
- Add normal-shell `Save and Return to Title` and `Continue` affordances with explicit valid, unavailable, incompatible, and corrupt states.
- Save only from the stable strategic boundary and reject tactical/transition/pending-command states.
- Restore the merged proof scenario at title entry with exact active faction, turn/round, resources, map/site/base/objective state, Champion/army state, recruitment stock, Intel/Lead state, and one-time Feed consequence state preserved.
- Add focused automated tests and one PlayMode route that mutates meaningful HRC or QXZ state, saves, returns to title, continues, and completes at least one legal post-resume action.

## Out of scope

- Tactical mid-battle save; multiple slots/profiles; autosave cadence; save naming/thumbnails; cloud sync; compression/encryption; migration; campaign/meta persistence; replay logs; seeded RNG work.
- New gameplay, balance, scenario topology, AI policy, faction content, tutorial, editor UI, or final audiovisual assets.
- Refactoring unrelated presentation or domain systems.
- Adding a third-party serialization package or a duplicate shadow gameplay model.

## Allowed placeholders

- Literal prototype slot labels `Continue` and `Save and Return to Title` are allowed through the existing replaceable player-facing string boundary.
- Version `1` supports rejection only; migration UI and recovery tooling are deferred.
- No placeholder integrity, always-green validation, fake save duration, or direct test-only state reconstruction is allowed.

## Dependencies

- EPIC-016 implementation sequence DONE/merged; deferred `STORY-PROOF-QA-001` remains separately pending and is not claimed complete.
- Save ADR approved in the same human decision as this story.
- Existing scenario import/runtime separation and Unity CI remain green.
- Unity README pointer names this story through merged PR #160; exact-head and post-merge pointer CI passed.

## Acceptance criteria

- [ ] A player can mutate at least resources, construction/recruitment or site state, Champion position/army state, objective/turn state, and one-time Feed/Intel state; save from the stable strategic shell; return to title; Continue; and observe structural equality for all current mutable strategic state.
- [ ] The next legal command after restore produces the same result as the same command against an equivalent unsaved state.
- [ ] Continue is offered only for a valid, compatible version-1 save; New Scenario remains usable when Continue is unavailable.
- [ ] Save is unavailable with a readable reason during tactical battle, transition/result application, invalid runtime, or another non-stable boundary.
- [ ] Malformed JSON, wrong format/schema, scenario ID/version mismatch, integrity mismatch, missing references, and out-of-range values fail closed without entering gameplay or deleting/overwriting the last valid save.
- [ ] An interrupted/failed replacement preserves a loadable previous-valid backup; tests use an injected/fake file boundary rather than destructive machine-path assumptions.
- [ ] Domain remains UnityEngine-free; file I/O remains Infrastructure-owned; no third-party serializer or duplicate runtime model is introduced.
- [ ] Normal player-facing save errors contain no stack traces, machine paths, raw IDs, or forbidden geography; debug diagnostics remain inspectable.
- [ ] Existing strategic, tactical, objective, AI, scenario import, and proof-route behavior remains green.
- [ ] EditMode, PlayMode, placeholder/provenance validator, standalone compile, exact-head PR CI, and post-merge main CI pass.

## Verification requirements

- TDD for envelope validation, canonical hash, state mapping, deterministic round trip, incompatibility/corruption, backup preservation, and stable-boundary rejection.
- EditMode tests for every acceptance failure class and structural equality of all current runtime collections/fields.
- PlayMode test from normal title -> faction start -> meaningful strategic mutations -> save/return -> Continue -> one legal post-resume action.
- UI layout/text-fit checks at 1920×1080 for Continue, unavailable reason, save confirmation, and corrupt/incompatible error.
- Evidence under `production/evidence/STORY-SAVE-001/`: README, exact test names/results, one pre-save and one resumed-state screenshot, save-envelope fixture with non-sensitive prototype data, CI URLs, omissions.
- `git diff --check`; asset/`.meta` pairing; no temporary workflow or generated machine save committed.

## Ambiguity Check

Status: PASS.

Human-approved assumptions:

- One continue slot plus last-valid backup is enough for the first prototype.
- Stable strategic boundary only; no tactical mid-battle save.
- JSON envelope, schema version 1, explicit scenario content version, SHA-256 integrity, atomic temp/readback/replace, and reject-without-migration policy are binding.
- Successful manual save returns to title; Continue is title-owned.
- Current deterministic state is preserved without declaring determinism permanent product identity.

Human approval: `Approved` on 2026-07-16, accepting the story and ADR exactly as proposed. Any change to these assumptions requires an approved amendment before implementation continues.

## Branch / PR requirements

- Branch: `story/STORY-SAVE-001-prototype-strategic-save-resume`
- PR title: `STORY-SAVE-001 prototype strategic save and resume`
- Evidence: `production/evidence/STORY-SAVE-001/`
- PR must link the story, both save/data ADRs, Unity scheme, control manifest, tests, and final CI.
- PR must list every omission or state `No known omissions`.
- Codex must commit, push the exact branch head, create/update a non-draft PR, and print branch/SHA/remote ref/PR URL.

## Story readiness gate

- [x] Stable ID, value, scope, acceptance criteria, verification, branch, and evidence are defined.
- [x] Exact approved roadmap/data/Unity/control/test sources are linked.
- [x] Approved save ADR resolves the architecture choices required for implementation.
- [x] Ambiguity Check is PASS.
- [x] Save ADR approved.
- [x] Human approval recorded.
- [x] Story promoted to READY / approved.
- [x] Guarded prompt converted to runnable.
- [x] Unity README pointer activated through CI.

## Activation evidence

- Design approval commit: `5e88074986c5b72d9561ce93abd8e50f7568ab2a`.
- Design publish CI: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/29510269770 — PASS.
- Unity pointer PR: https://github.com/myriwe-bot/neon-champions-unity/pull/160.
- Pointer exact head: `76c47acf31ebf1d5169170baf78b2576401b6bb4`.
- Pointer exact-head CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29510312784 — PASS.
- Pointer merge commit: `9a857e1a52f8d169cffb7f8d1e35b7be9176a0c0`.
- Pointer post-merge CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29510871938 — PASS.

## Verdict

READY / approved and fully activated. Sole current implementation packet after the connected proof; Codex may begin from current `main`.
