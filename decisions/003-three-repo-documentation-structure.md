# Decision 003 — Three-repo documentation structure

**Date:** 2026-03-10  
**Status:** Active  
**Made by:** Founding team

---

## Context

Three documentation repositories exist with overlapping scope: `becoming/`, `bkmng-foundation/`, and `bkmng-becoming/`. There was a question about whether all three are needed, and where the lines between them should be.

## Options considered

1. Collapse `bkmng-becoming/` into `bkmng-foundation/`
2. Keep all three with clearer role definitions
3. Collapse `bkmng-foundation/` into the other two

## Decision

Keep all three repositories with sharply defined roles:

- **`becoming/`** — formal public specification of the model (schema, primitives, ADRs). Sparse, versioned, publishable as a standard. No project history or rationale.
- **`bkmng-foundation/`** — comprehensive project encyclopedia (vision, problem, research, strategy, intellectual foundations, collaborators). Curated, stable. References `becoming/` for the formal spec; does not duplicate it.
- **`bkmng-becoming/`** — live project journal. Dated entries using Becoming primitives. Decisions, observations, directions. Append-oriented. This repo is the demo artefact.

## Rationale

1. The three repos have genuinely different editorial natures — formal spec, stable encyclopedia, and live journal are different things
2. Collapsing them would conflate the public standard (Becoming) with the private project knowledge (BKMNG)
3. `bkmng-becoming/` only has value if it is written *as Becoming records*, not as free-form notes — keeping it separate enforces this discipline

## Assumptions

- **Activity assumption:** Maintaining discipline to write `bkmng-becoming/` entries in Becoming format will be sustainable with Copilot assistance
- **Resource assumption:** The cognitive overhead of three repos is manageable given clear role definitions

## Expected results

- `becoming/` becomes a citable public artefact within 6 months
- `bkmng-foundation/` serves as the primary briefing doc for all AI tooling
- `bkmng-becoming/` grows into a navigable record of the project's evolution

## Commits to

- Model documentation moves from `bkmng-foundation/01-becoming/` → `becoming/` (to be completed)
- `bkmng-foundation/01-becoming/` becomes a summary that references the formal spec
- `bkmng-becoming/` entries are always structured as Becoming records, not prose notes
