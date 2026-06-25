---
title: EPIC-008 Faction Armies, Recruitment, and Role Identity Plan
type: implementation-plan
status: approved
phase: production
owner: shared
created: 2026-06-18
updated: 2026-06-25
related:
  - production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity
  - production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed
  - design/gdd/faction-unit-rosters
  - design/gdd/tactical-combat
  - design/gdd/strategic-map
---

# EPIC-008 Faction Armies, Recruitment, and Role Identity Plan

## Decision

Next epic direction is approved for planning: **Faction Armies, Recruitment, and Tactical Role Identity**.

Default settings:

- First faction pair: **Home Rule Coalition** vs **QXZ Meridian Arctic Mandate**.
- Home Rule canon posture: soft-canon / game-bridge provisional production name.
- Unit depth: 3 unit lines per faction, no upgrades yet.
- Tactical complexity: roles plus one readable status/effect.
- First status lane: QXZ `Strato Sensor Swarm` owns Sensor Lock / Marked in the next behavior slice.
- Recruitment model: fixed offers at starting hubs plus one neutral recruitment site.
- Story sizing: 4 medium-batched implementation slices + QA closeout.

## Why this epic now

EPIC-006 made tactical actions readable enough. EPIC-007 made strategic map/bases/regions readable enough. The next missing game-feel layer is army identity: factions need different units and recruitment choices so the strategic layer produces different tactical fights.

This is a better next move than a full strategic tile map, full Champion Assets/Operations, or full Intel economy because those systems need meaningful unit identities underneath them.

## Slice plan

### Slice A — STORY-ARMY-001 MVP Faction Unit Definitions and Roster Seed

Purpose:

- Stop treating stacks as cloned placeholders.
- Add the first game-facing unit definition layer and roster seed.

Scope:

- 3 Home Rule unit definitions.
- 3 QXZ unit definitions.
- 1-2 neutral guard definitions.
- Validation and lookup tests.
- Tactical setup consumes definitions where practical.
- UI/event feed displays unit names/counts.

Status:

- DONE / merged in Unity PR #60.

### Slice B — STORY-ARMY-002 Tactical Role Behaviors and Sensor Lock

Purpose:

- Make the unit definitions play differently.

Scope target:

- Melee/retaliator behavior lane.
- Ranged/recon behavior lane.
- Support/recon lane.
- One readable status/effect: Sensor Lock / Marked.
- QXZ `Strato Sensor Swarm` is the first primary Sensor Lock owner.
- Home Rule counters through positioning/local-knowledge flavor later, not in the first behavior implementation unless cheap.

Out of scope:

- Full cover/LOS/morale/damage taxonomy.
- Full faction signature mechanics.

Status:

- DONE / merged in Unity PR #61.

Human-approved default:

- Strato Sensor Swarm applies a separate 1 AP Sensor Lock support action; the next successful attack against the marked target deals +1 stack-count damage and consumes the mark.

### Slice C — [STORY-ARMY-003 Fixed Recruitment Offers and Army Summary](../stories/story-army-003-fixed-recruitment-offers-and-army-summary.md)

Purpose:

- Connect faction units to the strategic layer.

Scope target:

- Starting hubs offer fixed reinforcement/recruitment.
- One neutral recruitment site offers a fixed unit or neutral defender/recruit path.
- Army summary shows current stack composition.
- Recruited units enter tactical setup.

Out of scope:

- Town building tree.
- Weekly economy.
- Upgrades.

Status:

- DONE / merged in Unity PR #64. Human approval recorded 2026-06-19: Home Rule hub offers `settlement_watch`, QXZ hub offers `meridian_security`, neutral site attempts `survey_drones` if small, claims are one-time consumed, and counts use MVP defaults unless documented otherwise for readability.

### Slice D — [STORY-ARMY-004 Composition Consequence Scenario](../stories/story-army-004-composition-consequence-scenario.md)

Purpose:

- Prove recruitment and unit roles matter in a playable loop.

Scope target:

- One guarded site or central objective tuned to show composition effects.
- Compare starting composition vs reinforced composition.
- Post-battle summary records losses/reward/site outcome.

Out of scope:

- Full balance pass.
- Scenario editor.

Status:

- DONE / merged in Unity PR #67. Human approval recorded 2026-06-19: prove narrow Home Rule `settlement_watch` path first; require visible setup/label/loss-summary difference rather than guaranteed win/loss tuning; adapt existing guarded-site path if small otherwise create one story-scoped composition-demo guarded site; defer mirrored QXZ proof to QA/closeout unless trivial.

### Slice E — [STORY-QA-009 EPIC-008 Playtest and Closeout Review](../stories/story-qa-009-epic-008-playtest-and-closeout-review.md)

Purpose:

- Decide whether army/recruitment identity works before deeper systems.

Review loop:

1. recruit;
2. inspect army;
3. fight;
4. suffer losses;
5. return to strategic map;
6. fight with changed composition;
7. record verdict.

Possible next directions after closeout:

- Champion Assets/Operations.
- Intel/upgrades.
- deeper tactical systems.
- strategic economy/base depth.
- readability/balance repair.

Status:

- DONE / merged in Unity PR #70. Original verdict recommended `CLOSE EPIC`, but human playtest on 2026-06-25 rejected closeout because army/recruitment/tactical-role readability remains too poor to judge composition.

### Slice F — [STORY-ARMY-005 Army, Recruitment, and Map Readability Repair](../stories/story-army-005-army-recruitment-and-map-readability-repair.md)

Purpose:

- Repair the failed human playtest closeout by making army state, recruitment results, tactical stack identity, and map focus readable enough to judge EPIC-008.

Scope target:

- Selected-Champion bottom hero bar on the strategic map.
- Hero name/class/level placeholders where needed.
- Army stack slots with unit names, counts, and role hints.
- HoMM3 Tier-1-style fixed recruitment clarity for the prototype while preserving future dwelling extensibility.
- Compact tactical stack labels always visible, details on select.
- Strategic map panning/scrolling.
- Small objective contrast repair if directly tied to readability.

Status:

- DONE / merged in Unity PR #72. Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28163961946. Unity current-task pointer cleanup merged in PR #73 with post-merge CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28164738365.


### Slice G — [STORY-QA-010 EPIC-008 Repair Playtest and Closeout Review](../stories/story-qa-010-epic-008-repair-playtest-and-closeout-review.md)

Purpose:

- Re-test the repaired army/recruitment/tactical-role loop after ARMY-005 and decide whether EPIC-008 can close.

Scope target:

- Human playtest protocol.
- Closeout verdict: close epic, one narrow follow-up, or reject closeout.
- No Unity runtime changes.

Status:

- DONE / closeout rejected on 2026-06-25. Human notes: pan/zoom resets after button clicks; recruitment only increases drones once despite appearing available again; tactical drones cannot be selected/moved/utilized; stack info is not shown on tactical click.


### Slice H — [STORY-ARMY-006 Map Camera, Recruitment, and Tactical Stack Interaction Repair](../stories/story-army-006-map-camera-recruitment-and-tactical-stack-interaction-repair.md)

Purpose:

- Repair the QA-010 blockers that still prevent judging army composition after ARMY-005.

Scope target:

- Preserve strategic map pan/zoom across UI button clicks.
- Make recruitment availability/result truthfulness match the drone fixed-offer behavior.
- Make recruited tactical drone stacks selectable, inspectable, and usable/movable where current rules allow.

Status:

- READY-candidate / approval pending. No Unity implementation is authorized until explicitly approved.

### Parallel design-only brief — [Strategic Map Realism Brief](strategic-map-realism-brief-2026-06-25.md)

Purpose:

- Start deciding what a more realistic map means without authorizing map replacement implementation inside ARMY-005.

Status:

- DRAFT / design-only.

## MVP roster seed

### Home Rule Coalition

Soft-canon / game-bridge faction name. Do not use `Kalaallit` as a faction brand.

| Unit | Role | First gameplay posture |
| --- | --- | --- |
| Settlement Watch | Defensive infantry / baseline melee | holds space, retaliates |
| Sled Logistics Team | Support / mobility | support-role placeholder; later mobility/extraction/supply hooks |
| Hunter-Scouts | Recon / skirmisher | local-knowledge scout, target selection |

### QXZ Meridian Arctic Mandate

Reviewed soft-canon White Sky corporate faction.

| Unit | Role | First gameplay posture |
| --- | --- | --- |
| Meridian Security | Disciplined infantry | reliable baseline attacker |
| Strato Sensor Swarm | Ranged/recon drone | first Sensor Lock / Marked lane |
| Climate Bulwark | Heavy defender | slow, durable infrastructure protector |

### Neutral / shared

- Survey Drones.
- Site Guards.

Use both only if technically cheap; otherwise pick the one closest to current guarded-site setup.

## Guardrails

- No full faction roster.
- No upgraded unit variants.
- No full town tree.
- No full economy.
- No full Intel upgrade loop.
- No hard-canon lock beyond the accepted soft-canon production name.
- No direct use of real Greenlandic endonym/national-cultural identity as faction IP.

## Recommended approval question

`STORY-ARMY-001 MVP Faction Unit Definitions and Roster Seed` approved 2026-06-18 as the first EPIC-008 Unity implementation packet, using Home Rule Coalition as provisional soft-canon production name and the listed 3+3 roster seed.
