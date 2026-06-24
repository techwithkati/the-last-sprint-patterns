# The Last Sprint Patterns

Guardrails, checklists, and workflows for using AI coding agents — Claude Code, Codex — in real codebases without losing control of the diff.

AI is the entry point. Trustworthy code is the point.

This is the public workbench for [The Last Sprint](https://thelastsprint.dev). Everything here is something I use on real work and would point at.

## Who this is for

Intermediate-to-senior full-stack developers — solo, freelance, and small-team engineers — running coding agents in existing, production-style repos. If you care about repo guardrails, reviewable diffs, and safer refactors more than AI hype, this is for you.

## Start here

- `guardrails/agents-md-starter.md` — the minimum useful CLAUDE.md + AGENTS.md, and the few rules that actually change agent behavior
- `examples/synthetic-fullstack-repo/` — a filled CLAUDE.md + AGENTS.md you can copy and adapt
- `claude-md/react-ts.md` — the long-form annotated React + TypeScript CLAUDE.md template
- `patterns/react-ts-claude-md.md` — section-by-section walkthrough of that template
- `checklists/codebase-review.md` — what I check when I take over an unfamiliar codebase
- `skills/` — Claude Skills, added once they have earned their place on real work

## What's next

One useful artifact a week, working through: agent instruction starters, an AI PR-review checklist, repeatable debugging and refactor workflows, and the first shipped Claude Skill.

## How this connects to The Last Sprint

The Last Sprint is about getting AI coding agents to work the way your repo already works, and shipping diffs you would still approve in review. These files are that idea made reusable. If you want it applied to a real codebase: https://thelastsprint.dev/work/

## How patterns earn their place

A file starts in draft. It moves to published only after I have used it to ship something I would point at. Every change to a published artifact is logged in `CHANGELOG.md`.

## Safety note

No employer code, employer architecture, proprietary logic, or private data is used here. Examples are generic or built from reusable practice.

## License

MIT. Use, copy, modify, and adapt these templates and patterns in your own projects. Keep the license notice when redistributing.
