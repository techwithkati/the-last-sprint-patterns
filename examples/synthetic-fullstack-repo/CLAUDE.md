# CLAUDE.md for Taskboard

> Filled example for a fictional app. Copy this into your repo and replace every
> detail with the truth about your project. Keep it short: a working agreement,
> not a config file.

## Project context

Taskboard is a small team task tracker: boards, columns, and cards. It is built
with React + TypeScript + Vite on the frontend, a Node + Express REST API, and
Postgres reached through a thin repository layer.

Do not expand the scope of a task beyond what was asked. If a change seems to
need more, say so and stop.

## Stack constraints

- TypeScript strict mode is on. Do not use `any` without a one-line reason.
- Frontend code lives in `client/src`; API code in `server/src`.
- Shared UI in `client/src/components`, feature code in `client/src/features`,
  shared models in `client/src/types`.
- Database access goes through `server/src/repo`. Routes do not talk to the
  database directly.
- Do not add a state-management library, a UI kit, or an ORM unless asked.
- When unsure, follow the pattern in the nearest existing file.

## Do-not-touch zones

Do not modify these without explicit confirmation:

- `server/src/repo/**`: the persistence boundary. Changes can affect saved data.
- `server/src/db/migrations/**`: applied migrations are history; never edit in place.
- `client/src/types/**`: shared models ripple across the app.
- `*.config.ts`, `tsconfig*.json`: build and strictness settings are intentional.
- `.env*`: never create, edit, or commit secrets.

If a task needs one of these, stop and trigger the escape hatch.

## Escape hatch

When you hit risk or uncertainty, stop and say:

**STOP, escape hatch triggered.**

Trigger it when a task would: touch a do-not-touch zone, change architecture,
add a dependency, delete or weaken tests, change shared types or data shape, or
is ambiguous with more than one reasonable approach.

Then explain what needs to change, why, what could break, and what you
recommend. Do not guess. Do not proceed until I confirm.

## Code change rules

Before editing, name:

1. The files you expect to change.
2. The files that should not change.
3. The tests to add or update.
4. The risk level: low, medium, or high.

Then:

- Make the smallest change that solves the problem.
- Keep existing behavior unless the task changes it.
- Do not rewrite a file to improve style, and do not rename symbols unless the
  task needs it.
- Do not mix refactoring with feature work.
- If a change touches more than 3 files, explain the plan before editing.

## Testing rules

- New behavior gets a test. Bug fixes get a regression test when practical.
- Do not delete tests or weaken assertions to make a change pass.
- Test what the user sees: prefer role and label queries over test IDs.
- Run the relevant tests before calling a task done.
- If a test fails, fix the code first. Only change the test if the expected
  behavior changed on purpose.

## Dependencies

Do not add a dependency without naming the problem it solves, why existing code
cannot, the maintenance cost, and the smaller alternative.

## Commits

One logical change per commit. Use `feat:` / `fix:` / `refactor:` / `test:` /
`docs:` / `chore:` prefixes. Subject under 70 characters. No vague messages like
"update files."

---

For the long-form annotated version of these rules, see
[`../../claude-md/react-ts.md`](../../claude-md/react-ts.md).
