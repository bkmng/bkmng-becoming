---
id: decision-008
becoming_type: Decision
label: Domain service as a dedicated repository with zero-framework HTTP API
occurred_at: "2026-03-18"
status: active
made_by: actor-founding-team
rationale: >
  The domain tools layer — the controlled interface between AI/user intent and the
  Becoming model — is implemented as a standalone Node.js/TypeScript service in
  bkmng-service. The decision to use a dedicated repo (vs. embedding in bkmng-app)
  follows the repo-per-concern pattern established in ADR-003. The HTTP API uses
  Node.js built-in http module with zero framework dependencies beyond pg (PostgreSQL
  client), keeping the attack surface small and the dependency count minimal. All 17
  domain tools are exposed via POST /tools/{name} with JSON bodies.
based_on:
  - assumption-id: assumption-tools-over-tables
    assumption_type: activity
    predicate: "The 'tools over tables' principle requires a service boundary that validates, audits, and mediates all model access"
    confidence: high
    formed_at: "2026-03-18"
    attached_to: activity-domain-service-development
  - assumption-id: assumption-minimal-dependencies
    assumption_type: resource
    predicate: "A zero-framework approach reduces maintenance burden and security surface for a single-developer project"
    confidence: high
    formed_at: "2026-03-18"
    attached_to: resource-bkmng-service
commits_to:
  - activity-domain-service-development
  - resource-bkmng-service
eliminates: []
---

# Domain Service Implementation

## Context

ADR-006 committed to a modular monolith on Cloud Run. ADR-007 extended the Becoming model with the epistemic chain and knowledge layer. This decision records how these commitments were realized as working code.

## Decision

1. **Dedicated repository** (`bkmng-service`): The domain service lives in its own repo, matching the repo-per-concern pattern (ADR-003). This allows independent deployment and versioning.

2. **Zero-framework HTTP API**: Uses Node.js `http` module directly. The only runtime dependency is `pg` (PostgreSQL client). This means:
   - No Express, Fastify, or Hono
   - No ORM — raw SQL with parameterized queries
   - No middleware chain — just a request handler with pattern matching

3. **17 domain tools**: All tools from the domain-tools.md specification are implemented:
   - 6 read tools (safe, direct execution)
   - 11 write tools (transactional, with domain event logging)

4. **Database schema as migration**: The complete 20-table schema (core + prompt + knowledge) is a single SQL migration file, tracked by a `_migrations` table.

5. **Cloud SQL Auth Proxy**: Production connection via Unix socket (no public IP), local dev via TCP.

## Consequences

- The service can be deployed and scaled independently of the frontend
- All model access is mediated and audited — no direct database access from other services
- The MCP facade (future) can wrap this service without redesign
- The zero-framework approach means hand-writing concerns that frameworks typically handle (CORS, request parsing, etc.) — acceptable for the current scope
