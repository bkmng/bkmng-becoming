---
id: decision-004
becoming_type: Decision
label: Split web presence into public company site and private demo app
occurred_at: "2026-03-10"
status: active
made_by: actor-founding-team
rationale: >
  The Becoming demo contains real strategic content that should not be
  publicly indexable. bkmng-web is the right place for a public company
  presence. A separate private application with authentication is the
  right place for the demo.
based_on:
  - assumption-d004-1
  - assumption-d004-2
commits_to:
  - activity-demo-construction
eliminates: []
assumptions:
  - id: assumption-d004-1
    becoming_type: Assumption
    assumption_type: resource
    predicate: >
      Maintaining two separate web applications (bkmng-web and bkmng-app)
      is manageable with shared brand tokens and separate deployment pipelines.
    confidence: high
    formed_at: "2026-03-10"
    attached_to: activity-demo-construction
  - id: assumption-d004-2
    becoming_type: Assumption
    assumption_type: actor
    predicate: >
      The public company site (bkmng.com) serves a different audience
      than the authenticated demo (app.bkmng.com) — these are not the
      same entry point.
    confidence: high
    formed_at: "2026-03-10"
    attached_to: actor-founding-team
---

## Context

`bkmng-web` was originally conceived as both the company site and the
demo front-end. As the demo took shape with real strategic content,
it became clear these should be separate: a public presence and a
protected working tool.

## Options considered

1. Keep everything in bkmng-web, add auth to specific routes
2. Split into two repos with separate deployments

## Decision

- `bkmng-web` → stripped back to a public company landing page, deployed on Vercel at bkmng.com
- `bkmng-app` → new private repo containing the Becoming demo, deployed on GCP with IAP at app.bkmng.com
- `bkmng-becoming` added as a git submodule in `bkmng-app`

## Consequence

The Becoming data is loaded at build time directly from the submodule.
No separate platform API or database layer is needed at this stage.
