# Product design

Rally the Realm is a single-player Crusader Kings III mod about addressing troops before battle. The player gives a speech in their own words. Its meaning, the speaker, and the circumstances of the war shape how the troops respond. A strong speech can help the player's forces; a truly poor one can make the fight harder. Humor should come from what the player says and what happens in the campaign, not from the mod treating every scene as a joke.

This is the agreed product direction. It describes intended behavior, not verified CK3 capabilities. The [roadmap](roadmap.md) tracks the work needed to demonstrate it.

## First release

The first release targets single-player campaigns using the CK3 base game, on Windows first. English is the initial supported speech language. Both typed and spoken input are part of the release. The first release focuses on battles; other speech situations may be explored later. Compatibility with DLC and other mods will be investigated separately.

Players will choose and pay for any hosted AI service they use. Initial provider options are OpenAI, Anthropic, and Google Gemini, with multiple supported models per provider. The local speech-recognition component turns microphone input into editable text. Audio is not sent to an AI provider.

The project will publish its source and documentation on GitHub and distribute the mod through a workshop. The project license and final technology stack are still open.

## When the scene opens

The scene opens automatically when a qualifying battle is about to progress and the player's realm has an army in it. The game may already have created the combat and joined the armies; the scene must pause before the battle advances. The player configures the trigger in CK3's mod settings:

- Every battle involving the player's realm armies.
- Only battles in which the ruler or a chosen commander is leading an army.
- Off.

Participation counts even when the player is not the war leader, such as when the player's realm joins an ally's war. The scene pauses the game and waits for the player to submit a speech or skip it. After showing the result, the interface waits for the player to continue before the battle proceeds.

## Speaker and audience

The player chooses a speaker mode in the mod settings: the ruler, a field commander, or a choice at each battle. In field commander mode, the player chooses among commanders of their participating armies. A ruler can speak even when not commanding an army. A setting decides whether an absent ruler's address is delivered by a representative or whether the ruler can speak only when present.

The speech addresses the player's realm troops in the battle. It affects all of the player's participating realm armies together, not allied armies. The chosen speaker can address the troops without commanding one of their armies. The player may speak naturally; they are not required to imitate the character or speak in first person. The selected character informs the credibility assessment.

## Briefing and appeal

Before choosing an appeal, the player sees a briefing with the facts the mod can verify, including the battle's location, sides, commanders, and the war's purpose and stakes when available. The evaluator must not ask the player to supply missing game facts or invent facts the mod cannot verify.

The player then chooses one main appeal for the speech. The initial set is a working list: defend home, faith, revenge, loyalty, honor, and reward. Every appeal remains selectable in every situation. The choice sets an expectation for the speech; it is not a flat score multiplier. A speech that makes a convincing case for its chosen appeal can benefit, while one that ignores or contradicts it can lose credit. Other themes may appear in the speech.

## Speech input

Players can type or record a speech. There is no speech-time limit. Typed and transcribed text share a protective character limit, to be set during implementation, with a visible counter. The microphone activates only after the player chooses Speak; the screen shows when it is recording, and the player can stop or cancel. Recording stops before submission. A transcript appears for review and correction, and nothing is evaluated until the player submits it.

Speech suggestions are outside the first release: the player supplies the words. Speech length and vocal performance do not earn points by themselves. Both input methods use the same evaluation criteria.

## Assessment and gameplay effect

The AI assesses the speech against a project-owned rubric and returns a structured result. It does not choose or execute a gameplay effect. The project validates that result, then its own rules calculate the score and effect. The selected provider and model are shown; different models may assess the same speech differently, but they use the same project-owned gameplay rules. A retry of one submitted speech reuses the same accepted assessment rather than rerolling its outcome.

The initial rubric dimensions are:

1. Does the speech address this battle and its stakes?
2. Does it make a convincing case for the chosen appeal?
3. Would the intended audience believe this speaker?
4. Is it coherent and emotionally effective?

Only game facts the mod can verify may be used as evidence. An unsupported claim receives no bonus; a claim contradicted by verified facts may count against the speech. Character traits can inform credibility, but they do not dictate what the player may say. Stress has no automatic penalty; it matters only when the speech or situation gives a clear reason. A character can speak against their usual personality and still succeed.

The interface shows a 0–100 headline score, a plain-language label, and short explanations for each factor, tied to the speech or verified facts. The exact rubric, weights, thresholds, repeat-use rules, and balancing values remain open for dedicated design and evaluation. Weak or bland speeches can earn no benefit; genuinely insulting, incoherent, or contradictory speeches can cause a penalty. Repeating a speech can weaken its effect only when the game can verify that it was heard recently, and the breakdown must explain that contribution.

For the first release, the score controls a temporary Advantage effect for the player's participating realm armies in that battle. The precise implementation, duration, score-to-effect curve, and battle-specific scope must be demonstrated in CK3 before they are described as working behavior. A speech can change the conditions of a close fight; it does not declare victory or defeat.

The result screen explains what affected the score, how project rules turned it into an effect, which armies receive the effect, and how long it lasts. It distinguishes the AI's assessment from exact rule calculations. Players can read the completed breakdown before choosing Continue.

## Privacy and failure behavior

Microphone audio stays on the player's device. The player reviews the transcript before submission. Only the submitted text and relevant verified game facts go to the selected provider. The player supplies and pays for the provider account; the provider's own data handling applies to what it receives. Audio is discarded after transcription and review; the transcript is discarded after the result or cancellation. The campaign keeps the score, factor breakdown, effect, and battle outcome. An optional speech history can be considered later.

The companion application, if needed, owns provider, model, API-key, microphone, and transcription settings. In-game settings own battle triggers and speaker mode. The companion must work in the background so that the player never has to switch applications during a speech. A pure mod is preferred; a quiet background helper is an acceptable fallback if feasibility work shows it is needed.

Missing configuration, microphone or transcription errors, provider failures, invalid responses, and canceled requests are technical failures, not bad speeches. The player can retry or continue the battle without a speech effect. Canceling evaluation proceeds without an effect. No gameplay change is applied unless a valid assessment succeeds.

## Still open

- The speech-evaluation rubric's detailed definitions, examples, weights, and thresholds.
- The exact trigger mechanism, available battle context, and effect scope CK3 permits.
- Whether a no-helper integration can support the full flow; the helper and UI architecture remain undecided.
- Programming languages, libraries, package formats, and secure credential storage.
- Exact character limit, transcription model, and compatibility targets beyond Windows and the base game.
- Project licensing and contribution terms.

The two accepted architecture boundaries are recorded in [the decision index](decisions/README.md): project rules own gameplay effects, and the complete speech interaction stays in the game experience.
