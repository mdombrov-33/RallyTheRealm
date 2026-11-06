# Technical validation plan

This document tracks what must be verified in CK3 before choosing the implementation architecture. It separates source inspection from runtime evidence and gives each test an observable pass condition. The [design](design.md) owns the player experience; the [roadmap](roadmap.md) owns project status and work order.

## Evidence standard

Game-file examples are clues, not proof that a feature works in a running build. For every runtime result, record the CK3 version and checksum, enabled DLC and mods, operating system, debug-mode status, setup, reproduction steps, and observed result. Keep screenshots or recordings that show the relevant state. Do not publish credentials, private player data, or proprietary CK3 files.

Use these labels:

- **Source-observed:** the local game files contain an example or declaration.
- **Runtime-confirmed:** the behavior was reproduced in a recorded game build.
- **Unverified:** it remains a hypothesis or has only been observed in an unidentified build.
- **Not a release path:** it depends on a debug tool or manual step that does not meet the intended player flow.

The ignored `ck3-reference/` snapshot has no recorded game version or checksum. Keep it outside commits and distributable packages. Its files are cited by path below to make the observations traceable on the local research copy.

## Findings so far

| Capability | Current evidence | What it does not establish |
| --- | --- | --- |
| Custom CK3 window and event | One screenshot from an in-game run showed a custom window opening an event. The event applied +1 Advantage as a temporary character modifier to the player ruler. | Reproducibility, game version, automatic battle timing, army scope, or combat impact. The disposable probe implementation has been removed. |
| GUI action to script | `gui/interaction_menu_window.gui:370-379` invokes a scripted GUI, and `common/scripted_guis/00_character.txt:1-7` triggers an event. | A particular custom window automatically pausing or identifying the correct battle. |
| In-game text entry | `events/_events.info:167-187` describes a custom event text widget whose `text` controller saves entered text under a named key. | That arbitrary speech text can be read by a mod effect, exported from the game, or sent to a helper. |
| Combat start timing | `common/on_action/combat_on_actions.txt:1-9` says starting armies have joined combat sides when `on_combat_start` runs. | Whether the first combat phase has advanced before a blocking event can pause the game. This hook remains a candidate to test. |
| Microphone and speech recognition | No microphone, recording, or speech-recognition interface was found in the inspected GUI, event, and script files. | That another engine API or supported external route cannot provide it. |
| External communication | No ordinary-play network, arbitrary file, or external-process interface was found in the inspected files. Script examples contain `debug_log`; its output location and usefulness as a real-time signal are unknown. | That a normal-play helper bridge is impossible. The log path is a candidate, not an established bridge. |
| Console file execution and clipboard | The console GUI has a `run` command (`gui/console.gui:188-200`); clipboard actions are attached to specific game UI objects. | A normal-play, general-purpose channel between a mod and a companion. Console `run` is a debug tool and does not qualify as a release path by itself. |

## Test setup

Before each CK3 runtime test:

1. Record the game's version and checksum from the main menu.
2. Record operating system, enabled DLC, launcher playset, display mode, and UI scale.
3. Use a disposable single-player base-game save. Start with no unrelated mods.
4. Record whether debug mode or the developer console is enabled.
5. Keep a copy of the save before the test and note any required console commands.

Run normal-play checks separately from debug-only experiments. If a result depends on debug mode, developer console, manual file editing, or switching windows, label it **Not a release path** unless the product requirements are explicitly changed.

## Test plan

### TV-01: Pause at `on_combat_start`

**Question:** Can a mod open the intended scene from `on_combat_start` and pause the game before the battle advances?

**Procedure:** In a minimal test mod, have the hook identify a battle involving the player and open a blocking event or custom window. Use opposing armies with recorded commanders and starting strengths. Capture the battle state immediately before the UI appears, while it is open, and after choosing Continue. Check game time, casualties, advantage, and battle phase. Repeat with the game unpaused and without debug mode.

**Pass when:** The scene opens automatically for the right battle; the game stops advancing while it is open; no combat progress occurs before the player finishes or skips; Continue resumes the same battle without lost time or a duplicated event.

**If it fails:** Keep the result. Test the earliest alternate trigger available in the target build. Do not conclude that all automatic timing is impossible from this hook alone.

**Status:** Not started.

### TV-02: Trigger settings and eligible battles

**Question:** Can the mod detect the intended battles and honor the player's settings?

**Procedure:** Test every battle involving a player realm army, the ruler-or-selected-commander-led mode, and off. Verify the settings appear in CK3's mod settings and persist after restart. Include an allied war where the player is not war leader. Test the ruler absent, several player armies, and armies with different commanders.

**Pass when:** Each setting opens or suppresses the scene as designed, including in an ally's war. Record any case where the game does not expose enough context to distinguish an eligible battle.

**Status:** Not started.

### TV-03: Context available before battle progress

**Question:** Which facts are available in time to brief the player and evaluate the speech?

**Inspect:** Battle identity, location, sides, participating player realm armies, allied armies, commanders for each army, war leader, war purpose and target, and any facts used by the initial rubric. Check that a battle with several armies does not merge unrelated commanders or participants.

**Pass when:** The mod can display the relevant facts accurately before the battle advances and can identify all player realm armies while excluding allied forces from the speech effect target.

**Status:** Not started.

### TV-04: Speaker and audience selection

**Question:** Can the intended ruler and field-commander modes identify the speaker and the troops addressed?

**Procedure:** Test ruler mode, field commander mode, and ask-each-battle mode. In field commander mode, choose among commanders of participating player armies. Test a ruler who is not an army commander, an absent ruler under each representative setting, and multiple player commanders in one battle.

**Pass when:** The selected speaker is stable through the interaction, the scene reaches the player's realm armies in that battle, and allied armies remain outside the effect target. Record cases where CK3's available scopes do not match this target.

**Status:** Not started.

### TV-05: In-game text capture

**Question:** Can the event text widget capture a free-form speech and preserve it until submission?

**Procedure:** Build a small test event using the documented `text` controller. Test plain text, punctuation, line breaks, the intended character limit, correction before submit, cancel, and the English character set. Check what value is available to the event's effects and whether it persists after the event closes or the game saves.

**Pass when:** Typed text is captured accurately, can be reviewed and corrected in the CK3 UI, and is available at the point needed for evaluation without relying on a companion's visible input window. Document whether the script can access raw text or only a localized-text value.

**Status:** Not started.

### TV-06: Effect scope and lifetime

**Question:** Can one result affect every participating player realm army for only the intended battle?

**Procedure:** Apply a fixed test Advantage result. Inspect the battle calculation and verify that all of the player's participating armies receive the effect while allied forces, unrelated armies, and the player's concurrent battles do not. Test commander replacement, army movement/splitting if supported, expiration, and save/reload.

**Pass when:** The visible combat calculation shows the intended effect on the intended armies and no unrelated target. Record exactly when it begins and ends. A ruler character modifier alone does not pass.

**Status:** Not started.

### TV-07: Game-to-helper signal

**Question:** Can an in-game action notify a hidden helper during ordinary play?

**Candidate to test:** Emit a unique, non-sensitive `debug_log` marker from a test event when the player uses the in-game control. Determine where it appears, whether it appears in ordinary play, how quickly it can be detected, and whether the marker can identify the current request without writing the speech or other private data to logs.

**Pass when:** A helper can reliably detect start, stop, cancel, and request identifiers in normal play without the player opening another app, using the developer console, or manually editing a file. Test missed markers, duplicate markers, stale markers after reload, and log rotation. A debug-only or unreliable log route does not pass.

**Status:** Not started.

### TV-08: Helper-to-game result

**Question:** Can a controlled result return to the same running game and reach the correct battle?

**Procedure:** After TV-07 establishes a request, test candidate return paths with a fixed result and no model. Verify the player can see the result in the CK3 experience. Exercise timeout, invalid result, cancellation, duplicate response, stale response, unrelated battle, and save/reload. Treat console `run`, debug-only clipboard controls, and manual file edits as diagnostics, not a release pass.

**Pass when:** The same game session receives a bounded result without a window switch or manual console action; the correct battle receives it once; failure or cancellation leaves gameplay unchanged.

**Status:** Not started.

### TV-09: Background microphone and transcript

**Question:** Can the hidden helper capture audio only when the in-game screen requests it and return an editable transcript to CK3?

**Procedure:** Once the game-to-helper control path exists, test start, visible recording state in CK3, stop, cancel, transcription, and transcript return with CK3 kept in the foreground. Confirm the helper does not continuously listen. Test microphone permission denied, no device, device change, silence, noisy audio, long speech, and local resource use. Confirm raw audio stays local and the transcript is not submitted until the player approves it.

**Pass when:** Every microphone action starts from and is controlled by the in-game screen; the transcript returns to that screen for correction; cancel and permission errors recover without gameplay changes; no companion speech window or app switch is required.

**Status:** Not started.

### TV-10: Provider contract and scoring boundary

**Question:** Can supported providers return a bounded, validated assessment that project rules can explain consistently?

**Procedure:** Outside the game first, exercise each candidate provider/model with the same rubric schema and varied speech examples. Validate required fields, malformed output, refusal, timeout, rate limits, and model unavailability. Record provider/model identity and result variation. Confirm the provider receives only submitted text and verified game context, never raw audio or API credentials from the game save. Then connect one provider to the fixed-result game path.

**Pass when:** Model output is schema-validated; invalid or unavailable output cannot change gameplay; project-owned rules produce the displayed score/effect breakdown; the selected model is identified; technical retry reuses the accepted result.

**Status:** Not started.

### TV-11: Full single-player flow

**Question:** Does the whole experience work without leaving CK3?

**Procedure:** In a recorded Windows build, run a qualifying battle from automatic trigger through briefing, speaker and appeal selection, typed or spoken input, transcript review, submission, score breakdown, effect, and Continue. Repeat with skip, cancellation, missing provider configuration, failed connection, and invalid model response.

**Pass when:** The player never needs to open or switch to a companion window during play; the game pauses and resumes correctly; the right battle and armies receive one bounded effect; every failure can continue without an accidental gameplay change.

**Status:** Not started.

### TV-12: Clean installation and startup

**Question:** Can a player install the mod and any required helper without manual file editing or developer tools?

**Procedure:** After the architecture is selected, test from a clean Windows user setup. Install the mod through the intended workshop flow and the helper through its planned distribution. Configure a provider and microphone, launch CK3, and enter a campaign. Restart both applications and confirm settings persist. Test helper missing, update, repair, uninstall, and API-key removal behavior.

**Pass when:** Installation and first launch follow public instructions, the in-game interaction does not require debug tools or manual files, and uninstall handles helper-owned settings and credentials according to a documented policy.

**Status:** Not started.

## Choosing an implementation plan

Write the architecture decision only after the relevant runtime tests establish the usable boundaries. The decision should identify:

- The tested CK3 version and the interaction timing it supports.
- How the game identifies the battle, speaker, audience, and effect target.
- Whether a normal-play helper bridge works, and its request and result paths.
- Whether microphone capture can be started and stopped from CK3 while the helper stays hidden.
- The effect's scope, lifetime, save behavior, and failure behavior.
- The remaining unsupported cases and whether they fit the first-release scope.
- The chosen mod and companion languages, UI/runtime frameworks, packaging, and why the tested requirements favor them.

Until these facts are established, language and framework choices remain proposals. See [feasibility](feasibility.md) for how this evidence leads to an architecture decision.

## Reference implementation to inspect

[Voices of the Court](https://github.com/Voices-of-the-Court/VOTC) combines a CK3 mod with a desktop application. Its [installation guide](https://docs.voicesofthecourt.app/installation/) and [source](https://github.com/Voices-of-the-Court/VOTC) are useful examples for research, not proof that its bridge, user interaction, or effect scope meets Rally the Realm's requirements. Record the upstream revision and review its license before reusing code or assets.
