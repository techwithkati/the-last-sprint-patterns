# AGENTS.md — Taskboard

> Filled example for a fictional app. `AGENTS.md` is the tool-agnostic companion
> to `CLAUDE.md`: the commands and conventions any coding agent (Claude Code,
> Codex, or another) needs to work in this repo. Keep the deep rules in
> `CLAUDE.md`; keep this file practical and short.

## Setup

```bash
# Frontend
cd client && npm install

# API
cd server && npm install
```

Copy `.env.example` to `.env` and fill it in. Never commit `.env`.

## Commands

| Task | Command |
| --- | --- |
| Run frontend | `cd client && npm run dev` |
| Run API | `cd server && npm run dev` |
| Frontend tests | `cd client && npm test` |
| API tests | `cd server && npm test` |
| Type check | `npm run typecheck` (in each package) |
| Lint | `npm run lint` (in each package) |

Run the relevant tests and the type check before calling a task done.

## Where things live

- Frontend: `client/src` — `components/` (shared UI), `features/` (board,
  column, card), `lib/` (utilities), `types/` (shared models).
- API: `server/src` — `routes/` (Express handlers), `repo/` (database access),
  `db/` (connection and migrations).
- Routes call into `repo/`; they do not query the database directly.

## Boundaries

Do not change these without asking first:

- `server/src/repo/**` and `server/src/db/migrations/**` — persistence boundary.
- `client/src/types/**` — shared models.
- Build and TypeScript config files; `.env*`.

When a task would cross a boundary, change architecture, add a dependency, or
weaken tests, stop and ask before proceeding.

## Conventions

- TypeScript strict mode; avoid `any`.
- Smallest change that solves the problem; no drive-by refactors.
- One logical change per commit, with a clear prefixed message.

For the full reasoning behind these rules, see
[`CLAUDE.md`](./CLAUDE.md) and
[`../../guardrails/agents-md-starter.md`](../../guardrails/agents-md-starter.md).
