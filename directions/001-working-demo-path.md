# Direction — Working demo path

**Date:** 2026-03-10  
**Status:** Active exploration  
**Type:** Direction

---

## The question

What is the minimum viable path from current state to a working, meaningful demo that can be shown to NHH faculty and potential collaborators?

## Constraints

- No backend team yet — solo or small founding team
- The demo must show Becoming working on real strategy content, not toy examples
- It should be navigable without explanation (or with minimal explanation)

## Proposed path

### Step 1 — Formal schema as TypeScript types

Create `bkmng-platform/` with TypeScript type definitions derived from `becoming/schema/types.md`.

This is the source of truth for the data shape. Everything downstream depends on it.

### Step 2 — Seed data from this project

Create a JSON or TypeScript seed file that represents BKMNG's own strategy as a Becoming instance:
- the core decisions (captured in this repo)
- the key assumptions (resource, actor, result)
- the main activities (building the model, building the platform, NHH engagement)
- expected and observed results

### Step 3 — Static demo view in bkmng-web

Use the seed data to build a read-only Astro-based web view:
- Decision map: what major decisions have been made, and what they commit to
- Assumption tracker: what are we betting on, and what is the confidence level
- Timeline: how has the model evolved (model versions)

### Step 4 — Interactive editing (later)

Once the static view is validated, add the ability to edit and extend the model in the browser. This is where `bkmng-platform/` becomes a real API.

## Key assumption

This whole path assumes that a static, read-only demo with real content is more valuable for the NHH audience than a flexible but empty interactive system.

This assumption should be tested in the first NHH conversation.

## Open questions

- Should the demo be publicly accessible (hosted on GCP) or only a local preview for now?
- What view is most compelling for a strategy/entrepreneurship audience — the decision map, the assumption tracker, or the temporal evolution?
- Who is the right NHH contact for a first conversation?
