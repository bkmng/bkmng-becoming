# 2026-03-19 — Domain service live, strategy model reseeded

**Type:** Observation
**Status:** confirmed

## What happened

Over March 18-19, the BKMNG platform moved from a static demo to a live, AI-powered domain service with full CRUD capabilities. The key milestones:

1. **bkmng-service deployed** (v0.5.1) — A Node.js/TypeScript service on Cloud Run with 20 domain tools (6 read, 11 write, 3 lifecycle), PostgreSQL 16 with pgvector, and Vertex AI Gemini integration (`gemini-2.5-flash`).

2. **Conversational AI interface working** — Split-pane UI with chat on the left and dynamic model view (overview, entities, decisions, assumptions, graph) on the right. The AI acts as advisor+secretary per the Becoming spec.

3. **Strategy as first-class concept** — Strategy CRUD (create, rename, archive) with sidebar management UI. All model content scoped to strategy. Conversations carry strategy context.

4. **Model lifecycle implemented** — Full object lifecycle: `draft -> proposed -> confirmed -> deprecated/rejected`. Lifecycle tools (`deprecate_object`, `reject_object`, `remove_relation`) enable the model to evolve. Deprecated content filtered from all read operations and AI context.

5. **Strategy model reseeded** — Replaced execution-level seed (14 entities, 15 events, 20 assumptions about repos, infrastructure, deployment) with core strategic choices per Van den Steen's definition: 1 Resource, 4 Decisions, 3 Assumptions, 4 Relations.

## Core strategic model (v2)

- **Resource:** Becoming Core Architecture (conversational AI + structured knowledge base + integrated tooling)
- **Decisions:** Model scope as core choices, epistemic chain extension, early adopter focus, conversational interface priority
- **Assumptions:** Core architecture enables high-value activities (high), curated knowledge beats RAG (medium), epistemic types add value without complexity (medium)

## Architecture decisions confirmed

- Modular monolith: AI layer directly in bkmng-service, not a separate prompt service
- Path-based routing: `/api/*` -> bkmng-service, default -> bkmng-app, shared IAP
- Scope injection: `workspace_id` and `strategy_id` injected server-side, not in Gemini tool declarations
- Enum constraints on all Gemini tool parameters to reduce hallucination

## What we learned

- **Gemini parameter hallucination** is a real problem. `workspace_id` had to be removed entirely from tool declarations because Gemini would substitute labels for UUIDs. Scope injection from conversation context is the correct pattern.
- **SQL NULL traps** in NOT IN clauses: `NULL NOT IN ('deprecated', 'rejected')` evaluates to NULL, not TRUE. Must use `(column IS NULL OR column NOT IN (...))`.
- **PL/pgSQL variable name collisions**: Using `strategy_id` as both a variable name and column name causes ambiguity errors. Use distinct variable names.
- **Migration idempotency requires excluding new IDs from deprecation UPDATEs**: Otherwise re-runs deprecate the content they just inserted.

## Open questions

1. How should the internal strategy structure work? The vision doc describes Strategic Intent -> Strategic Theme -> Goal -> Hypothesis -> Activity -> Observation -> Learning, but this is a future concern.
2. When do we need multiple workspaces in practice?
3. What is the right balance between AI autonomy and user control in the confirmation flow?

## Next expected events

- First real strategic conversation using the live system
- Feedback from NHH session
- Expand the core strategic model through guided conversations
