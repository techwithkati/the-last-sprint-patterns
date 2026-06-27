# Changelog

All notable changes to The Last Sprint Patterns will be documented here.

This repo tracks public artifacts for The Last Sprint: CLAUDE.md templates, Claude Skills, named patterns, and supporting docs.

## 2026-06-26

### Added

- `checklists/ai-assisted-refactor.md`: a checklist for using a coding agent to refactor in a real repo without losing control of the diff. Covers when to use it and when not to, a plan-first prompt, what to watch during the refactor, verification checks, a review prompt, PR notes, and a final merge checklist. Frames AI-assisted refactoring as still refactoring: preserve behavior, keep it small enough to review, verify with tests, lint, typecheck, and a diff read.

## 2026-06-24

### Removed

- `claude-md/react-ts.md`: the long-form React + TypeScript CLAUDE.md template.
- `patterns/react-ts-claude-md.md`: the section-by-section walkthrough of that template.

### Notes

- These were an earlier, second CLAUDE.md track that overlapped the agent instruction starter. The guardrails starter in `guardrails/agents-md-starter.md` is now the single entry point for agent instructions, and links that pointed at the retired files were updated or removed.

## 2026-06-23

### Added

- `guardrails/agents-md-starter.md`: the minimum useful CLAUDE.md + AGENTS.md, the 5 to 7 rules that matter most, a before/after example, and how to adapt it.
- `examples/synthetic-fullstack-repo/`: a fictional taskboard app with a filled, copy-ready `CLAUDE.md` and `AGENTS.md`.

### Changed

- `README.md` repositioned around using AI coding agents in real codebases without losing control of the diff, with a "who this is for" and "what's next" section.

### Notes

- The synthetic taskboard repo is fictional. No real project, client, or codebase is described.

## 2026-06-18

### Added

- `checklists/codebase-review.md`: checklist for taking over an unfamiliar codebase before making changes.
- `patterns/react-ts-claude-md.md`: section-by-section walkthrough of the React + TypeScript CLAUDE.md template.
- `skills/README.md`: what the skills folder is for and what is planned.

### Changed

- `README.md` rewritten around the open pattern library.
- `claude-md/react-ts.md` provenance updated: the template is maintained here directly.

### Notes

- The source lab has been retired. This repo is the public source of truth for reusable artifacts going forward; future updates come from tested patterns, recreated examples, or demo repos.

## 2026-05-19

### Added

#### `claude-md/react-ts.md` v1.0

Initial annotated CLAUDE.md template for React + TypeScript side projects.

Built from a synthetic React + TypeScript demo repo used to test CLAUDE.md patterns, Claude Skills, AI code review workflows, refactor patterns, and testing rules. The example was recreated or generalized so it could be shared publicly.

The template includes sections for:

- Project context
- Stack constraints
- Do-not-touch zones
- Escape hatch phrase
- Code change rules
- Testing rules
- Dependency rules
- Commit rules
- PR description rules
- Documentation rules
- Security and privacy rules
- When to ask vs. when to proceed
- Final verification before calling a task done

### Notes

- This is v1.0 of the reusable template, not a universal final version.
- Future updates should come from tested usage, broken assumptions, or repeated workflow patterns worth turning into Claude Skills.
