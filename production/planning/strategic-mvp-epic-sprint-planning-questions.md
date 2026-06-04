---
title: Strategic MVP Epic/Sprint Planning Questions
type: planning
status: draft
phase: production
owner: shared
created: 2026-06-04
updated: 2026-06-04
source_lore: []
related:
  [
    design/gdd/strategic-map,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger,
    production/stories/story-strat-005-strategic-battle-result-application,
  ]
approval: pending
---

# Strategic MVP Epic/Sprint Planning Questions

## Current read

`EPIC-STRAT-MVP-001` has already delivered the foundation slice:

- scenario/map graph state;
- hotseat turns;
- Champion route movement;
- minimal strategic presentation/input/HUD;
- two-faction hotseat smoke;
- two QA/readability passes;
- battle setup/result DTO boundary.

The user clarified the next desired direction on 2026-06-04:

- next work should be a visible vertical slice, not a domain-only packet;
- guarded neutral site victory should immediately control the site;
- the desired near-future demo should move toward a larger map with cities/bases, recruitment, tactical combat, and neutral-site capture.

Clarification of earlier option A:

> "Strategic battle consequence works" means the player can interact with a guarded neutral site on the visible strategic map, launch a battle handoff, receive/apply a battle result, and then see the strategic map change: the site becomes controlled, rewards/result summary update, and the Champion/army state reflects the outcome. It does not necessarily mean a full tactical battle is playable yet.

The current epic should therefore be treated as a vertical-slice bridge, not just architecture. It should close only after a visible guarded-site capture loop is demonstrable.

## Proposed epic sizing rule

Use epics as capability slices that end in a demonstrable player/system behavior, not as huge feature categories.

Recommended size:

- 4-8 implementation stories plus optional QA/story-hardening stories.
- 1 clear playable or testable milestone.
- 1-3 weeks of agent execution at current cadence, depending on CI/review friction.
- Ends with a mergeable demo/checklist, not just architecture.

If an epic needs more than ~8 implementation stories, split it. If it cannot be demonstrated, it is probably a planning theme, not an epic.

## Candidate next epic shapes

### Option A — Finish Strategic Battle Consequence Loop

Goal: a guarded site can be selected, battle handoff generated, battle result applied, and visible strategic consequences appear.

Likely stories:

- STORY-STRAT-004 site interaction and guarded battle trigger.
- STORY-STRAT-005 strategic battle result application.
- STORY-LOOP-002 guarded-site loop smoke / evidence pass.
- STORY-QA-003 readability/feedback for battle handoff and result summary.

Best if the next milestone is: "the strategic map finally has consequence."

### Option B — Minimal Tactical Battle Execution

Goal: replace DTO-only handoff with the smallest tactical encounter that can produce a real `BattleResult`.

Likely stories:

- tactical encounter scene/minimal board setup;
- unit stack placement from `BattleSetup`;
- minimal combat resolver/AI or deterministic smoke battle;
- return `BattleResult` to strategy.

Best if the next milestone is: "I can enter a real fight, even if ugly."

### Option C — Strategic Economy + Recruitment Loop

Goal: make sites matter before/after battle through Credits/Materials/Intel and reinforcement choices.

Likely stories:

- resource stockpile visibility and deltas;
- one-time and/or recurring site rewards;
- recruitment/reinforcement offer contract;
- minimal reinforcement interaction smoke.

Best if the next milestone is: "the map has reasons to race and contest."

### Option D — Scenario Objective/Victory Loop

Goal: make the two-faction scenario end cleanly through central objective or Champion defeat.

Likely stories:

- central objective control/progress;
- Champion defeat scenario loss;
- victory HUD/summary;
- playtest checklist.

Best if the next milestone is: "a small match can be won or lost."

## Planning questions for human decision

1. What should the next sprint prove to you as a player/designer?
   - A: strategic battle consequence works;
   - B: a tiny tactical battle exists;
   - C: economy/recruitment makes map choices meaningful;
   - D: match victory/loss works;
   - or another goal.

2. Should `EPIC-STRAT-MVP-001` close after STORY-STRAT-004/005 plus a smoke/QA pass, or should it remain open until a full map-to-battle-to-result playable loop exists?

3. For guarded neutral sites, what feels better for first MVP?
   - Win battle = site immediately controlled and reward granted.
   - Win battle = guards cleared, then player must claim/collect separately.
   - Hybrid: immediate for simple resource sites, separate interaction for central/recruitment sites.

4. Should the next sprint stay domain/test-heavy, or should it include a visible Unity scene/UI path even if rough?

5. How large do you want sprints to be in practice?
   - 1 story + review/merge;
   - 2-3 tightly related stories;
   - a small vertical slice ending in one demo/QA packet.

6. What is your preferred epic promise format?
   - Player-facing promise: "A player can do X."
   - System-facing promise: "The architecture supports X safely."
   - Playtest-facing promise: "We can test whether X is fun."

7. What is the next meaningful demo you want to see before we build more infrastructure?

## Recommendation after user clarification

Recommended current vertical slice:

> A player uses the visible strategic map to select a Champion, move to a guarded neutral site, choose an explicit site interaction, launch the battle handoff, apply a test/stubbed battle result, and see the neutral site become controlled.

Recommended remaining stories for `EPIC-STRAT-MVP-001`:

1. `STORY-STRAT-004` — visible guarded-site interaction and battle handoff.
2. `STORY-STRAT-005` — apply guarded-site battle result; attacker win immediately controls the site.
3. `STORY-LOOP-002` — visible guarded neutral site capture smoke, using the smallest acceptable tactical/result stub until real tactical combat exists.
4. Optional `STORY-QA-003` — readability/feedback pass only if the smoke is hard to understand.

Recommended next epic after that:

> `EPIC-VSLICE-MVP-002 Larger Map, Bases, Recruitment, and Minimal Tactical Combat`

Proposed promise:

> A player can play a small but legible two-faction map with bases/cities, recruit/reinforce at a site, capture neutral sites through tactical combat, and see enough strategic consequences that the HoMM-like MVP loop is testable.

This should include tactical combat before deep economy polish, because neutral-site capture without a real fight will feel fake quickly. Recruitment should be simple and visible, not a full town system.
