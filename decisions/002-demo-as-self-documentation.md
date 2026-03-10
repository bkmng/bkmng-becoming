# Decision 002 — Build the demo by building BKMNG

**Date:** 2026-03-10  
**Status:** Active  
**Made by:** Founding team

---

## Context

A demo is needed to communicate the value of Becoming to external audiences — NHH, collaborators, potential users. The question was: what should the demo show, and where does the content come from?

## Options considered

1. Build a synthetic demo with fictional company data
2. Build the demo using BKMNG's own strategic work as content

## Decision

The demo is BKMNG's own strategy, represented in Becoming.

The web frontend (`bkmng-web/`) will visualize BKMNG's own decisions, assumptions, activities, and results — as captured in this repository.

## Rationale

1. Authentic content is more compelling than synthetic content
2. There is no lag between "doing the work" and "having demo content" — they are the same thing
3. This forces the model to work on a real, live strategy, not a curated toy example
4. Founders can explain the demo from direct experience, not from a constructed narrative

## Assumptions

- **Actor assumption:** Observers (NHH faculty, collaborators) will find a real strategy example more credible than a synthetic one
- **Activity assumption:** Building the demo this way will accelerate model refinement — friction with the real strategy will reveal gaps
- **Result assumption:** The demo will be ready for an NHH conversation before a full platform implementation is needed

## Expected results

- A working demo by the time of the first NHH pilot conversation
- A Becoming model of BKMNG that is honest, complete enough to be navigable, and instructive

## Commits to

- `bkmng-web/` will visualize data from the BKMNG Becoming instance
- `bkmng-platform/` seed data = BKMNG's own strategy
- No synthetic demo scenarios until a real one exists
