# 2026-03-23 — Strategic framework analysis tab deployed

**Type:** Observation
**Status:** confirmed

## What happened

Over March 20-23, the BKMNG platform gained a complete strategic framework analysis capability, implementing 7 analyses from Lasse Lien's "Strategiboken." This is the centerpiece feature for the planned NHH demo.

### Backend: 7 framework analyses + orchestrator

Created `analyzeSvima()`, `analyzeFiveForces()`, `analyzeActivitySystem()`, `analyzePositioning()`, `analyzeValueChain()`, `analyzeStrategicGroups()`, `analyzeMarketSegments()`, plus `analyzeFrameworks()` orchestrator that runs all 7 in parallel. All share a `fetchModelData()` helper that fetches entities, events, relations, and assumptions in parallel and builds adjacency maps + text search helpers.

Each analysis uses keyword matching (Norwegian + English bilingual) to map model elements to framework concepts. Returns structured results with assessments, issues (critical/warning/info), evidence, and guidance.

Total: 8 new tool registrations, ~1300 lines of analysis logic.

### Frontend: Analysis tab with framework renderers

Created `src/features/model/analysis.ts` with the full FRAMEWORKS registry (7 entries), `loadAnalysis()`, `renderAnalysis()`, `initAnalysisControls()`, and 7 framework-specific renderers:

- **SVIMA**: Matrix table with S-V-I-M-A columns, score dots, implication tags, assumption counts
- **Five Forces**: Force cards with intensity indicators, actor links, assumption quotes
- **Activity System**: Activity cards showing core/supporting roles, reinforcement links, fit type assessment
- **Positioning**: 2x2 matrix (cost/differentiation x broad/focus), signal counts, quadrant highlighting
- **Value Chain**: Horizontal flow diagram with stage cards, element counts, flow arrows
- **Strategic Groups**: Competitor cards with strategic assumptions
- **Market Segments**: Segment cards with served/identified status, segment choice decisions

Each renderer includes a collapsible documentation section with:
- The key strategic question the framework answers (always visible)
- "What is [framework]?" explanation (expandable)
- "How to use this analysis" instructions (expandable)
- Strategiboken chapter reference

### Other changes

- Added `analysis` to SPA router tab set
- Added analysis state variables to `src/lib/state.ts`
- Wired analysis lazy-loading in `src/features/layout/tabs.ts`
- Simplified `knowledge.ts` to domain knowledge only (removed Observation/Interpretation/Learning UI)
- ~580 lines of CSS for all framework renderers
- Fixed SVIMA column order to match acronym: S, V, I, M, A (was V, S, I, M, A)
- Translated all Norwegian UI strings to English across backend and frontend

### Tool count growth

The service now has 42 domain tools (was 20 at the March 19 observation):
- 9 read (was 6, added `search_relations`, `get_event`, `get_expectation`)
- 18 write (was 11 + 3 lifecycle, added 4 update tools)
- 5 general analysis (new)
- 8 strategic framework analysis (new)
- 2 knowledge (new)

## Architecture patterns confirmed

- **Shared `fetchModelData()` helper**: All framework analyses reuse one function that parallel-fetches all model data. Avoids N+1 queries and ensures consistent data across analyses.
- **Bilingual keyword matching**: Norwegian arrays for user content matching (users model in Norwegian), English for UI display. This separation works well.
- **Framework registry pattern**: Client-side registry with id, label, icon, chapter, description, question, howToUse, and render function. Clean extensibility for future frameworks.
- **Collapsible documentation**: Each analysis includes its own guide. Users can learn the framework without leaving the tool.

## Commits

- `6d077b8` (bkmng-service): "feat: 7 strategic framework analyses (SVIMA, Five Forces, Activity System, Positioning, Value Chain, Strategic Groups, Market Segments)"
- `2e9fdb2` (bkmng-app): "feat: analysis tab with 7 framework renderers, collapsible documentation guides, SVIMA column order fix"

## What we learned

- **SVIMA is not VRIO**: The Norwegian framework adds Appropriability (A) and uses a different dimension order (S-V-I-M-A). The sequential evaluation cascade matters — a resource must pass each test in order to qualify for the next level of advantage.
- **Framework analyses are data-hungry**: With a thin model, most frameworks show mostly empty states and "unknown" scores. The value becomes apparent only with richer model content.
- **Module-level type exports required**: TypeScript interfaces used in exported function return types must be at module level, not inside functions.

## Next expected events

- NHH demo with Lasse Lien
- Enrich the strategic model to show richer framework analysis results
- Potential additions: PESTEL, Generic Strategies matrix, Resource-Activity mapping
