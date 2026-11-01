# Working in Rally the Realm

Rally the Realm is a CK3 mod project in design and feasibility research. The repository currently contains documentation; no runtime, integration method, or build tooling has been selected.

## Read for the task

- Before changing gameplay or player interactions, read [the design](docs/design.md). It owns the product baseline and unresolved design questions.
- Before researching or implementing CK3 integration, read [the feasibility milestone](docs/feasibility.md). It owns the current milestone, acceptance criteria, and evidence requirements.
- Before choosing or changing an architectural boundary, read [the decision index](docs/decisions/README.md) and the relevant records.

## Project constraints

Keep intended behavior distinct from demonstrated CK3 capabilities. Verify script hooks, accessible context, effect scope, and external communication against a documented game version before relying on them.

Treat the speech evaluation rubric as unresolved. Example inputs, scores, and modifiers are proposals until the design explicitly adopts them.

Keep model output behind validation and project-owned gameplay rules. Preserve the requirement that players can complete a speech without switching applications.

## Documentation and verification

Write public documentation for players and contributors who have no conversation history. Explain behavior, reasons, limitations, and evidence in plain language. Keep personal environment details and session transcripts out of project documentation.

Update the document that owns a fact and link to it elsewhere. Record architectural decisions with their alternatives and consequences; mark a changed decision as superseded rather than silently rewriting its history.

For documentation changes, check relative links and consistency with the design and accepted decisions. There are currently no executable checks. Add setup and verification commands only after running them successfully, and keep milestone status tied to the evidence in the feasibility document.
