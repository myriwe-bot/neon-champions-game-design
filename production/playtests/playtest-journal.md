---
title: Playtest Journal
type: playtest
status: active
phase: production
owner: shared
created: 2026-07-05
updated: 2026-07-24
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

## [2026-07-24] post-launch-repair unaided owner playtest — REJECT CLOSEOUT / DESIGN RESET REQUIRED

- Build / commit / PR: local Windows standalone built from Unity `main` after PRs #186-#188; instructed source head `8dad95d2854f26a7445f8ea1b3fb2dc4f3e08ae5`, but the tester did not paste an independent build hash.
- Scenario / mode: ordinary Explorer launch; QXZ; unaided title and first-ten-minute strategic-map route. Test stopped after the first section because the experience was not judgeable as fun.
- Tester / role: human owner / solo unaided playtest.
- Story / epic under review: post-EPIC-018 continuity and whole-prototype direction.
- Evidence: direct structured human report. Screenshots/video are neither supplied nor requested for this design-reset verdict.

### What worked technically

- Explorer launch reached a usable window within a few seconds.
- The window was not black, blank, frozen, or visibly at the wrong resolution.
- Text was not generally overlapping or clipped.

### What dragged

- The title reads as gameplay UI with a much smaller title box layered over it; the map and shell remain visible behind `White Sky Calibration failure` and `New Scenario`.
- The shell is overcrowded, map elements look like similar buttons, and the lower bar presents too many choices.
- Movement is complicated and its rules are not understood.
- The feed repeatedly says `Action unavailable` without creating useful understanding.
- The base cannot be reopened or found after the Champion moves away; buildings are not presented as clear, accessible physical structures.
- `Stratospheric Lab`, `specialists`, `Effect: Starting-hub support`, `Verify Lead`, and the Weather Station interaction do not communicate a coherent player purpose or consequence.

### What confused

- The objective was unclear immediately.
- Turn ownership was inferred only from whether actions appeared possible.
- The Champion was hard to identify because the frame was overwhelmingly blue.
- Building `Stratospheric Lab` looked like a meaningful first decision, but its purpose and recruitment promise were not understood.
- The player expected to recruit units and instead lost access to the base after moving.
- The map read as a complicated node-and-edge graph, not a physical Arctic place or an isometric strategy/adventure map.

### What felt off-fiction and off-product

- The game does not look or feel like the discussed product or its inspiration games.
- Preliminary art is not functioning as readable game art.
- Vague objective/direction text and unexplained systems read as generated filler rather than authored strategy-game choices.
- The current implementation does not reveal a legible core loop or a source of fun.

### Exact complaints to preserve

- “There is a very big problem here.”
- “The game does not look or feel like anything we have discussed, definitely not like the games that give it inspiration.”
- “Movement is complicated, art is hard to read, bases cant even be opened.”
- “The text and the ‘objectives’ are confusing, not simple in any way.”
- “Something has got to change radically.”
- “This is quite shit.”
- “We need to turn this into a normal isometric-type view game where even if art is preliminary, it is still understandable.”
- “Bases need to be accessible and haver clearly defined buildings.”
- “There may have been assumptions baked in here that are not fixed.”
- “I do not understand at all what the game loops are supposed to be or where the fun should be.”
- “There are way too many buttons to click and options to choose.”
- “It is not fun AT ALL.”
- “I started as QXZ and built a ‘Stratospheric Lab’, even though I do not understand what id does.”
- “I also do not think we have designed these buildings together....”
- “I tried to ‘verify lead’, did not understand why I am doing it or what it did.”
- “I went to ‘Weather station’ and clicked on something, got some AI slop text in return.”
- “I do not understand what I am doing and this is DEFINITELY not fun and not fitting with the design.”
- “Straight away.”
- “See above - complete chaos.”
- “A node and edge graph and very complicated.”

### Fun verdict

- REJECT CLOSEOUT — the build launches, but the title, map metaphor, base interaction, information hierarchy, authored content, first-turn purpose, and core fun loop all fail the unaided human gate. This is not a narrow polish/readability defect.

### Gate consequence

- Stop feature throughput and do not ask the owner to continue this playtest route on the same design surface.
- Reopen design basics: player fantasy, first-session core loop, meaningful decisions, map/movement metaphor, base/building interaction, objective framing, and information hierarchy.
- Treat a normal readable isometric-type physical map, directly accessible bases, and clearly defined buildings as explicit owner direction for the reset—not as approval of a specific technical implementation yet.
- Remove or quarantine unexplained prototype content such as `Stratospheric Lab`, `Verify Lead`, and vague generated consequence text unless it can be traced to newly approved design authority.
- No screenshots or video are required from this solo playtest.

## [2026-07-23] STORY-STANDALONE-DISPLAY-001 — REJECT / launch-context blocker

- Build / commit / PR: Unity `main` `b0ea56ad2998421464baadee3bfbd32a16790ec0`; executable SHA-256 `E83058C236F35A720C27E465DC42D1549F13B25A8573DCE464438B855764E7AF`.
- Scenario / mode: ordinary Explorer/executable-directory launch versus repository-root `Start-Process`; no `-screen-*` arguments.
- Tester / role: human owner / 2560x1440 two-monitor Windows machine.
- Story / epic under review: `STORY-STANDALONE-DISPLAY-001` / EPIC-018.
- Evidence: direct human report, read-only `Screenmanager *` inventory, state `Title|faction_1|846|632|0`, player log, and controlled working-directory A/B launches.

### What dragged

- Explorer and explicit executable-directory working-directory launches showed the Unity splash, then a gray window that became black when resized.
- The broader HRC/QXZ and continuity route remains unexecuted because normal launch is still player-blocking.

### What surprised

- The exact same no-screen-argument executable opened from repository-root working directory.
- `-logFile` only and `-logFile` plus smoke signal both opened from repository root; smoke signal was not required.
- Saved display values already described a visible on-screen 1920x1080 windowed launch, so registry deletion was rejected as unnecessary and speculative.

### Exact complaints to preserve

- “Window color: grey originally, black when resized. Window visible. Window resizable.”
- “On the same monitor, when tests run, the game opens just fine.”
- “A — EXE DIRECTORY: splash then gray/black  B — REPOSITORY ROOT: title opened.”

### Fun verdict

- REJECT — the player depends on repository-root current working directory, while CI inherits that successful context and masks normal distribution behavior.

### Next decision

- Human approved `STORY-STANDALONE-LAUNCH-CONTEXT-001` through implementation merge, followed by one exact-machine Explorer double-click gate.
- No registry, graphics API, renderer, gameplay, or continuity scope expansion.

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
