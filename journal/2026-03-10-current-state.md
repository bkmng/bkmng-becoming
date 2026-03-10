---
id: observation-2026-03-10
becoming_type: Observation
label: Current state of BKMNG — March 2026
observed_at: "2026-03-10"
confirms: []
disconfirms: []
updates:
  - resource-bkmng-foundation
  - resource-becoming-formal-model
  - activity-model-specification
---

## Current observed state

**What exists:**

- `resource-bkmng-foundation` — mature (30 files, vision, research, strategy, collaborators)
- `resource-becoming-formal-model` — now populated (ontology, concepts, TypeScript schema, ADRs)
- `resource-bkmng-web-frontend` — minimal (Astro landing page only)
- `resource-bkmng-becoming-instance` — started (this repo, first records written today)

**What does not exist yet:**

- `bkmng-platform` repo — no data layer, no API
- `bkmng-ai` repo — no Copilot instructions, no prompt library
- `result-working-demo` — not yet realized
- `result-nhh-pilot-conversation` — not yet realized

## Open questions

1. What is the right first implementation target — static seed data or live editable system?
2. How should model versions be represented in the data layer — snapshots, branches, or tags?
3. What is the minimum schema implementation for a credible NHH pilot?

## Next expected events

- Create `bkmng-platform/` with TypeScript data layer importing `@bkmng/becoming`
- Seed with BKMNG's own strategy as a Becoming instance
- Connect `bkmng-web/` to seeded data for a first demo view
