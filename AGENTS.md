# Working in Rally the Realm

Rally the Realm is a Crusader Kings III mod in design and feasibility work. The repository currently has no selected implementation stack or development commands. Keep product intent, technical evidence, and implementation decisions distinct.

## Read the document that owns the work

- For player behavior and scope, read [product design](docs/design.md).
- For current status and the next work item, read the [roadmap](docs/roadmap.md).
- Before investigating CK3 behavior or planning runtime tests, read [technical validation](docs/technical-validation.md) and [feasibility](docs/feasibility.md).
- Before changing an architectural boundary, read the [decision index](docs/decisions/README.md) and relevant records.

Update the document that owns a fact and point other documents to it. Keep the roadmap as the single source for project status and next steps.

## Project constraints

- Do not describe intended behavior as a demonstrated CK3 capability.
- Verify script hooks, accessible context, effect scope, and external communication on a documented game version before relying on them.
- Keep speech evaluation behind validation and project-owned rules. The rubric and score-to-effect values remain unfinished until explicitly calibrated.
- Preserve the requirement that players can complete a speech without switching applications. A background helper is an acceptable fallback if feasibility work requires one.
- Keep the ignored `ck3-reference/` game files out of commits, examples, and distributable packages.

## Documentation and evidence

Use direct, natural language for readers without conversation history. Explain behavior, reasons, limitations, and evidence; omit session transcripts and personal setup details. Record consequential architecture choices with alternatives and consequences. When a choice changes, supersede the old decision instead of silently rewriting its history.

For documentation changes, check relative links and consistency with design and accepted decisions. For CK3 experiments, record the tested game version, checksum, setup, and observed result. Treat a package build as packaging evidence only; CK3 behavior requires an in-game test.
