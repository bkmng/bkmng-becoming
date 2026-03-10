---
id: decision-003
becoming_type: Decision
label: Three-repo documentation structure with distinct roles
occurred_at: "2026-03-10"
status: active
made_by: actor-founding-team
rationale: >
  The three repos have genuinely different editorial natures: formal spec,
  stable encyclopedia, and live journal are different things.
  Conflating them would obscure the boundary between the public standard
  (Becoming) and the private project knowledge (BKMNG).
based_on:
  - assumption-d003-1
  - assumption-d003-2
commits_to:
  - activity-model-specification
  - activity-live-journal
eliminates: []
assumptions:
  - id: assumption-d003-1
    becoming_type: Assumption
    assumption_type: activity
    predicate: >
      Maintaining discipline to write bkmng-becoming/ entries as formal
      Becoming records will be sustainable with Copilot assistance.
    confidence: medium
    formed_at: "2026-03-10"
    attached_to: activity-live-journal
  - id: assumption-d003-2
    becoming_type: Assumption
    assumption_type: resource
    predicate: >
      The cognitive overhead of three repos is manageable given
      clear role definitions.
    confidence: medium
    formed_at: "2026-03-10"
    attached_to: resource-bkmng-becoming-instance
---

## Repo roles

| Repo | Role | Nature |
|---|---|---|
| `becoming/` | Formal public spec (schema, primitives, ADRs) | Sparse, versioned, publishable |
| `bkmng-foundation/` | Project encyclopedia (vision, research, strategy) | Curated, stable |
| `bkmng-becoming/` | Live project journal in Becoming format | Append-oriented, dated records |

## Consequence

Model documentation moves from `bkmng-foundation/01-becoming/` → `becoming/`
(to be completed). `bkmng-foundation/01-becoming/` becomes a summary
referencing the formal spec.

`bkmng-becoming/` entries are always structured as Becoming records, not prose.
