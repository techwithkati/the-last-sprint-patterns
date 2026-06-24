# Skills

This folder will hold Claude Skills: small, reusable procedures that package a workflow so Claude runs it the same way every time.

Nothing ships here yet, and that is deliberate. A skill earns its place only after the workflow behind it has been tested enough times to be worth automating. A skill written before then just encodes a guess.

## Planned

- `safe-claude-code-change`: the plan-then-edit loop. Name the files that will change, the files that must not, the tests to add, and the risk level, before touching code.
- `ai-assisted-pr-review`: walk a generated diff against a manual review checklist instead of trusting a green test run.

These move out of "planned" once they have been used on real projects and I would point at the result. Until then this file is the honest placeholder.

See [`../patterns/react-ts-claude-md.md`](../patterns/react-ts-claude-md.md) for the change and review rules these skills will build on.
