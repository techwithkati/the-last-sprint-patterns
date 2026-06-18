# Codebase Review Checklist

What I check when I take over a codebase I did not write, before I change anything.

The goal of a first pass is not to fix things. It is to learn what is load-bearing, what is fragile, and where the surprises are, so the first change is not the one that breaks production.

## 1. Get it running

- [ ] Clone, install, and run the app from a clean checkout, following only the README.
- [ ] Note every undocumented step the README is missing.
- [ ] Find how it is built and deployed, and where production actually runs.
- [ ] Locate environment config and how secrets are handled. Do not read secret values.

## 2. Map the shape

- [ ] Identify the entry points: routes, pages, jobs, or API surface.
- [ ] Find the data layer and how persistence works.
- [ ] Find the shared types or models that ripple across the app.
- [ ] Note the boundaries: where the app talks to a database, an API, or a third party.

## 3. Find the load-bearing and the fragile

- [ ] List the files that, changed carelessly, affect saved data or money.
- [ ] Find code with no tests around behavior users depend on.
- [ ] Spot copy-paste duplication that will drift out of sync.
- [ ] Note any "do not touch, it just works" areas and ask why.

## 4. Check the safety net

- [ ] Run the test suite. Record what passes, fails, and is skipped.
- [ ] Check whether tests assert behavior or just confirm the code runs.
- [ ] Find the type checker and linter config, and whether they are enforced in CI.
- [ ] Confirm there is a way to roll back a bad deploy.

## 5. Read the history

- [ ] Skim recent commits and PRs for how the team works.
- [ ] Look for repeated reverts or hotfixes around the same area. That is where the risk lives.
- [ ] Note who to ask about the parts no document explains.

## 6. Write it down

- [ ] A one-page map: entry points, data layer, risky zones, missing tests.
- [ ] A short list of safe first changes that build confidence.
- [ ] The questions you could not answer from the code alone.

A first change should be small, reversible, and in a well-tested area. Save the scary part of the codebase for after you have earned a map of it.

Make it survive past the demo.
