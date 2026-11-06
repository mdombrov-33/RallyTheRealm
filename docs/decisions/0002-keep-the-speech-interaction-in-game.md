# ADR 0002 Keep the speech interaction in the game experience

**Status:** Accepted  
**Date:** 2026-11-06

## Context

A speech occurs during a campaign, before combat. The intended scene opens automatically according to the player's battle settings, pauses the game, and stays available through recording or typing, transcript review, submission, and result inspection. Requiring the player to switch to another application during that flow would interrupt the interaction. CK3's ability to support automatic pre-battle timing, recording, external evaluation, and the intended interface has not been established for this project.

## Decision

The complete speech interaction must remain accessible without switching applications during play. The player chooses whether and how often the scene opens in CK3 settings; the speech itself is presented automatically before qualifying battles rather than started from a button press.

A pure mod is preferred, but a quiet background application is acceptable if feasibility work requires one. Native CK3 UI is the desired presentation when it can support the experience; an overlay remains a candidate if it can stay over the game and avoid a visible application switch. This decision specifies the player experience without selecting the technical architecture.

The requirement covers the speech interaction. Installation, API configuration, and application startup will need their own usability design.

## Alternatives

A separate foreground application would simplify some interface work, but requiring routine window switching during speeches does not meet the intended experience.

Requiring every component to run natively inside CK3 would constrain implementation before the necessary capabilities have been demonstrated. That restriction is not adopted.

## Consequences

The [technical validation plan](../technical-validation.md) must test battle timing, the visible interaction, and the exchange of data. A functioning external process is insufficient evidence if the player must leave the game to use it.

If a helper or overlay is selected, its interaction with game focus, input, window modes, and supported platforms will need testing. The communication method, UI technology, startup process, and operating system support remain undecided.
