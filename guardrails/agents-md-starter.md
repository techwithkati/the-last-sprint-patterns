# Agent Instruction Starter: CLAUDE.md + AGENTS.md

The minimum useful set of agent instructions for a full-stack repo, plus the few
rules that actually change how an agent behaves.

Most CLAUDE.md files are too long to be read and too vague to be enforced. This
starter is the opposite: a short, filled-in pair you copy, adapt in fifteen
minutes, and change like code. It is built against a fictional taskboard app so
every rule points at something concrete.

- Filled files to copy: [`../examples/synthetic-fullstack-repo/CLAUDE.md`](../examples/synthetic-fullstack-repo/CLAUDE.md) and [`AGENTS.md`](../examples/synthetic-fullstack-repo/AGENTS.md).
- The fictional repo they describe: [`../examples/synthetic-fullstack-repo/README.md`](../examples/synthetic-fullstack-repo/README.md).

## CLAUDE.md vs AGENTS.md: what goes where

They overlap, and that is fine. The split that works in practice:

- **`AGENTS.md`** is tool-agnostic and practical: how to install, run, test, type-check, and lint; where things live; the hard boundaries. Any agent (Claude Code, Codex, another) should be able to act from it. Keep it short and factual.
- **`CLAUDE.md`** is where the *reasoning* and the judgment rules live: the escape hatch, what "done" means, when to stop and ask. Claude reads it every turn.

Keep both. Put commands and the file map in `AGENTS.md`, put the working agreement in `CLAUDE.md`, and link rather than duplicate. If you only keep one, keep the one your primary agent reads every time.

## The rules that matter most

Out of everything you could write, these are the ones that change behavior. Each
exists to prevent a specific failure.

### 1. Project context up front
**Prevents:** the agent falling back to generic patterns from training and quietly expanding scope. Name the stack, the folder map, and "do not expand scope unless asked." That last line is doing real work.

### 2. Do-not-touch zones
**Prevents:** persistence, shared types, migrations, build config, and `.env` files getting edited without anyone noticing until production. Name your real boundaries: the data-access layer, applied migrations, anything that touches saved data or money.

### 3. The escape-hatch stop phrase
**Prevents:** the agent guessing when it is unsure instead of surfacing the decision. Give it one verbatim phrase, `STOP, escape hatch triggered`, so it is easy to grep for in a transcript, and a short list of exactly when to use it.

### 4. Name the diff before editing
**Prevents:** the change that works in the demo but is impossible to review. Before touching code, the agent states the files that will change, the files that must not, the tests to add, and the risk level. This one rule is the spine of a reviewable diff.

### 5. Do not weaken or delete tests to pass
**Prevents:** green CI that means nothing. Fix the code first; only change a test if the expected behavior changed on purpose. Prefer tests that assert what the user sees.

### 6. Justify new dependencies
**Prevents:** a package pulled in for something a small local utility would handle. Require four answers: the problem, why existing code cannot solve it, the maintenance cost, the smaller alternative.

### 7. (Optional) One logical change per commit
**Prevents:** vague commits like "update files" that hide what changed. Worth keeping if you review by reading history; drop it if your team squashes anyway.

If you keep nothing else, keep 2, 3, and 4. They are what stop an agent from quietly doing something you would not have approved.

## Before and after

The same task, with and without the starter in place.

**Task:** "Add a `dueDate` field to cards."

**Without guardrails:** the agent edits a card component, then reaches into the
shared types file, then "while it was there" rewrites the repository function
that saves cards, changes its signature, and updates three call sites, all in
one pass, no tests, reported as done. The diff touches the persistence boundary
and you find out in review, if you catch it at all.

**With the starter:** the agent stops first and says:

> Files I expect to change: `client/src/features/card/CardForm.tsx`, plus a test.
> `client/src/types/**` and `server/src/repo/**` are do-not-touch zones and this
> field needs both. **STOP, escape hatch triggered.** Adding `dueDate` to the
> stored shape means changing a shared type and the persistence layer. Risk:
> medium. Recommend we agree on the type change and a migration before I edit.

That pause is the whole point. The field still gets added, but as a change you
chose, with a diff you can review.

## Adapt it to your repo

1. Copy `CLAUDE.md` and `AGENTS.md` into your repo root.
2. Replace every taskboard specific (stack, paths, commands, boundaries) with the truth about your project.
3. Delete any rule you will not actually enforce. A rule you do not mean teaches the agent the whole document is decorative.
4. Commit them, and change them through PRs. Treat them like code.

## Keep it small

This starter is short on purpose. A working agreement you can read in one screen
gets followed; a config nobody finishes reading gets ignored. Resist the urge to
document everything. Add a rule only when the agent makes the same mistake
twice, or a new convention becomes load-bearing. When the file outgrows a screen,
that is usually a sign to cut, not to add.

Make it survive past the demo.
