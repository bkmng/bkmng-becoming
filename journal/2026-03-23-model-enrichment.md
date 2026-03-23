# 2026-03-23 — Model enrichment and strategic honesty

**Type:** Decision + Observation
**Status:** confirmed

## What happened

Two major rounds of model changes to the BKMNG self-referential strategy:

### Round 1: Model enrichment for demo readiness

Ran `scripts/enrich-bkmng-model.cjs` to populate the model with enough data for all 7 framework analyses to show rich results. Added:
- 7 new Actor entities (competitors, supplier, customer segments)
- 2 new Resource entities (AI/LLM infrastructure, user insights)
- 2 new Result entities (customer value, market traction)
- 4 new Activity events (customer discovery, content curation, academic collab, platform ops)
- 3 new Decision events (focus niche, differentiation over cost, academic-first)
- 18 new Assumptions (SVIMA keywords, Five Forces intensity, positioning)
- 37 new Relations (activity-to-activity for Activity System fit, resource-to-result for SVIMA, decision chains)

Fixed backend keyword matching:
- Removed 'startup' from Five Forces `new_entrants` keywords (was matching customer segments)
- Tightened `buyer_power` keywords to avoid false positives from generic 'bargaining'
- Adjusted Positioning cost/diff threshold from 0.35/0.65 to 0.40/0.60

Added SVIMA `implication_reason` — each resource assessment now explains in natural language what its implication means and why it was assigned. Frontend shows expandable detail rows.

### Round 2: Addressing strategic critiques

Three critiques of the model's honesty were addressed via `scripts/address-critiques.cjs`:

**Critique #1 — Missing core value proposition**: Updated strategy description to explicitly state "BKMNG exists to help people build the best possible strategy." Added Decision: "Phase 1: strategy formulation first, implementation support later" with causal justification for why phasing matters.

**Critique #2 — Aspirational customer segments presented as real**: 
- Updated 3 segment descriptions to be explicit about status (NOT YET SERVED / PARTIALLY SERVED)
- Expired "served" relations from system/value to Startup Founding Teams
- Reactivated 3 real near-term users: BKMNG Founders (Dogfooding), Lasse Lien, NHH Strategy Students
- Added relations showing who is actually served and the gatekeeper relationship (Lasse Lien → NHH Students)
- Added 3 honest assumptions including "startup WTP is UNVALIDATED" and "Lasse Lien is concentration risk"

**Critique #3 — Goodhart's Law risk**: Added 2 assumptions about the risk of users gaming framework scores instead of genuinely understanding their strategy. The key insight: "the AI must be Socratic, not generative."

## Post-change model state

| Element | Count |
|---------|-------|
| Active confirmed entities | ~25 (8 resources, 12 actors, 5 results) |
| Active events | ~15 (7 activities, 8 decisions) |
| Active assumptions | ~38 |
| Active relations | ~86 |

All 7 framework analyses verified working with correct results.

## Commits

- `c19eb66` (bkmng-service): "feat: enrich BKMNG model for demo + fix Five Forces and Positioning keyword thresholds"
- `cdfbfdf` (bkmng-service): "feat: SVIMA implication_reason"
- `0d8c9c7` (bkmng-app): "feat: expandable SVIMA implication details"
- Scripts: `enrich-bkmng-model.cjs`, `address-critiques.cjs`

## What we learned

- **Honesty in the model is itself a strategic asset**: A model that claims 3 served segments when there are 0 paying customers undermines the entire value proposition. The corrected model — showing founders dogfooding as the only truly served users — is more credible and surfaces real risks.
- **Keyword matching is fragile but workable**: The framework analyses depend on keyword matching against user-entered text. This creates false positives (e.g., 'startup' matching new_entrants when it appears in customer segment descriptions). Careful keyword curation and threshold tuning is necessary.
- **SVIMA implication chain is powerful when explained**: Just showing "Temporary Advantage" doesn't tell the user anything. Explaining "V=yes, S=yes, I=partial — the chain breaks at Inimitability because there's only partial evidence the resource is hard to copy" makes the assessment diagnostic.
- **Goodhart's Law is the deepest product risk**: If BKMNG becomes a tool that generates green checkmarks rather than one that surfaces hard questions, it fails at its core mission regardless of technical quality.

## Next expected events

- Demo preparation for Lasse Lien
- Consider whether the Market Segments analysis incorrectly classifies competitors (Notion, Miro) as customer segments
- Further UI refinements based on how the analyses look with real data
