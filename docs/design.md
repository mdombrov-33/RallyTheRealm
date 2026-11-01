# Design

Rally the Realm lets players influence a battle by addressing their troops. The words are evaluated in the context of the speaker, the army, and the war. The design aims to make a speech worth attempting, with consequences that players can understand and that remain part of CK3's military game.

This document describes intended behavior. The [feasibility milestone](feasibility.md) tracks what must be demonstrated before implementation choices can support it.

## Scope

The first release is intended for single-player campaigns using the CK3 base game. A specific game version and supported operating systems will be established through implementation and testing. DLC compatibility, multiplayer, and compatibility with other mods require separate investigation.

Both rulers and commanders can be speakers. Each speech has an identified character speaking to an identified army. Which interactions make a character eligible, and how the player selects them, remain open.

The mod should support serious roleplay and the occasional spectacular failure. Humor should come from the player's words and the situation. The evaluator should not pursue a joke at the expense of a coherent response from the troops.

## Speech interaction

The player deliberately starts an optional interaction before combat. The intended experience pauses the game while the player prepares and delivers the speech. The entry point, timing, and ability to keep the game paused must be verified.

The player can record a speech or enter text. Both use the same evaluation criteria. Recording provides a transcript that the player can review and correct before submission; it does not provide a scoring bonus. Vocal performance is outside the initial evaluation design.

Submission commits the speech for that opportunity. A poor result does not offer another attempt. A technical retry preserves the submitted speech. What constitutes a new opportunity, and what limits prevent repeated use, still need to be designed.

The player then sees the assessment, the calculation of its consequences, and the resulting gameplay effects. The full interaction should work without switching applications. A background process may support it, but the choice between native menus, an overlay, or another approach depends on feasibility research. See [ADR 0002](decisions/0002-keep-the-speech-interaction-in-game.md).

## Evaluation

The meaning of the words and their relationship to the situation drive the assessment. Relevant circumstances include the speaker and the opposing sides of the war, using information the integration can reliably provide. Emotional meaning expressed through the words may also matter.

Character traits inform interpretation without dictating what the player must say. A speech that contradicts the speaker's usual personality can still succeed. An army's reaction and any consequences for its speaker can differ.

The evaluation rubric is unresolved. No dimensions, scoring scale, weights, or thresholds have been selected. Personality, stress, and speech quality are candidate factors for the visible calculation, not an established formula. Available game context must be investigated before the rubric depends on particular fields.

The model assesses the speech. Validated output passes through project-owned rules that determine the permitted effects and their magnitude. The separation and its tradeoffs are recorded in [ADR 0001](decisions/0001-separate-assessment-from-gameplay-effects.md).

## Gameplay consequences

A good speech can help an army, and a bad one can harm it enough to change a close battle. Military conditions should still determine most of the outcome. A speech changes combat conditions rather than directly declaring victory or defeat.

Effects must be bounded and apply to the intended target. The actual modifiers, their duration, and the definition of the intended engagement require research and balancing. This design does not assume CK3 exposes a particular army or battle modifier.

Failures to record, transcribe, evaluate, or validate a speech are technical failures. They should allow recovery or cancellation without a gameplay penalty. An evaluated speech that fails to inspire the army is a gameplay outcome and can carry a penalty.

## Showing the result

The calculation is part of the experience. A visual sequence should show the relevant inputs, each contribution to the result, and the resulting effects. Players can skip the animation and inspect the completed breakdown.

The interface must distinguish a model judgment from an exact calculation. It can show an assessment and the reasons returned for it, then display precisely how the rules turn that assessment and other inputs into effects. These reasons are an explanation of the assessment, not a claim to expose the model's internal reasoning.

Every displayed numerical contribution must correspond to the calculation actually used. The final view should make clear what changes in the game, which character or army is affected, and how long the effect lasts. Numerical presentation and visual styling will be designed alongside the effect system.

## API use

Players supply and pay for any API services they use. Providers, configuration, and the role of local models remain undecided. A hosted service operated by the project is not part of the current plan.

## Open design questions

These questions remain open without blocking the first integration experiment:

- How does the player choose an eligible speaker and army, and when is the interaction available?
- Which facts about the speaker, troops, and war are both useful and accessible?
- What rubric produces understandable assessments across different speeches and situations?
- How should evaluation handle invented claims, uncertain context, and attempts to manipulate the evaluator?
- Which effects and limits make speeches consequential without rewarding repetitive use?
- Which languages should the first release support, and how will transcription quality be evaluated?
- What latency is acceptable, and how should cancellation and interrupted sessions behave?
- How should recordings, transcripts, game context, and API credentials be handled and retained?
- Which distribution channels and project license should be used?

The rubric needs its own design and evaluation work after the integration experiment establishes the available context and practical effect boundaries.
