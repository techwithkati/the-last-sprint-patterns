# CLAUDE.md Template — React + TypeScript Side Project

# Version: 1.0

# Status: testing

# Last updated: 2026-05-19

# Source: derived from tls-react-lab/CLAUDE.md

# Lab repo: https://github.com/techwithkati/tls-react-lab

This is a reusable CLAUDE.md template for React + TypeScript side projects.

It is derived from the CLAUDE.md used in `tls-react-lab`, a public-safe lab repo for testing CLAUDE.md patterns, Claude Skills, and AI code review workflows.

This file is not universal. Adapt it to your own project. Delete sections that do not apply. Add constraints that matter in your codebase.

---

## 1. Project Context

<!--
Why this section exists:
Claude needs to know what this project is before it edits files.
Without project context, it defaults to generic React patterns that may not match your codebase.
-->

[PROJECT_NAME] is a [short description of the project].

It is built with:

- React
- TypeScript
- Vite
- [CSS approach: Tailwind / CSS modules / styled-components / other]
- [Routing: React Router / TanStack Router / none]
- [Testing: Vitest + Testing Library / Jest / other]
- [Persistence: LocalStorage / Supabase / API / other]

This is a [side project / client project / internal tool / learning project].

The goal of this codebase is:

- [Goal 1]
- [Goal 2]
- [Goal 3]

Do not expand the project scope unless explicitly asked.

---

## 2. Stack Constraints

<!--
Why this section exists:
Claude has defaults from training. This section overrides those defaults with the decisions already made in this project.
-->

Follow these stack rules:

- TypeScript strict mode is expected.
- Do not use `any` unless there is no better option.
- If `any` is used, add a short comment explaining why.
- Prefer explicit types for shared data models.
- Keep components small and readable.
- Do not introduce a new state management library unless asked.
- Do not introduce a new UI library unless asked.
- Do not change routing structure unless the task is specifically about routing.
- Do not change build tooling unless the task is specifically about tooling.

Current conventions:

- Components live in `[path/to/components]`.
- Feature-specific code lives in `[path/to/features]`.
- Shared types live in `[path/to/types]`.
- Shared utilities live in `[path/to/lib-or-utils]`.
- Tests live `[next to the file / in __tests__ / in test folders]`.
- Styling uses `[Tailwind / CSS modules / other]`.

When unsure, follow the existing pattern in the nearby files.

---

## 3. Do-Not-Touch Zones

<!--
Why this section exists:
Some files are load-bearing. AI should not casually regenerate them.
This section names the files and folders Claude must not edit without asking first.
-->

Do not modify these files or folders without explicit confirmation:

- `[path/to/storage.ts]` — persistence boundary. Changes can affect saved data.
- `[path/to/types.ts]` — shared types. Changes ripple through the app.
- `[path/to/api-or-repo-layer]` — data access boundary. Keep function signatures stable.
- `vite.config.ts` — build configuration.
- `vitest.config.ts` — test configuration.
- `tsconfig.json` and related TypeScript config files — strict settings are intentional.
- `.env*` files — never create, edit, or commit secrets.

If a requested change requires touching a do-not-touch zone, stop and say:

**STOP, escape hatch triggered.**

Then explain:

1. Which file or folder needs to change.
2. Why the change is necessary.
3. What could break.
4. What you recommend doing next.

Do not proceed until the developer confirms.

---

## 4. Escape Hatch Phrase

<!--
Why this section exists:
Without an explicit stop phrase, Claude may guess when it is unsure.
This rule tells Claude exactly when to pause and surface the decision.
-->

Use this phrase when you hit uncertainty or risk:

**STOP, escape hatch triggered.**

Trigger the escape hatch when:

- A task requires editing a do-not-touch zone.
- A task requires changing project architecture.
- A task requires adding a new dependency.
- A task requires deleting or weakening tests.
- A task requires changing shared types.
- A task requires changing persistence or data shape.
- A task is ambiguous and multiple reasonable approaches exist.
- A task would expand the project scope beyond the request.

After the phrase, explain the decision clearly and wait for direction.

Do not guess.
Do not silently proceed.
Do not make destructive changes without confirmation.

---

## 5. Code Change Rules

<!--
Why this section exists:
AI-generated code often works in the demo but becomes hard to review later.
These rules make changes smaller, clearer, and easier to inspect.
-->

When changing code:

- Make the smallest change that solves the problem.
- Prefer boring, readable code over clever code.
- Keep existing behavior unless the task explicitly changes it.
- Do not rewrite a file just to improve style.
- Do not rename variables, files, or functions unless needed for the task.
- Do not mix refactoring with feature work unless asked.
- Preserve existing public function signatures unless the change is approved.
- If a change touches more than 3 files, explain the plan before editing.
- If a change creates a new pattern, document the pattern briefly.

Before editing, identify:

1. Files expected to change.
2. Files that should not change.
3. Tests that should be added or updated.
4. Risk level: low, medium, or high.

---

## 6. Testing Rules

<!--
Why this section exists:
AI-generated code often treats tests as optional or weakens assertions to make tests pass.
This section defines what “done” means.
-->

Testing expectations:

- New behavior should include tests.
- Bug fixes should include a regression test when practical.
- Do not delete tests to make a change pass.
- Do not weaken assertions unless the test was wrong.
- Prefer user-facing tests with Testing Library.
- Use role and label queries when possible.
- Avoid testing implementation details.
- Avoid test IDs unless there is no accessible alternative.
- Run the relevant tests before calling the task complete.

For React components:

- Test the behavior the user sees.
- Test important empty states.
- Test important error states.
- Test important disabled/loading states when relevant.

For utilities and data functions:

- Test normal cases.
- Test edge cases.
- Test invalid or empty input when relevant.

If tests fail:

1. Explain the failing test.
2. Explain whether the code or test is wrong.
3. Fix the code first.
4. Only update the test if the expected behavior changed intentionally.

---

## 7. Dependency Rules

<!--
Why this section exists:
Claude may add dependencies when a small local solution would be better.
Dependencies increase project surface area.
-->

Do not add a new dependency without explaining:

1. What problem it solves.
2. Why existing code cannot solve it.
3. The maintenance cost.
4. The smaller alternative.

Prefer:

- Existing project dependencies.
- Small local utilities.
- Platform APIs.
- Simple React patterns.

Avoid adding dependencies for:

- Formatting dates unless the app already uses a date library.
- Small utility helpers.
- Simple state management.
- One-off UI behavior.

---

## 8. Commit Rules

<!--
Why this section exists:
AI-generated commits can become vague and hard to review.
This keeps commit history readable.
-->

Use clear, small commits.

Preferred format:

- `feat: add [thing]`
- `fix: correct [thing]`
- `refactor: simplify [thing]`
- `test: add coverage for [thing]`
- `docs: update [thing]`
- `chore: update tooling`

Rules:

- One logical change per commit.
- Commit subject should be under 70 characters.
- Avoid vague commits like `update files`, `fix stuff`, or `changes`.
- Mention tests when relevant.
- Do not commit generated files unless they belong in the repo.

---

## 9. PR Description Rules

<!--
Why this section exists:
A good PR description makes AI-assisted code easier to review.
This format forces Claude to name risk and verification steps.
-->

When asked to write a PR description, use this format:

```md
## Summary

- [What changed]
- [Why it changed]

## Files changed

- `[file]` — [reason]
- `[file]` — [reason]

## Risk level

Low / Medium / High

Reason:
[Explain the risk.]

## Test plan

- [ ] [Test or command run]
- [ ] [Manual check]

## Manual review checklist

- [ ] Types are safe.
- [ ] Tests cover the changed behavior.
- [ ] No do-not-touch zones were modified without approval.
- [ ] No unrelated files were changed.
- [ ] No scope creep was introduced.

## AI-assisted note

This change was AI-assisted and manually reviewed.
```
