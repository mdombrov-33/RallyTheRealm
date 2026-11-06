# Feasibility

This page explains when the project has enough evidence to choose an implementation. The [technical validation plan](technical-validation.md) is the working record for source findings, test procedures, results, and pass conditions. The [roadmap](roadmap.md) owns the current project state and next work item.

## Current evidence

One screenshot from an in-game run showed a custom window opening an event and applying a temporary +1 Advantage character modifier to the player ruler. Its CK3 version and checksum were not recorded. This confirms only that path in that run; it does not establish battle timing, army scope, combat impact, microphone capture, or communication with a helper.

The local CK3 source snapshot has unknown version provenance. It shows event text entry and UI-to-script examples. It also shows that `on_combat_start` fires after the starting armies join combat sides, but does not say whether the first combat phase advances before a blocking event can pause the game. The source scan found no documented microphone API or ordinary-play helper bridge. These findings guide the tests; they do not prove those features impossible.

## Gate for an implementation plan

Before selecting languages or application frameworks, the technical validation plan must establish:

- Whether an in-game scene can pause a qualifying battle before it advances, including from `on_combat_start`.
- Which battle, speaker, army, and war facts are available at that moment.
- Whether a bounded effect can reach the player's participating armies for the intended battle only.
- Whether a normal-play path can carry an in-game request to a hidden helper and return a result to the same game session.
- Whether the in-game screen can control background microphone capture and show a transcript for review.
- Whether failure, cancellation, duplicate responses, and save/reload leave the campaign in a predictable state.

Record the chosen architecture and alternatives in a decision record after these tests. If a test fails, update the design or the technical approach before building provider integrations and release tooling. Do not treat a debug-only route or a button-to-character-modifier demonstration as proof that the speech experience works.
