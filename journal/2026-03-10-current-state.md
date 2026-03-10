# Journal — 2026-03-10 — Current state of BKMNG

**Type:** Observation  
**Observed at:** 2026-03-10

---

## Current observed state

The BKMNG project has a strong conceptual foundation but no working implementation.

**What exists:**
- A mature knowledge base (`bkmng-foundation/`) covering vision, problem framing, intellectual foundations, research, and commercialization direction
- A formal model specification (`becoming/`), now populated with ontology, concepts, schema, and design decisions
- A minimal web frontend (`bkmng-web/`) — Astro, TypeScript, landing page only
- Infrastructure placeholder (`bkmng-infra/`) — no implementation
- Working documentation repo (`bkmng-becoming/`) — now being used

**What does not exist yet:**
- `bkmng-platform` — backend, data model, API
- `bkmng-ai` — AI context, prompt library, Copilot instructions
- `bkmng-experiments` — prototypes and pilots
- Any working demo
- Any external users or validators beyond the founding team

## Open questions

1. What is the right first implementation target — a static data demo or a live editable system?
2. How do we represent model versions in the data layer — as snapshots, branches, or tags?
3. What is the simplest schema implementation that would support a credible NHH pilot?
4. Should `bkmng-ai/` be a separate repo or a directory within `bkmng-platform`?

## Next expected events

- Populate `bkmng-becoming/` with first decisions and directions
- Create `bkmng-platform` repo with TypeScript schema
- Seed the platform with BKMNG's own strategy as a Becoming instance
- Wire `bkmng-web/` to the seeded data for a first demo view
