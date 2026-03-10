---
id: decision-001
becoming_type: Decision
label: Use Becoming to document the BKMNG project itself
occurred_at: "2026-03-10"
status: active
made_by: actor-founding-team
rationale: >
  Building the model while using it produces the fastest feedback loop
  and the most authentic demo content.
based_on:
  - assumption-d001-1
  - assumption-d001-2
  - assumption-d001-3
commits_to:
  - activity-live-journal
eliminates: []
assumptions:
  - id: assumption-d001-1
    becoming_type: Assumption
    assumption_type: actor
    predicate: >
      The founding team will find Becoming-structured documentation more useful
      than unstructured prose over time.
    confidence: medium
    formed_at: "2026-03-10"
    attached_to: activity-live-journal
  - id: assumption-d001-2
    becoming_type: Assumption
    assumption_type: activity
    predicate: >
      Writing decisions in Becoming format will surface model gaps faster
      than theorizing in isolation.
    confidence: high
    formed_at: "2026-03-10"
    attached_to: activity-live-journal
  - id: assumption-d001-3
    becoming_type: Assumption
    assumption_type: result
    predicate: >
      This repo will serve as compelling evidence of the model's value
      for NHH and collaborators.
    confidence: medium
    formed_at: "2026-03-10"
    attached_to: result-nhh-pilot-conversation
---

## Context

BKMNG is building a tool for explicit organizational self-representation.
The question arose: should we use the tool for our own strategic work,
or wait until the platform is mature enough?

## Options considered

1. Wait until the platform is built before using Becoming for internal work
2. Use Becoming immediately, even in document form

## Decision

Use Becoming immediately — `bkmng-becoming/` is the first live instance
of a Becoming model.
