---
id: decision-002
becoming_type: Decision
label: Build the demo by building BKMNG
occurred_at: "2026-03-10"
status: active
made_by: actor-founding-team
rationale: >
  Authentic content is more compelling than synthetic. There is no lag
  between doing the work and having demo content — they are the same thing.
based_on:
  - assumption-d002-1
  - assumption-d002-2
commits_to:
  - activity-demo-construction
  - activity-live-journal
eliminates:
  - activity-synthetic-demo
assumptions:
  - id: assumption-d002-1
    becoming_type: Assumption
    assumption_type: actor
    predicate: >
      NHH faculty and collaborators will find a real strategy example
      more credible than a synthetic one.
    confidence: high
    formed_at: "2026-03-10"
    attached_to: activity-nhh-engagement
  - id: assumption-d002-2
    becoming_type: Assumption
    assumption_type: activity
    predicate: >
      Building the demo with real content will accelerate model refinement —
      friction with actual strategy will reveal gaps faster than a curated example.
    confidence: high
    formed_at: "2026-03-10"
    attached_to: activity-demo-construction
---

## Context

A demo is needed to communicate the value of Becoming to NHH and
collaborators. The question was what content to use.

## Options considered

1. Build a synthetic demo with fictional company data
2. Build the demo using BKMNG's own strategic work as content

## Decision

The demo is BKMNG's own strategy, represented in Becoming.
`bkmng-web/` will visualize data drawn from this repository.
No synthetic demo scenarios until a real one exists.
