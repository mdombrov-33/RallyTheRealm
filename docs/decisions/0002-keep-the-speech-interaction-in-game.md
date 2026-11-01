# ADR 0002 Keep the speech interaction in game

**Status:** Accepted  
**Date:** 2026-11-01

## Context

A speech occurs during a campaign, before combat. Requiring the player to switch to another application to record, submit, or inspect it would interrupt that interaction. CK3's ability to support recording, external evaluation, and the intended interface has not been established for this project.

## Decision

Players must be able to initiate a speech, provide and review its text, submit it, and inspect the result without switching applications during play.

A background application is acceptable if the implementation needs one. Native game menus, an overlay, and other integration approaches remain candidates. This decision specifies the player experience without selecting where recording or evaluation runs.

The requirement covers the speech interaction. Installation, API configuration, and application startup will need their own usability design.

## Alternatives

A separate foreground application would simplify some interface work, but requiring routine window switching during speeches does not meet the intended experience.

Requiring every component to run natively inside CK3 would constrain implementation before the necessary capabilities have been demonstrated. That restriction is not adopted.

## Consequences

The integration experiment must exercise the visible interaction as well as the exchange of data. A functioning external process is insufficient evidence if the player must leave the game to use it.

If a helper or overlay is selected, its interaction with game focus, input, window modes, and supported platforms will need testing. The communication method, UI technology, startup process, and operating system support remain undecided.
