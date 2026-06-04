---
title: Strategic MVP Closeout Story Train 002
type: milestone
status: approved
phase: production
owner: shared
created: 2026-06-04
updated: 2026-06-04
source_lore: []
related:
  [
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger,
    production/stories/story-tac-002-minimal-hex-board-and-stack-placement,
    production/stories/story-tac-003-minimal-tactical-movement-and-attack-resolution,
    production/stories/story-tac-004-minimal-battle-end-and-result-return,
    production/stories/story-strat-005-strategic-battle-result-application,
    production/stories/story-loop-002-visible-guarded-site-capture-smoke,
    production/stories/story-qa-003-guarded-site-capture-readability-and-evidence-pass,
  ]
approval: approved
---

# Strategic MVP Closeout Story Train 002

## Purpose

Close `EPIC-STRAT-MVP-001` through one visible guarded-site capture vertical slice using minimal real hex tactical combat, not a deterministic result stub.

The train remains intentionally narrow: select guarded site, launch handoff, fight a tiny real hex battle, return a real `BattleResult`, apply strategic control, and verify the visible smoke.

## Sequence

| Order | Story                                                                                                                                            | Status           | Why now                                                                 | Stop before next if                                                                       |
| ----: | ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
|     1 | [STORY-STRAT-004 Site Interaction and Guarded Battle Trigger](../stories/story-strat-004-site-interaction-and-guarded-battle-trigger.md)         | DONE / merged    | Adds visible site-marker selection and HUD Attack/Interact handoff      | Handoff is not visible, duplicate launch unresolved, or BattleSetup contract is ambiguous |
|     2 | [STORY-TAC-002 Minimal Hex Board and Stack Placement](../stories/story-tac-002-minimal-hex-board-and-stack-placement.md)                         | READY-candidate  | Establishes tiny real hex board and stack placement from BattleSetup    | Hex/placement model needs full tactical design invention or DTO mismatch appears          |
|     3 | [STORY-TAC-003 Minimal Tactical Movement and Attack Resolution](../stories/story-tac-003-minimal-tactical-movement-and-attack-resolution.md)     | READY-candidate  | Makes the tiny board playable enough to resolve a fight through actions | Movement/attack needs AP/initiative/ability complexity beyond the slice                   |
|     4 | [STORY-TAC-004 Minimal Battle End and BattleResult Return](../stories/story-tac-004-minimal-battle-end-and-result-return.md)                     | READY-candidate  | Produces real BattleResult from tactical outcome                        | Result DTO cannot validate or tactical layer starts mutating strategic state              |
|     5 | [STORY-STRAT-005 Strategic Battle Result Application](../stories/story-strat-005-strategic-battle-result-application.md)                         | READY-candidate  | Applies attacker-win: site immediately controlled                       | Reward/victory defaults require broader economy/scenario design                           |
|     6 | [STORY-LOOP-002 Visible Guarded Site Capture Smoke](../stories/story-loop-002-visible-guarded-site-capture-smoke.md)                             | READY-candidate  | Proves the full visible loop end-to-end                                 | Smoke cannot be completed, evidence is missing, or player cannot understand what happened |
|     7 | [STORY-QA-003 Guarded Site Capture Readability and Evidence Pass](../stories/story-qa-003-guarded-site-capture-readability-and-evidence-pass.md) | Draft / optional | Use only if LOOP-002 is technically complete but hard to read/judge     | N/A; this is optional closeout polish/evidence                                            |

## Implementation contract

- One story per branch/PR.
- Start from updated Unity `main` after each previous PR merges.
- Use the exact branch names in the story files.
- Read linked design docs, architecture/control docs, Unity repo `AGENTS.md`, and scoped `AGENTS.md` files before coding.
- Use TDD for production logic.
- Keep implementation story-scoped.
- Include evidence and omissions in every PR.
- Stop on draft/pending contradiction, ambiguous source authority, unrelated dirty files, failed CI, or scope expansion.

## Epic close condition

`EPIC-STRAT-MVP-001` can close when:

- STORY-STRAT-004, STORY-TAC-002, STORY-TAC-003, STORY-TAC-004, STORY-STRAT-005, and STORY-LOOP-002 are DONE/merged;
- CI passes on the final merged Unity main;
- evidence shows the guarded-site capture loop from strategic map to tactical battle to site control;
- omissions are documented;
- human review accepts the smoke as sufficient for moving larger map/bases/recruitment to `EPIC-VSLICE-MVP-002`.

## Gate status

Approved story train. Human approval recorded on 2026-06-04. `STORY-STRAT-004` is DONE / merged in Unity PR #13. Next candidate is `STORY-TAC-002 Minimal Hex Board and Stack Placement`; it remains READY-candidate until individually promoted or explicitly approved.
