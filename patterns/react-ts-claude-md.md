# Walkthrough: The React + TypeScript CLAUDE.md

A section-by-section read of [`claude-md/react-ts.md`](../claude-md/react-ts.md): what each section is for, the failure it prevents, and how to adapt it to your repo.

A CLAUDE.md is a working agreement between you and a coding agent. It is not a prompt and not a style guide. It is the set of constraints you would give a careful contributor on their first day, written down so the agent reads them every time, not just when you remember to say them.

## How to use it

1. Copy `react-ts.md` to `CLAUDE.md` at the root of your repo.
2. Replace every `[BRACKETED]` placeholder with the truth about your project.
3. Delete sections that do not apply. A rule you do not mean is worse than no rule.
4. Commit it, and change it through PRs. Treat it like code.

If you keep a rule you do not enforce, the agent learns the whole document is decorative.

## Section by section

### 1. Project Context

**What it does:** tells the agent what the project is before it edits anything.

**Failure it prevents:** with no context, the agent falls back to generic React patterns from training that may not match your codebase, and quietly expands scope.

**How to adapt:** be specific about stack, structure, and goals. The last line, "do not expand the project scope unless explicitly asked," is doing real work. Keep it.

### 2. Stack Constraints

**What it does:** overrides the agent's training defaults with the decisions your project has already made.

**Failure it prevents:** unrequested state-management libraries, a second UI kit, a quiet routing change, `any` scattered through shared models.

**How to adapt:** list the conventions someone could not guess from a single file. If your repo already uses a date library or a data-fetching layer, say so here so the agent reaches for it instead of adding another.

### 3. Do-Not-Touch Zones

**What it does:** names the files and folders that are load-bearing, so the agent does not casually regenerate them.

**Failure it prevents:** persistence, shared types, build config, and env files edited without anyone noticing, until production.

**How to adapt:** this is the most project-specific section. Name your real persistence boundary, your data-access layer, and anything where a careless change affects saved data or money. Pair it with the escape hatch in section 4.

### 4. Escape Hatch Phrase

**What it does:** gives the agent one explicit stop phrase, `STOP, escape hatch triggered`, and a list of exactly when to use it.

**Failure it prevents:** the agent guessing when it is unsure instead of surfacing the decision to you.

**How to adapt:** keep the phrase verbatim so it is easy to grep for in a transcript. Add triggers that match your risks. The point is a clear pause-and-ask boundary, not a longer document.

### 5. Code Change Rules

**What it does:** makes changes smaller, more boring, and easier to read.

**Failure it prevents:** the change that works in the demo but is impossible to review: a whole-file rewrite for a one-line fix, refactoring smuggled in with a feature, renamed symbols you did not ask for.

**How to adapt:** the "identify files that will change, files that should not, tests, and risk level before editing" step is the spine of a reviewable diff. Keep it even if you trim the rest.

### 6. Testing Rules

**What it does:** defines what "done" means, so tests are not treated as optional.

**Failure it prevents:** assertions weakened or tests deleted to make a change pass, and tests that check implementation details instead of behavior.

**How to adapt:** match the tools you actually use. The rule that matters most is "fix the code first, only change the test if the expected behavior changed intentionally."

### 7. Dependency Rules

**What it does:** forces a justification before a new dependency is added.

**Failure it prevents:** a package pulled in for something a small local utility would handle, growing the surface area you have to maintain.

**How to adapt:** keep the four questions (problem, why existing code cannot solve it, maintenance cost, smaller alternative). They are quick to answer when a dependency is genuinely warranted and slow when it is not, which is the point.

### 8. Commit Rules

**What it does:** keeps commit history readable and reviewable.

**Failure it prevents:** vague commits like "update files" that hide what changed.

**How to adapt:** swap in your team's convention if you have one. One logical change per commit matters more than the exact prefix style.

### 9. PR Description Rules

**What it does:** gives a fixed PR format that names risk and verification.

**Failure it prevents:** a generated change that ships because tests passed, not because anyone walked the diff.

**How to adapt:** the "manual review checklist" block at the end is the moment a human reads the diff on purpose. If you keep one thing from this section, keep that.

## When to revise it

A CLAUDE.md is wrong the moment your project changes and the file does not. Revise it when a rule gets in the way repeatedly, when the agent makes the same mistake twice, or when a new convention becomes load-bearing. Log meaningful changes the way you would log a code change.

Make it survive past the demo.
