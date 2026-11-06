# Feasibility

This document owns CK3 evidence and acceptance criteria. The [design](design.md) owns intended player behavior; the [roadmap](roadmap.md) owns current status and next work. Keep intended behavior separate from observed game behavior.

## Existing evidence

One in-game run showed a custom window opening an event and applying a temporary +1 Advantage character modifier to the player ruler. The observation came from a screenshot; its game version and checksum are unknown. It supports only the window-to-event-to-character-modifier path. It does not demonstrate automatic battle detection, pre-combat pause control, army selection, combat impact, a battle-scoped effect, or external communication.

The ignored local game-source snapshot has unknown version provenance. Its `common/on_action/combat_on_actions.txt` comments say `on_combat_start` runs after the starting armies have joined their combat sides. The inspected GUI and script examples also show that UI actions can invoke scripted events and that character modifiers can be applied. These observations do not establish a pre-battle trigger, an army-scoped effect, or a normal-play external communication channel. Verify every relevant behavior in a recorded game build before relying on it.

## Experiment 1: pre-battle trigger and briefing

Test on a recorded CK3 build in an ordinary single-player base-game campaign. Start with no unrelated mods. Record the version and checksum from the game, enabled DLC, launcher configuration, and exact steps.

Demonstrate each intended trigger setting:

1. Every battle involving a player realm army.
2. Only battles where the ruler or a selected field commander leads an army.
3. Off.

For the enabled modes, record whether the game pauses before combat, what the player can do while paused, and how play resumes. Include a battle in an ally's war where the player is not war leader. Inspect whether CK3 exposes the battle, location, sides, armies, commanders, and war purpose in time to show a useful briefing. Test multiple player armies and commanders. The prototype need not evaluate a speech or apply a combat effect.

### Acceptance

The experiment passes only when the game opens the custom scene automatically before combat under the selected setting, pauses as intended, presents verified participants and context, and proceeds correctly when the player continues or disables the feature. Record the precise trigger and any limits. A manually opened test event or a hook that runs after combat starts does not pass.

## Experiment 2: effect target and duration

Once battle participants are available, apply a fixed test effect to all participating armies belonging to the player's realm. Confirm that allied armies, unrelated armies, and the player's other simultaneous battles do not receive it. Test when the ruler is absent, when a selected speaker is not an army commander, and when a commander is replaced. Verify how the effect expires and what a save/reload does.

The existing ruler modifier is not evidence of an army-level effect. The Advantage bonus proposed by the design remains a target until the prototype proves its scope and lifetime in combat.

## Experiment 3: exchange data with an external process

After the in-game request has a reliable identity and participant context, test a minimal controlled request and response in the same running session. Do not add speech recognition or a model; use a fixed result first. Prefer a pure-mod connection, then test an unobtrusive helper if the pure-mod route cannot meet the intended interaction. The player must not switch applications during play.

Record the actual data exchanged, transport, normal-play/debug requirements, process startup behavior, UI approach, and failure handling. Test missing helper, timeout, retry, cancellation, malformed result, duplicate result, unrelated target, and save/reload. A screenshot or successful package build alone is insufficient. Do not choose a programming language or UI framework until the required boundary has been exercised.

## Evidence to record

For each experiment, record:

- CK3 version, checksum, enabled DLC and mods, operating system, and relevant settings.
- Experiment revision and reproduction steps.
- The event timing, game context observed, and intended and actual effect targets.
- Expected and observed behavior for success, cancellation, failure, duplicate, and save/reload cases that apply.
- Screenshots or recordings that support the result, and relevant game logs.
- Known limitations and whether they prevent the intended player experience.

Remove credentials and private player data from published evidence. Keep local CK3 game files out of the repository and all distributed packages. The ignored `ck3-reference/` directory is local research material only.

## Architecture decision

Once a repeatable path supports pre-battle timing, the required context, a return result, and a bounded effect, record the chosen architecture in a new decision record. Compare the pure-mod and helper approaches against the player experience, reliability, installation, maintenance, and supported systems. A route that only works with a debug console or manual file editing is not automatically suitable for public release.

The [Voices of the Court](https://github.com/Voices-of-the-Court/VOTC) project is a reference for studying a CK3 mod used alongside a desktop application. Its [installation guide](https://docs.voicesofthecourt.app/installation/) and [source](https://github.com/Voices-of-the-Court/VOTC) are examples to investigate, not proof that their integration path meets Rally the Realm's pre-battle timing, context, effect, or privacy needs. Review its applicable license before reusing any code or assets.
