# Rally the Realm

Rally the Realm is an in-development Crusader Kings III mod about addressing your troops before battle. Your words are judged in the context of the speaker, the audience, and the war. A successful speech can help your realm's armies; a truly poor one can make the coming battle harder.

The intended scene opens automatically before a qualifying battle, pauses the game, and lets the player speak or type. A clear score breakdown explains how the speech was assessed and what effect follows. Typed and spoken input, multiple hosted AI providers and models, and a polished in-game experience are part of the first-release target.

## Project status

The project is in design and feasibility work. There is no playable speech mod or companion application yet. The [roadmap](docs/roadmap.md) is the source for the current state and next work item; [feasibility](docs/feasibility.md) records what has been observed and what must be proved.

## Project guide

- [Product design](docs/design.md) describes the intended player experience, scope, and open design work.
- [Roadmap](docs/roadmap.md) shows what is demonstrated and what comes next.
- [Technical validation plan](docs/technical-validation.md) records CK3 source findings and the runtime tests needed before choosing a stack.
- [Feasibility](docs/feasibility.md) explains the evidence required before an implementation plan can be chosen.
- [Architecture decisions](docs/decisions/README.md) records accepted boundaries and alternatives.

## Target scope

The first release is planned for single-player CK3 using the base game, on Windows first, in English. It will include typed and microphone input, with speech recognition running locally. Players will configure and pay for their own AI provider. The project plans to publish source on GitHub and distribute the mod through a workshop.

These are targets, not existing features. No supported CK3 version, integration method, programming language, or release build has been established. See [what remains open](docs/design.md#still-open) and the current status in the [roadmap](docs/roadmap.md).
