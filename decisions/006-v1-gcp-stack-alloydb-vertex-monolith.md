---
id: decision-006
becoming_type: Decision
label: Cloud SQL PostgreSQL as operational database, Vertex AI for LLM, modular monolith on Cloud Run
occurred_at: "2026-03-18"
status: active
made_by: actor-founding-team
rationale: >
  The system architecture conversation committed to a concrete GCP stack for v1:
  Cloud SQL for PostgreSQL as the operational database (entities, relations, events,
  knowledge), Vertex AI Gemini for LLM inference, and a modular monolith on
  Cloud Run. Pub/Sub is explicitly deferred — domain events are stored as
  database rows. BigQuery is reserved for analytics projections later.
  Cloud SQL is chosen over AlloyDB for cost reasons — the schema is standard
  PostgreSQL and can be migrated to AlloyDB when workload justifies it.
based_on:
  - assumption-d006-1
  - assumption-d006-2
  - assumption-d006-3
  - assumption-d006-4
commits_to:
  - activity-platform-development
eliminates: []
assumptions:
  - id: assumption-d006-1
    becoming_type: Assumption
    assumption_type: resource
    predicate: >
      Cloud SQL for PostgreSQL provides sufficient performance and flexibility
      for the Becoming model at early stage — JSONB columns handle semi-structured
      model data, and standard PostgreSQL compatibility means migration to AlloyDB
      is seamless when scale or performance justifies the higher cost.
    confidence: high
    formed_at: "2026-03-18"
    attached_to: activity-platform-development
  - id: assumption-d006-2
    becoming_type: Assumption
    assumption_type: activity
    predicate: >
      Domain events stored as a database table (domain_event) are sufficient
      for v1 without a message bus. Pub/Sub can be added later when there are
      multiple independent consumers.
    confidence: high
    formed_at: "2026-03-18"
    attached_to: activity-platform-development
  - id: assumption-d006-3
    becoming_type: Assumption
    assumption_type: resource
    predicate: >
      Vertex AI Gemini provides adequate LLM capability for the guided
      conversational transaction loop — context assembly, tool routing,
      and knowledge-grounded responses.
    confidence: medium
    formed_at: "2026-03-18"
    attached_to: activity-platform-development
  - id: assumption-d006-4
    becoming_type: Assumption
    assumption_type: activity
    predicate: >
      A modular monolith on Cloud Run is the right starting architecture —
      splitting into microservices should happen only when there is a clear
      operational reason, not as an upfront design choice.
    confidence: high
    formed_at: "2026-03-18"
    attached_to: activity-platform-development
---

## Context

The previous infrastructure decision (005) established GCP Cloud Run + IAP for
the static demo. The system now needs to move beyond static site generation toward
a full application architecture with a database, LLM integration, and domain
service layer.

## Options considered

### Database
1. Firestore — document-oriented, good for rapid prototyping but poor for relational queries
2. Cloud SQL PostgreSQL — managed PostgreSQL, cost-effective, standard compatibility
3. AlloyDB for PostgreSQL — fully managed, PostgreSQL-compatible, better performance but significantly higher cost

### LLM
1. OpenAI API — external dependency, strong models
2. Vertex AI Gemini — GCP-native, integrated with IAM and other services
3. Self-hosted — too complex for v1

### Application architecture
1. Microservices from day one — premature complexity
2. Modular monolith — simple deployment, clear module boundaries, split later
3. Serverless functions — too fragmented for a domain-heavy application

## Decision

- **Cloud SQL for PostgreSQL** as operational database (migrate to AlloyDB when scale justifies cost)
- **Vertex AI Gemini** for LLM inference
- **Modular monolith on Cloud Run** for the application layer
- **No Pub/Sub in v1** — domain events as database rows
- **BigQuery deferred** — add when analytics projections are needed

## v1 deployment topology

```
Browser
  → HTTPS LB + Cloud Armor
    → Frontend (Cloud Run)
      → BFF / API (Cloud Run)
        → Domain service
        → Prompt service → Vertex AI
        → Query / Projection API
      → Cloud SQL PostgreSQL
```

## Consequences

- Database schema must be designed for entities, events, relations, knowledge, and prompt execution
- Domain tools layer ("tools over tables") becomes the primary API pattern
- The guided conversational transaction loop requires Vertex AI integration
- Infrastructure scripts in bkmng-infra need to be extended for Cloud SQL provisioning
