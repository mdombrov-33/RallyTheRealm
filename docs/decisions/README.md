# Architecture decisions

These records explain choices that constrain the implementation. An accepted decision records project intent; it does not mean that its implementation exists or has been verified.

| Record | Status | Decision |
| --- | --- | --- |
| [0001](0001-separate-assessment-from-gameplay-effects.md) | Accepted | Validate model assessments and let project rules determine effects |
| [0002](0002-keep-the-speech-interaction-in-game.md) | Accepted | Keep the complete speech interaction in the game experience |

The technology stack, communication method, and calibrated evaluation rubric remain open. The [roadmap](../roadmap.md) and [feasibility work](../feasibility.md) record what must be demonstrated before choosing an integration.

## Adding a decision

Use a numbered Markdown file with a descriptive title. Record its status, the problem and constraints, the decision, alternatives considered, and the consequences. Link to evidence where the choice depends on a technical finding. A proposal should remain marked as proposed until it is adopted.

Keep product behavior in the [design](../design.md), test procedures and evidence in the [technical validation plan](../technical-validation.md), and the decision gate in [feasibility](../feasibility.md). An ADR should explain a consequential choice rather than repeat those documents.

When a decision changes, add a new record and mark the old one as superseded with a link to its replacement. Preserve the original reasoning so readers can understand why the earlier choice was made.
