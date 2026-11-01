# Rally the Realm

Rally the Realm is a planned Crusader Kings III mod that lets players address their troops before battle. Speak as a ruler or commander, or type a speech, and have those words evaluated against the circumstances of the war. The resulting reaction can help or hurt the army in the coming fight.

The project is in design and feasibility research. There is no playable release yet. The first milestone is to demonstrate a reliable interaction between CK3 and an external process, with a visible gameplay effect and no need for the player to switch applications.

## Intended experience

A speech should matter because of what it means to the people hearing it. The speaker, the opposing sides, and the situation should shape the response. A disastrous speech can turn a close fight against the player. Funny outcomes can emerge naturally from a world that takes the speech seriously.

Players should be able to follow the result as it is calculated. The interface will distinguish the model's assessment from the rules that apply gameplay effects, show each actual contribution, and leave the completed breakdown available to inspect.

The initial scope is single-player CK3 using the base game. Compatibility with DLC, other mods, and additional modes has not been established. A background application is an option under investigation; the player experience should remain within the game throughout a speech. Players will supply and pay for any API services they use.

## Project documentation

- [Design](docs/design.md) describes the intended behavior, scope, and unresolved design questions.
- [Feasibility milestone](docs/feasibility.md) defines the first experiment and the evidence required to proceed.
- [Architecture decisions](docs/decisions/README.md) records decisions, their reasons, and their consequences.

There are no installation, build, or test commands yet. They will be documented when the corresponding implementation can be run and verified.
