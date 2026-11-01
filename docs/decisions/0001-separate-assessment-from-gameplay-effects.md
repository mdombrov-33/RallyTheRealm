# ADR 0001 Separate assessment from gameplay effects

**Status:** Accepted  
**Date:** 2026-11-01

## Context

Speech evaluation involves judgments about meaning and circumstances. Gameplay effects need explicit limits and must be explainable to the player. Letting the same model freely choose effects and their magnitude would make those limits harder to enforce and the resulting calculation harder to inspect.

## Decision

The model produces an assessment of the speech and reasons for that assessment. Its output is validated before project-owned rules map it, together with relevant game inputs, to permitted gameplay effects.

The rules own effect selection, magnitude, duration, and applicable limits. Model output cannot directly execute game commands. For the same accepted assessment and game inputs, the rules produce the same effects. This does not promise that repeated model evaluations will return identical assessments.

The result interface distinguishes the model's judgment from the subsequent calculation and shows the actual contributions used by the rules.

## Alternatives

Allowing the model to choose arbitrary modifiers or generate executable game commands would make balancing and explanation depend on unconstrained output. That approach is rejected.

A wholly rule-based speech evaluator remains a possible subject for experiments, but it is not the selected direction for interpreting free-form speech in context.

## Consequences

The implementation needs a defined assessment format, output validation, and a separately testable mapping to effects. Invalid or unavailable assessments must follow technical failure handling rather than become poor speech ratings.

The rubric, output schema, and effect mapping still require design. This decision establishes their boundary without choosing scores, providers, libraries, or balancing values.
