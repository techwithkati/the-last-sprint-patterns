# Synthetic Full-Stack Repo: Taskboard

This is a **fictional** full-stack app. It does not exist as running code. It is here only as a backdrop so the `CLAUDE.md` and `AGENTS.md` next to it have something concrete to point at.

No real project, client, or codebase is described here. If you are adapting these files, replace every detail below with the truth about your own repo.

## The pretend app

**Taskboard** is a small team task tracker: boards, columns, and cards you can drag between columns.

Stack:

- **Frontend:** React + TypeScript + Vite, Tailwind for styling, React Router.
- **API:** Node + Express, REST under `/api`.
- **Database:** Postgres, reached through a thin repository layer (no ORM in the hot path).
- **Tests:** Vitest + Testing Library on the frontend, Vitest on the API.

## The pretend folder map

```txt
/
  client/
    src/
      components/        # shared UI
      features/          # board, column, card features
      lib/               # shared utilities
      types/             # shared TypeScript models
  server/
    src/
      routes/            # Express route handlers
      repo/              # database access layer (the persistence boundary)
      db/                # connection + migrations
  CLAUDE.md
  AGENTS.md
```

## How to use these files

1. Copy `CLAUDE.md` and `AGENTS.md` into the root of your own repo.
2. Replace the taskboard specifics with your real stack, paths, and boundaries.
3. Delete any rule you will not actually enforce.
4. Commit them, and change them through PRs like code.

For the reasoning behind each rule, see [`../../guardrails/agents-md-starter.md`](../../guardrails/agents-md-starter.md). For the full annotated long-form template, see [`../../claude-md/react-ts.md`](../../claude-md/react-ts.md).
