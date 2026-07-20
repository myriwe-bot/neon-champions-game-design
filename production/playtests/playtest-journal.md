---
title: Playtest Journal
type: playtest
status: active
phase: production
owner: shared
created: 2026-07-05
updated: 2026-07-20
source_lore: []
related:
  [
    production/stories/story-playtest-001-playtest-journal-and-gate-hook,
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    production/gates/review-mode,
    production/gates/gate-template,
    docs/architecture/testing-strategy,
  ]
approval: approved
---

# Playtest Journal

## Purpose

This journal makes playtest feel notes first-class production evidence. Use it for human/director playtests, agent-run closeout reviews, and any subjective readability/fun verdict that would otherwise live only in chat.

Recorded notes are source authority for future repair stories when they preserve exact player complaints. Do not smooth sharp complaints into generic UX language.

## Rules

- Keep dated entries append-only unless correcting a factual link/commit typo.
- Preserve exact human complaints in quotes when available.
- Separate observed player friction from proposed fixes.
- Link the build/commit, scenario, story/epic under review, and evidence path.
- Every closeout/playtest story must link one or more journal entries, or explicitly state why playtest evidence is N/A.
- Terse notes are valid. A short exact complaint is better than a polished paraphrase.

## Dated entry template

Copy this section for each playtest.

```markdown
## [YYYY-MM-DD] <story/epic/build> — <short verdict>

- Build / commit / PR:
- Scenario / mode:
- Tester / role:
- Story / epic under review:
- Evidence path / screenshots / video:

### What dragged

-

### What surprised

-

### What confused

-

### What felt off-fiction

-

### Exact complaints to preserve

- "..."

### Fun verdict

Choose one and add a sentence:

- KEEP — works well enough; continue.
- REVISE — promising but needs a narrow repair.
- REJECT — does not prove the intended experience.
- RETEST — evidence was inconclusive or setup was invalid.

### Next decision

- Close story/epic:
- One narrow follow-up:
- Broader direction decision:
- N/A with reason:
```

## Gate summary format

When a gate or closeout story references playtest evidence, summarize it like this:

```markdown
Playtest evidence:
- Journal entry: `production/playtests/playtest-journal.md#[YYYY-MM-DD]-...`
- Build / commit:
- Verdict: KEEP / REVISE / REJECT / RETEST
- Exact preserved complaints, if any:
  - "..."
- Gate consequence:
```

## Existing preserved complaint seeds

These are not retroactive full journal entries; they are exact complaint seeds already used as acceptance authority before the journal existed. Future entries should quote the relevant dated playtest section instead of scattering complaint text across stories.

### STORY-QA-004 map scale / zoom / UI clarity

Source: `production/stories/story-qa-004-playability-map-scale-zoom-and-ui-clarity-pass.md`.

- "The strategic map is still tiny and unreadable."
- "Text labels overlap themselves."
- "Buttons are obstructed by text."
- "The prototype is very confusing."
- "There is no zoom."
- "It is hard to understand what is clicked."
- "It is hard to understand what buttons do."

### STORY-QA-006 state/action feedback readability

Source: `production/stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass.md`.

- Strategic turn ownership: “Not really” clear whose turn it is.
- Strategic position/state: selected Champion is visible, but with some nodes “it is unclear” where the Champion is.
- Reachability: mostly visible, but route/node meaning is only “somewhat” clear.
- Guard/site state: guarded vs unguarded is unclear; site/objective state is not meaningful enough.
- Turn changes: “I am unsure what changes each turn.”
- Tactical current actor: “No” — the active stack is not clear, and both stacks appear selectable.
- Tactical sides/targets: friendly vs enemy is “not really” clear; legal attacks are not clear; attacking feels like selecting the other army.
- Tactical results: attack/damage/result feedback is not understood.
- Champion Command: ability availability is visible, but what abilities do and why denials happen is not understood.
- UX blockers explicitly selected: clickable affordances, denial reasons, result feedback, and battle completion/attack understanding.

### EPIC-008 / STORY-ARMY-005 army and recruitment readability

Source: `production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md` and `production/stories/story-army-005-army-recruitment-and-map-readability-repair.md`.

- "I would not know how to create a composition or how to view it, so no. It is completely unreadable right now."
- UI is still hard to read and cluttered.
- Dark top-screen hue hurts objective readability.
- Map cannot be moved/panned, making focus annoying.
- Player cannot see or understand their army, units, stacks, roles, or composition.
- Recruitment/dwellings only say “recruited” and do not explain unit type/count/cost/future dwelling model.
- Tactical roles and stack differences are invisible.

### STORY-UX-002 tactical scale / resources / stack clarity

Source: `production/stories/story-ux-002-tactical-playability-scale-resource-hud-and-stack-clarity.md`.

- "Resource use is unclear, resources are not displayed anywhere."
- "Unit stacks also unclear."
- "Tactical area still small."
- "central objective situation seems broken - champion is directed away from the point. Holding is not possible."
- ""Engage CHampion" option is incorrectly displayed there. Cannot attack guard or take control over objective."
- "Also, champion-on-champion combat is not working."

### STORY-QA-007 Champion encounter initiation clarity

Source: `production/stories/story-qa-007-champion-encounter-initiation-clarity.md`.

- Moving into the same area does not clearly trigger battle.
- Movement may be blocked.
- Enemy Champion interaction can feel like selecting the other Champion.

### STORY-CMD-005 command explanation

Source: `production/stories/story-cmd-005-champion-command-explanation-pass.md`.

- Rally Order availability is visible, but what it does is unclear.
- Rally Order denial/result is not understood.
- Drone Strike availability is visible, but what it does and target meaning are unclear.
- Second-use denial is not understood.
- Rally Order and Drone Strike do not yet feel differentiated.
- Marshal vs Operator identity is not yet clear.

## [2026-07-20] STORY-PROTOTYPE-CONTINUITY-QA-002 — REJECT / BLOCKED

- Build / commit / PR: Unity `main` `91443c87e7f68241403cb1004c4acb0f12c07089`; gameplay implementation from PR #176. Executable SHA-256 was not supplied during the partial run.
- Scenario / mode: ordinary Windows standalone launch versus diagnostic CI-style forced 1920x1080 window launch.
- Tester / role: human owner / high-resolution Windows machine.
- Story / epic under review: `STORY-PROTOTYPE-CONTINUITY-QA-002` / EPIC-018.
- Evidence: direct human report plus pasted forced-launch player log; no valid HRC/QXZ or continuity captures were reached.

### What dragged

- Ordinary double-click launch showed the Made with Unity splash and then a black window.
- The first required replaytest step failed, so no broader discovery or continuity result is claimed.

### What surprised

- The same executable opened normally on the same machine when forced to a 1920x1080 window, matching CI’s launch policy.
- The log showed normal Unity, D3D12, Mono, PhysX, and Input System initialization without a fatal error.

### What confused

- CI was green because it always supplied safe screen arguments; it did not prove normal player launch.
- Project settings combine 1024x768 defaults with native-resolution startup, non-resizable windows, and fullscreen mode 1.

### Exact complaints to preserve

- “For some reason my machine does not open the build. It shows the made with unity splash but after that gives a black screen.”
- “It is running windowed, my display is actually much larger in resolution.”
- “The window properly pops open on the same machine when the tests run.”

### Fun verdict

- REJECT — normal player entry remains blocked; forced-resolution command-line launch is diagnostic evidence, not an accepted workaround.

### Next decision

- Keep EPIC-018 active.
- Review/approve one bounded safe-default-window and no-arguments-launch-parity repair candidate.
- Repeat the human recovery continuity replaytest after repair.

## [2026-07-17] STORY-PROTOTYPE-CONTINUITY-QA-001 — REJECT / BLOCKED

- Build / commit / PR: local Windows build prepared after Unity pointer PR #167; exact local build SHA was not reported. Activated Unity `main` pointer commit: `ab6e7b823a8aaec48f619b0b0ca4f605767a2f82`.
- Scenario / mode: attempted standalone title-to-HRC continuity route; partial HRC Editor play after manual bootstrap setup.
- Tester / role: human owner / first playtester.
- Story / epic under review: `STORY-PROTOTYPE-CONTINUITY-QA-001` / EPIC-017.
- Evidence path / screenshots / video: direct human report in session; no new truthful capture package supplied.

### What dragged

- Standalone showed the Unity splash and then a gray window.
- The Editor path required manually adding `Strategic Map Bootstrap`.
- Map readability and discoverability blocked further testing.

### What surprised

- `New Scenario` -> `Play HRC` worked in the Editor workaround.
- Opponent movement after End Turn was visible and understood; it moved toward nodes.

### What confused

- Champion army/inventory/stack inspection could not be found.
- `Sled Logistics Team x5` and `Mobility support` were visible, but the role meaning was unexplained.
- Clicking the base, including with `Inspect` selected, did not expose construction or upgrade interaction.
- White text was unreadable against gray/light-blue map geometry.
- The meaning of the polygons and the intended next action were unclear.

### What felt off-fiction

- The visible map read as an abstract node/polygon diagram rather than a physical Arctic frontier with infrastructure, routes, bases, and sites.
- The title copy `White Sky Calibration failure` was stylistically acceptable but sounded AI-written; copy revision is later work, not the current blocker.

### Exact complaints to preserve

- "There seems to be no interactivity whatsoever."
- "The readability on the map is horrible."
- "I have no idea what do do."
- "The map is very strange and text is unreadable, it is in general a mess."
- "Base cannot be oponed or upgraded."
- "Also it seems that we are still using a node map based system."

### Fun verdict

- REJECT — usability and standalone-entry failures prevented the intended continuity and core-loop experience from being judged.

### Next decision

- Close story/epic: close the QA execution as DONE / REJECT; do not close EPIC-017 as a successful human gate.
- One narrow follow-up: `STORY-STANDALONE-ENTRY-001` first.
- Broader direction decision: approved physical Arctic adventure map over the hidden authored corridor graph; no visible polygon/node metaphor; defer full tile/hex movement.
- Next visual gate: one representative map-and-shell vertical slice before whole-map rollout.
