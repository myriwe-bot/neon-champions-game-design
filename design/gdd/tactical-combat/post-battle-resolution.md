---
title: Tactical Combat — Post-Battle Resolution
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-30
updated: 2026-05-30
source_lore: []
related:
  [design/gdd/tactical-combat, design/research/tactical-combat-deep-reference]
approval: pending
---

# Tactical Combat — Post-Battle Resolution

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Post-Battle Resolution: Outcome Categories
- Post-Battle Losses and Preservation
- Post-Battle Rewards and Spoils
- Rare Capture, Resurrection, and Post-Battle Control
- Rare Recovery, Resurrection, and Faction Return Mechanics
- Post-Battle Resolution Summary UI
- Post-Battle Block MVP Cut
- End of Post-Battle Block — Integration Check

---

## Post-Battle Resolution: Outcome Categories

Approved direction:

1. Post-battle resolution uses fixed primary outcome categories with optional scenario subtitles.
2. Fixed primary outcomes provide systemic clarity and consistent player expectations.
3. Scenario subtitles provide narrative and objective-specific precision without inventing incompatible outcome taxonomies for every battle.
4. Victory has no universal grade; victory is victory by default.
5. Defeat grades are scenario-specific only.
6. Post-battle resolution uses systemic rules first, with scenario overrides where needed.

Baseline primary outcomes:

```text
Victory: the player wins the battle under the battle's core rules.

Defeat: the player loses the battle under the battle's core rules.

Retreat: the player voluntarily exits through the battle-type retreat rules.

Surrender: the player accepts a negotiated/concessionary loss through surrender rules.

Extraction Success: the player completes an extraction-type objective.

Extraction Failure: the player fails an extraction-type objective.
```

Scenario subtitle rule:

```text
A scenario may attach a subtitle or result note to the fixed primary outcome to explain what actually happened. The primary outcome drives systemic resolution; the subtitle clarifies objective, narrative, and reward/loss context.
```

Example outcome display:

```text
Victory — Data Secured
Victory — Upload Completed, Asset Exposed
Defeat — Target Escaped
Defeat — Siege Line Broken
Retreat — Army Forfeited, Champion Escaped
Surrender — Forces Preserved, Reputation Damaged
Extraction Success — VIP Extracted, Drone Wing Lost
Extraction Failure — Asset Killed
```

Design notes:

- Fixed primary outcomes prevent vague or incompatible scenario resolution logic.
- Scenario subtitles keep non-standard missions from feeling mislabeled.
- Victory should not require universal Decisive/Standard/Pyrrhic grading; scenarios can express nuance in subtitles and rewards.
- Defeat grades are not universal. If a scenario needs Rout, Catastrophic Defeat, Asset Captured, or Target Escaped, it should express that as a scenario subtitle or override.
- Systemic rules handle default rewards/losses first; scenarios may override or add specific consequences.

## Post-Battle Losses and Preservation

Approved direction:

1. After ordinary Victory, surviving allied stacks return to the army, and losses inside stacks are permanent by default.
2. Victory preserves surviving stack entities but does not automatically restore killed units.
3. After ordinary Defeat, all committed allied stacks are lost by default.
4. Surrender preserves some surviving stacks based on surrender terms.
5. Surrender should be meaningfully softer than ordinary defeat or retreat, but still costly and negotiable.
6. Post-battle unit losses can be recoverable only through faction, building, asset, repair, medbay, insurance, body-subscription, drone recovery, biotech regrowth, or similar strategic systems.
7. There is no universal free automatic recovery percentage for killed units.

Baseline rule text:

```text
Victory Preservation: after ordinary Victory, all surviving allied stacks return to the army. Units killed inside those stacks are gone unless recovered by a specific strategic recovery system.

Defeat Loss: after ordinary Defeat, all committed allied stacks are lost by default. Scenario rules may override this only when the battle explicitly defines survivor escape, extraction, capture, recovery, or special preservation.

Surrender Preservation: after Surrender, some surviving stacks may be preserved according to negotiated terms, faction rules, scenario context, enemy policy, and strategic concessions. Surrender is softer than ordinary Defeat but not free.

Unit Recovery Systems: killed units are not automatically restored. Recovery requires specific infrastructure, faction mechanics, assets, buildings, insurance, repair capacity, medbay support, biotech regrowth, drone salvage, or scenario rules.
```

Design notes:

- Victory uses HoMM-like attrition: what survives comes home; what died is gone unless a separate recovery system applies.
- Default Defeat is harsh and clear: committed stacks are lost. Retreat, surrender, and extraction are the designed alternatives for changing that outcome.
- Surrender must preserve enough to be tempting, but its cost should be visible: resources, reputation, prisoners, leverage, access, legal exposure, contracts, or strategic debt.
- Recovery/repair systems fit the cyberpunk setting, but should be strategic investments and faction identity tools rather than automatic forgiveness.
- This preserves battle stakes while leaving room for medbay, repair bay, insurance, body subscription, drone salvage, and biotech faction mechanics later.

## Post-Battle Rewards and Spoils

Approved direction:

1. Victory rewards/spoils are granted by battle, site, or scenario reward tables.
2. Victory does not use one universal flat reward for every battle.
3. Defeated enemy stacks can produce salvage, intel, samples, hardware, data, or other spoils, but collection depends on post-battle recovery/salvage capacity.
4. Captures/prisoners are rare special outcomes, not routine spoils from defeated stacks.
5. Spoils are not magically collected just because an enemy stack was defeated.
6. Casualties reduce rewards only for specific objective types.
7. There is no universal casualty penalty applied to all rewards.
8. Surrender or retreat can preserve objective rewards already secured before leaving.
9. Surrender/retreat do not grant generic victory spoils by default.

Baseline rule text:

```text
Victory Rewards: after Victory, rewards are determined by the battle, site, or scenario reward table. Different battle types and strategic-map locations define different resources, intel, access, reputation, recruits, salvage, assets, or narrative outcomes.

Spoils and Salvage: defeated enemy stacks may create recoverable spoils, but collection requires relevant post-battle capacity such as salvage teams, drones, secure transport, data extraction, biotech containment, legal cover, or scenario access.

Casualty-Sensitive Rewards: casualties reduce reward quality or quantity only when the objective defines that relationship, such as rescue missions, extraction contracts, clean raids, public-defense operations, stealth jobs, or preservation-based objectives.

Secured Objective Rewards: if the player retreats or surrenders after already securing a discrete objective reward, that secured reward may be retained unless the battle or surrender terms explicitly remove it. Retreat/surrender do not grant generic spoils by default.
```

Design notes:

- Reward tables keep strategy-map rewards readable while letting locations and scenarios differ.
- Salvage/intel should feel logistical and cyberpunk: drones, cyberware, vehicles, data cores, biotech samples, and other recoverable materials require the means to recover and process them.
- Casualty penalties should be objective-authored, not a blanket punishment for hard-won battles.
- Retreat/surrender can still recognize partial objective success, but should not become a safe way to farm battlefield spoils.
- Recovery capacity creates design space for factions, buildings, assets, Champion operations, and strategic preparation.

## Rare Capture, Resurrection, and Post-Battle Control

Approved direction:

1. Routine post-battle capture/prisoner systems are not the baseline.
2. Enemy units should rarely be captured after battle.
3. Capture may exist through specific faction mechanics, scenario objectives, unit traits, Champion skills, assets, or authored events.
4. Resurrection, recovery, reanimation, reprinting, drone re-keying, Echo restoration, biotech regrowth, or similar post-battle return mechanics may exist for some factions or skills.
5. Capture/resurrection should be exceptional and identity-driven, not a standard reward pipeline.
6. Capturing enemy assets or special units requires explicit rules and appropriate capacity/containment when used.
7. General prisoner economy and routine capture-to-recruitment are not MVP baseline systems.

Baseline rule text:

```text
Rare Capture: enemy units are not routinely captured after battle. Capture only occurs when a scenario, faction mechanic, unit trait, Champion skill, support asset, or explicit objective allows it.

Factional Recovery / Resurrection: some factions or skills may recover, resurrect, reprint, repair, re-key, regrow, or restore units after battle. These are faction identity mechanics, not universal post-battle rules.

Special Capture Capacity: when a capture or containment mechanic exists, it defines its own requirements such as transport, holding space, drone control, data isolation, biotech containment, legal cover, or scenario custody.

No Routine Prisoner Economy: ordinary victories do not create a generic pool of prisoners for recruitment, ransom, or conversion. Those outcomes require explicit mechanics.
```

MVP boundary:

```text
MVP does not need a general capture/prisoner economy. MVP may include rare authored capture objectives or faction-specific recovery/resurrection mechanics if they are central to a faction or scenario.
```

Design notes:

- This avoids capture becoming a win-more army-growth loop.
- Recruitment from defeated enemies should be rare, authored, or faction-specific rather than a standard post-battle reward.
- Cyberpunk recovery fantasy still has room: drone salvage, backup bodies, Echo continuity, biotech regrowth, contractual body replacement, or resurrection-like faction mechanics can exist where appropriate.
- The key distinction: salvage/intel/data can be common post-battle rewards; captured living units should be rare.
- Champion capture remains separate and only happens by explicit scenario rule.

## Rare Recovery, Resurrection, and Faction Return Mechanics

Approved direction:

1. Post-battle unit return mechanics can exist as faction identity tools.
2. Some factions may recover, resurrect, repair, reprint, re-key, regrow, restore, insure, or otherwise return units after battle.
3. Return mechanics may restore the same unit/stack or create a replacement depending on the faction mechanic.
4. The usual output should be a replacement unit rather than true restoration of the exact same unit.
5. True restoration can exist, but should be rarer and more identity-specific.
6. Recovery/resurrection is limited by a combination of resource cost, infrastructure/capacity, time/cooldown, and faction/scenario constraints.
7. Whether recovery/resurrection is MVP should be decided during faction roster design, not added globally.

Baseline rule text:

```text
Faction Return Mechanic: a faction, Champion skill, asset, building, doctrine, or scenario may define a way for some lost units to return after battle. This is not a universal post-battle rule.

Replacement Output: most return mechanics create a replacement unit/stack rather than restoring the exact original. The replacement may represent repaired drones, contract replacement bodies, backup-grown biotech, reprinted shells, fresh recruits from an insurance pool, or other faction-specific continuity.

True Restoration: some rare mechanics may restore the same unit/stack identity, such as Echo continuity, preserved control cores, elite body recovery, or named/special unit restoration. These should be exceptional.

Return Limits: every return mechanic defines its cost and bottleneck, such as resources, repair bays, med/clone capacity, drone control, biotech vats, data backups, legal insurance, cooldowns, strategic time, or scenario restrictions.
```

MVP boundary:

```text
Do not add global recovery/resurrection to MVP by default. Include a simple version only if an MVP faction, scenario, or Champion identity requires it.

Faction roster design decides whether a faction needs a return mechanic and what form it takes.
```

Design notes:

- This preserves attrition while allowing cyberpunk identity mechanics.
- Replacement is the safer baseline because it avoids erasing losses completely while still supporting continuity fantasy.
- True restoration should feel special and may matter more for elite/special units than ordinary stacks.
- Strong return mechanics need strong bottlenecks or they will flatten post-battle consequences.
- Examples: drone repair pool, corporate body-insurance replacement, biotech regrowth, Echo-backed continuity shell, re-keyed autonomous unit, medbay survival protocol, faction-specific resurrection analogue.

## Post-Battle Resolution Summary UI

Approved direction:

1. The post-battle result screen should always show outcome, stack losses, rewards, objectives, assets at risk, and recovery/return effects.
2. The result screen should show why losses, rewards, missed rewards, recovery, salvage, forfeiture, and asset consequences happened.
3. Major unavailable or failed rewards should be shown with the reason they were missed.
4. Minor missed micro-salvage does not need to clutter the result screen.
5. The result screen should preview only available strategic follow-up actions.

Baseline result-screen sections:

```text
Outcome: fixed primary outcome plus optional scenario subtitle.

Objectives: secured, failed, partial, contested, or scenario-specific objective results.

Army Losses: surviving stacks, lost units inside surviving stacks, destroyed/lost committed stacks, routed/removed stacks where relevant.

Rewards and Spoils: resources, access, intel, reputation, recruits, salvage, assets, or other rewards gained.

Missed Major Rewards: important rewards or spoils not gained, with reasons such as no salvage capacity, objective failed, retreat forfeiture, surrender terms, enemy escape, asset destroyed, or time expired.

Assets at Risk / Asset Consequences: committed Champion assets, support assets, drone wings, transports, safehouses, channels, or special systems lost, damaged, exposed, preserved, or recovered.

Recovery / Return Effects: factional recovery, repair, replacement, resurrection, insurance, drone salvage, biotech regrowth, Echo restoration, or other return mechanics that apply.

Available Follow-Up Actions: only actions the player can actually take next, such as repair, recover, replace, debrief, process salvage, assign medbay, trigger insurance, continue, or resolve scenario-specific aftermath.
```

Reason-line examples:

```text
Army Forfeited: Retreat from field battle forfeits committed stacks.
Salvage Missed: No drone recovery team assigned.
Objective Reward Secured: Data core extracted before retreat.
Asset Exposed: Operator channel was committed and traced.
Replacement Available: Corporate body-insurance pool can replace 3 lost units next strategic turn.
Recovery Blocked: Biotech containment capacity full.
```

Design notes:

- Result UI must make consequence channels legible: outcomes, objectives, stack losses, assets, rewards, missed major rewards, and recovery effects.
- Always explain why important consequences happened. This prevents retreat, salvage, surrender, and recovery systems from feeling arbitrary.
- Show major missed rewards as teaching moments, but avoid spam for tiny salvage fragments.
- Follow-up actions should be actionable, not encyclopedic. If the player cannot do it now, hide it or put it in a detail tooltip.

## Post-Battle Block MVP Cut

Approved direction:

1. MVP post-battle resolution includes outcome, stack losses, basic rewards, secured objective rewards, missed major rewards, asset consequences, and result screen presentation.
2. Rare capture is post-MVP by default unless specifically required by a scenario, faction, skill, or asset.
3. Complex salvage capacity and complex asset consequence chains are post-MVP by default.
4. Faction return/recovery/resurrection mechanics are not globally post-MVP or MVP by default; inclusion is decided during faction roster design.
5. MVP salvage capacity should be numeric rather than only binary.
6. MVP includes asset-at-risk reporting if assets exist in MVP.

Baseline MVP contract:

```text
MVP Post-Battle Resolution: resolve and display the primary outcome, optional scenario subtitle, stack losses, basic reward table results, secured objective rewards, missed major rewards, asset consequences, and available follow-up actions.

MVP Salvage Capacity: MVP may use a simple numeric salvage capacity to limit how much salvage/spoils can be recovered. This should be lightweight and readable, not a full logistics simulation.

MVP Asset Reporting: if assets can be committed in MVP, the result screen must report whether committed assets were preserved, damaged, lost, exposed, recovered, or otherwise affected.
```

Post-MVP defaults:

```text
Rare Capture: post-MVP by default, except for authored scenario/faction/skill/asset needs.

Complex Salvage Logistics: post-MVP by default. MVP numeric salvage capacity should not require deep transport, legal, personnel, quarantine, and processing chains unless a scenario needs them.

Complex Asset Consequence Chains: post-MVP by default. MVP should report direct asset consequences, but deeper follow-on chains can wait.

Faction Return Mechanics: decided during faction roster design. Add to MVP only if an MVP faction's identity depends on it.
```

Design notes:

- This keeps post-battle resolution useful in MVP without implementing the entire aftermath economy.
- Asset consequences are MVP-relevant if assets are MVP-relevant; do not hide them if they exist.
- Numeric salvage capacity gives more tuning control than a binary support flag, but should stay simple.
- Rare capture remains explicitly outside the normal MVP reward loop to avoid snowballing.
- Recovery/resurrection remains faction-driven, not a global tactical-combat requirement.

## End of Post-Battle Block — Integration Check

Approved direction:

1. Post-battle resolution is listed in MVP scope as a compact post-battle resolution/result screen bullet.
2. General capture/prisoner economy is explicitly out of scope for MVP.
3. Rare authored or faction-specific capture can still exist when required by a scenario, faction, skill, or asset.
4. Faction return/recovery/resurrection mechanics are roster-design dependent, not globally included or excluded.
5. The next design area after post-battle resolution is army composition and deployment rules.

Integration notes:

- MVP Scope now includes post-battle resolution/result screen: outcomes, stack losses, basic rewards, secured objectives, missed major rewards, and asset consequences where assets exist.
- Out of Scope for MVP now includes general capture/prisoner economy.
- Out of Scope for MVP now also clarifies that global recovery/resurrection/return mechanics are not default; faction-specific return mechanics are decided during roster design.
- This closes the post-battle block and sets up the pre-battle counterpart: what army is brought, how stacks are selected, and how deployment works.
