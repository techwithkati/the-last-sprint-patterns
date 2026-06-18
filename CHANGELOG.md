# Changelog

All notable changes to The Last Sprint Patterns will be documented here.

This repo tracks public artifacts for The Last Sprint: CLAUDE.md templates, Claude Skills, named patterns, and supporting docs.

## 2026-06-18

### Added

- `checklists/codebase-review.md` — checklist for taking over an unfamiliar codebase before making changes.
- `patterns/react-ts-claude-md.md` — section-by-section walkthrough of the React + TypeScript CLAUDE.md template.
- `skills/README.md` — what the skills folder is for and what is planned.

### Changed

- `README.md` rewritten around the freelance practice plus open library, with a pointer to https://thelastsprint.dev/work/.
- `claude-md/react-ts.md` provenance updated: the template is maintained here directly.

### Notes

- `tls-react-lab` has been archived. This repo is the single source of truth going forward; future updates come from real project work.

## 2026-05-19

### Added

#### `claude-md/react-ts.md` v1.0

Initial annotated CLAUDE.md template for React + TypeScript side projects.

Derived from the active `tls-react-lab/CLAUDE.md`, which is currently used in a public-safe React + TypeScript lab for testing CLAUDE.md patterns, Claude Skills, AI code review workflows, refactor patterns, and testing rules.

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
- The source lab file is `tls-react-lab/CLAUDE.md`.
- Future updates should come from real usage in `tls-react-lab`, broken assumptions, or repeated workflow patterns worth turning into Claude Skills.
