# Feasibility milestone

Demonstrate one complete speech-related interaction between CK3 and an external process before implementing speech recognition or model evaluation. The experiment must obtain real game context, return a controlled result, and apply a visible effect to the intended target while the player stays in the game.

**Status:** Not started. No integration experiment has been run, and no CK3 capability has been verified for this project.

This document owns the current milestone. The [design](design.md) defines the desired experience; the experiment determines which implementation can support it.

## Research questions

Investigate these questions in order, using the installed game version, relevant modding documentation, and inspectable implementations:

1. Can a player-initiated pre-combat interaction identify a speaker and army, and keep the game paused?
2. Can the mod expose enough real context for an external process to identify that interaction and its participants?
3. Can an external result be received during the running session and applied through game scripting?
4. Which effects can be scoped to the intended character, army, or engagement, and how do they expire?
5. Which interface approach lets the player initiate the interaction and inspect the result without switching applications?

Custom game UI, a background helper, and an overlay are candidates. An interface displayed over CK3 does not by itself establish native support for recording audio or calling an API. Integration methods should be assessed on reproducibility, installation burden, maintenance cost, and their effect on ordinary play.

## Experiment

Build the smallest mod and external process needed to test the round trip. Use a fixed or manually selected result with a known, limited effect. The experiment does not need a microphone, transcription service, model, evaluation rubric, or polished calculation animation.

Record the actual transport, the available context, the target of the effect, and any special runtime requirements. If a route depends on a console, debug mode, clipboard access, runtime hooks, or another unusual mechanism, document that dependency and how it affects a possible public release. An experimental mechanism is not automatically a release architecture.

## Acceptance criteria

The milestone passes when a reproducible demonstration establishes all of the following:

- A player action inside CK3 begins the interaction before combat, with the game paused as intended.
- The external process receives enough real context to identify the request and the chosen participants.
- A controlled external result reaches the same running game session without restarting CK3 or manually editing files during play.
- The intended target receives the documented effect, and an unrelated target does not.
- The result and effect are visible without the player switching applications.
- A failed or cancelled exchange leaves gameplay unchanged. A duplicate result does not apply the effect twice.
- After the interaction completes, saving and reloading preserves the expected effect state without reapplying the result.

If only part of this path works, record the demonstrated portion and the remaining blocker. A transport demonstration alone does not establish correct effect scope or a usable player interaction.

## Required evidence

For each attempted approach, record:

- The CK3 version, enabled DLC and mods, operating system, and runtime configuration used for the test.
- The implementation revision and exact reproduction steps.
- The context exchanged and how requests and results are associated with their targets.
- The expected and observed effects, including the failure, duplicate, and save/reload checks.
- Supporting output, screenshots, or recordings that make the result reviewable.
- Known limitations and whether they prevent the intended public release experience.

Keep credentials and personal data out of published evidence. Setup and verification commands belong here once they have been exercised successfully. Until then, there is no executable verification procedure for this milestone.

## Outcome

A successful experiment should lead to an architecture decision explaining the chosen communication and UI approach, the alternatives examined, and their tradeoffs. It should also provide the list of accessible context and supported effects needed to begin evaluation design.

If a reliable round trip cannot be demonstrated, document the specific limitation and reconsider the interaction or integration method. There is no settled prohibition on particular integration techniques, and there is no commitment to adopt a technique merely because it can be made to work.

## Reference project

[Voices of the Court](https://github.com/Voices-of-the-Court/VOTC) is a relevant implementation to investigate. Its [installation documentation](https://docs.voicesofthecourt.app/installation/) describes a CK3 mod used with a separate desktop application. Its [window implementation](https://github.com/Voices-of-the-Court/VOTC/blob/main/src/main/main.ts) provides an example of an external overlay.

These references establish a candidate approach to study. They do not demonstrate Rally the Realm's required context, effect scope, or interaction. Record the exact upstream revision when using its implementation as evidence for a technical choice, and review the applicable license before reusing code.
