# Roadmap

This roadmap tracks evidence and working software. A planned milestone is not complete because its scripts compile, its package builds, or a screenshot resembles the intended interface. Record the game version, test setup, steps, and observed result for each in-game milestone. See [feasibility](feasibility.md) for evidence standards and open integration questions.

## Current state

**Project phase:** product baseline and feasibility.

**Implementation:** no playable speech mod or companion application.

**Observed CK3 behavior:** one in-game run showed a custom window opening an event and applying a temporary +1 Advantage character modifier to the player ruler. The game version and checksum were not recorded. This does not prove automatic battle timing, army targeting, combat impact, or external communication; see [feasibility](feasibility.md).

**Next work item (`not_started`):** prototype automatic detection of a battle involving a player realm army, pause before combat, and show participating armies and commanders. Keep AI, microphone, and speech scoring out of this slice.

The ignored `ck3-reference/` folder is a local game-source snapshot with unknown version provenance. It is research material, not project source; keep it out of commits and distributable packages.

## Next: prove the pre-battle scene

Build a focused in-game prototype that detects a battle involving a player realm army, pauses before the fight begins, and presents a briefing with the participating armies and commanders. It should cover the case where the player's realm joins an ally's war but the player is not war leader. Keep AI, microphone, and speech scoring out of this prototype.

The supplied source snapshot says `on_combat_start` runs only after the battle has started and its starting armies have joined their sides. That hook cannot by itself deliver the required pre-battle pause. The prototype must test another trigger path in the actual game build. Mark the item complete only after the scene opens automatically at the intended time, its context is correct, and the player can continue safely.

## Planned milestones

### 1. Identify the battle and pause before combat

Demonstrate the configurable trigger in a single-player base-game campaign. Verify an every-player-realm-army mode, a ruler-or-commander-led mode, and off. Verify the pause and continue flow, including an allied war where the player is not the war leader. Record which context CK3 actually exposes before the battle.

### 2. Establish speakers, audience, and effect scope

Verify ruler and participating field-commander choices, including several player armies with different commanders and a speaker who is not commanding an army. Test the absent-ruler setting. Demonstrate that a successful fixed test result affects all participating player realm armies in that battle, excludes allies and unrelated armies, and expires as intended. Do not infer army scope from a ruler modifier.

### 3. Prove the external round trip

Test a controlled request and response while CK3 remains in the same running campaign. Start with a pure-mod route. If it cannot satisfy the interaction, test a background helper that stays out of the player's way. Compare normal-play requirements, reliability, installation burden, supported platforms, and maintenance cost. Keep the player inside the game for the entire flow. Exercise failure, retry, cancellation, duplicate response, and save/reload behavior. Choose languages and application frameworks only after this boundary is demonstrated.

### 4. Design and calibrate the speech assessment

Use the verified game context and the initial four rubric dimensions to build a collection of varied speech examples, including strong, bland, inaccurate, contradictory, funny, and emotionally effective attempts. Define factor scales, weights, score labels, repeat-use handling, and the score-to-Advantage curve. Check that the breakdown matches the calculation and that different supported models stay within acceptable gameplay variation. Treat all numerical examples as proposals until this work is complete.

### 5. Build the speech vertical slice

Connect the in-game scene to one provider and a controlled set of verified context facts. Validate structured model output and apply only project-owned effects. Keep API credentials outside CK3 saves. Show the briefing, selected appeal, model assessment, factor explanations, exact effect calculation, and recovery paths in the pause screen.

### 6. Add both speech inputs

Provide typing and local microphone transcription in the release build. Let the player start and stop recording, review and correct the transcript, and explicitly submit it. Keep audio local, show a character counter, discard audio and transcript according to the privacy behavior in the [design](design.md), and verify that both input paths use the same rubric.

### 7. Prepare a public release

Test the Windows build in the base game and document the exact supported CK3 version. Check installation and update steps for GitHub and the selected workshop. Review bundled assets and provider requirements, complete the license decision, and write player-facing setup, privacy, troubleshooting, and compatibility guidance. Broader OS, DLC, popular-mod, and non-battle support can follow based on testing and player interest.

## Release boundary

The first release is single-player, Windows-first, English-language, base-game-focused, and battle-focused. It includes typed and spoken input, multiple major hosted providers, and multiple supported models per provider. It does not include AI-written speeches, local/offline language models, multiplayer, or non-battle speech scenes. These boundaries describe the target, not features already implemented.
