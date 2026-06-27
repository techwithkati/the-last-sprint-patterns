# AI-Assisted Refactoring Checklist

How to use a coding agent (Claude Code, Codex, Cursor, Copilot, or similar) to refactor code in a real repository without losing control of the diff.

AI-assisted refactoring is still refactoring. The goal has not changed: keep behavior stable, keep the change small enough to review, and verify it with the relevant tests, lint, typecheck, and a careful read of the diff. An agent makes the edits faster, but the parts that make a refactor safe are still yours to do.

## 1. When to use this checklist

- [ ] The change should preserve behavior, not add features. Same inputs, same outputs.
- [ ] You can describe the target shape of the code in a sentence or two.
- [ ] There is a way to tell whether behavior actually stayed the same: tests, a typecheck, or a manual path you can run.
- [ ] The blast radius is bounded enough that a human can read the whole diff.

## 2. When not to use it

- [ ] The behavior is supposed to change. That is a feature or a fix, not a refactor. Treat it as one.
- [ ] You cannot yet describe what "done" looks like. Plan the change first, then come back.
- [ ] The area has no tests and touches saved data or money. Add characterization tests around the current behavior, or write a manual verification plan, before refactoring.
- [ ] The refactor would sprawl across the codebase in one pass. Split it into reviewable steps first.

## 3. Before asking the agent to edit

- [ ] State the goal in one or two sentences: what shape the code should have when you are done.
- [ ] Name the files you expect to change, and the files that must not change.
- [ ] Start from a clean branch or commit so the agent's diff is easy to isolate.
- [ ] Confirm the current tests pass on a clean checkout, so you have a known-good baseline.
- [ ] Write down the exact commands that prove behavior held, for example `npm test`, `npm run typecheck`, `npm run lint`, or the repo-specific equivalents.
- [ ] Decide the risk level. If it touches a boundary (persistence, shared types, migrations, public API), agree on the approach before any edit.
- [ ] Decide what kind of refactor this is: move/rename, extraction, simplification, dependency cleanup, or test cleanup.

## 4. Plan-first prompt

Ask the agent to inspect and plan before it touches code. Read the plan, and correct it, before you let it edit.

```
We are doing a behavior-preserving refactor. Do not edit anything yet.

Goal: <one or two sentences describing the target shape of the code>

Use the existing project conventions. Do not reformat unrelated code, add dependencies, or change tests unless the plan calls for it.

First, inspect the relevant code and tell me:
1. The files you expect to change, and why.
2. The files that must NOT change (boundaries, shared types, persistence, public API).
3. How current behavior is verified here (which tests, typecheck, lint commands).
4. Any behavior that is hard to preserve, or any place the refactor could leak a
   behavior change.
5. The smallest first step that is reviewable on its own.

Then stop and wait for me to confirm the plan before editing.
```

## 5. During the refactor

Use a narrow edit prompt for each approved step.

```
We approved the plan. Now do only step <number/name>.

Constraints:
- Only edit these files: <files>
- Do not change public signatures, exported types, persistence, migrations, schemas, snapshots, or lockfiles unless listed above.
- Do not reformat unrelated code.
- Do not change tests unless I explicitly asked for it.
- Stop after this step and summarize the diff.
```

- [ ] Hold the agent to the planned files. If it wants to touch a file outside the plan, that is a stop-and-discuss, not a silent expansion.
- [ ] Keep each step small enough to review on its own. Prefer several reviewable commits over one large rewrite.
- [ ] Give the agent one refactor step at a time. Do not combine extraction, renaming, dependency changes, and test edits in the same pass.
- [ ] Do not let public signatures, exported types, or interfaces drift unless the plan said so.
- [ ] Watch for "while I was here" changes: renamed variables across unrelated files, reformatting, dependency additions. These hide the real diff.
- [ ] No lockfiles, generated files, snapshots, migrations, or schema files changed unless the plan explicitly included them.
- [ ] If the agent gets stuck and starts changing behavior to make something pass, stop. Re-plan instead of letting it improvise.

## 6. Verification checks

- [ ] The relevant tests pass, and they assert behavior, not just that the code runs.
- [ ] No tests were weakened, skipped, or deleted to get to green. If a test changed, it was to preserve the same behavior more clearly, not to accept new behavior.
- [ ] Typecheck passes with no new suppressions or `any` escapes added to silence it.
- [ ] Lint passes without new disable comments hiding the change.
- [ ] You ran the affected path manually if it is not fully covered by tests.
- [ ] You checked the risky behavior edges for this refactor: ordering, defaults, null/undefined, errors, permissions, async timing, and serialization.
- [ ] You reviewed the actual `git diff`, not only the agent's summary.
- [ ] No new dependency was pulled in for something existing code already handles.

## 7. Review prompt

Before merge, have the agent review its own completed refactor against the behavior-preserving bar. Treat its answer as input to your review, not a replacement for it.

```
You just completed a behavior-preserving refactor. Review the full diff as if you
were a reviewer who did not write it.

Tell me:
1. Anything in this diff that could change behavior, even subtly (edge cases, error
   handling, ordering, null/undefined, async timing).
2. Any file changed that was outside the stated plan, and why.
3. Any test that was weakened, skipped, or deleted, and whether that was justified.
4. Any public signature, exported type, or interface that changed.
5. Anything unrelated to the refactor that snuck in (renames, reformatting, new
   dependencies).

Be specific and point at lines. If something is risky, say so plainly.
```

## 8. PR notes

- [ ] State that this is a behavior-preserving refactor, and what behavior was preserved.
- [ ] List what changed in shape, and what intentionally did not change.
- [ ] Note how you verified it: tests run, typecheck, lint, and any manual path.
- [ ] Call out anything a reviewer should look at closely, including any boundary the change came near.

## 9. Final merge checklist

- [ ] The diff is one you would approve if someone else opened it.
- [ ] You read every file in the diff, not just the summary the agent gave you.
- [ ] Tests, typecheck, and lint pass in CI, not only locally.
- [ ] Behavior is unchanged by evidence, not by assertion.
- [ ] The change is small, reversible, and easy to roll back if it misbehaves in production.

A refactor is done when the code is in better shape and nobody downstream can tell anything moved. The agent can speed up the edits. It does not get to decide the refactor is done.

Make it survive past the demo.
