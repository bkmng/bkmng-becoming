---
id: decision-007
becoming_type: Decision
label: Extend Becoming model with epistemic chain and knowledge layer
occurred_at: "2026-03-18"
status: active
made_by: actor-founding-team
rationale: >
  The system architecture conversation identified that the existing Becoming
  model (RAKR + Decision/Assumption/Observation) lacks explicit representation
  of interpretation, hypothesis formation, and learning. These are needed to
  represent how organizations move from evidence to understanding to action.
  Additionally, a curated knowledge layer is needed to ground AI interactions
  in validated theory and practice rather than generic LLM knowledge.
based_on:
  - assumption-d007-1
  - assumption-d007-2
commits_to:
  - activity-model-specification
  - activity-platform-development
eliminates: []
assumptions:
  - id: assumption-d007-1
    becoming_type: Assumption
    assumption_type: activity
    predicate: >
      Adding Interpretation, Hypothesis, and Learning as explicit types
      will make the Becoming model significantly more useful for representing
      organizational sensemaking and learning, without making the model
      unmanageably complex (projections handle complexity for users).
    confidence: medium
    formed_at: "2026-03-18"
    attached_to: activity-model-specification
  - id: assumption-d007-2
    becoming_type: Assumption
    assumption_type: activity
    predicate: >
      A curated knowledge layer with editorial pipeline will produce better
      AI-guided interactions than generic LLM knowledge or RAG over
      arbitrary documents.
    confidence: medium
    formed_at: "2026-03-18"
    attached_to: activity-platform-development
---

## Context

The Becoming model v0.1.0 includes seven concept types: Resource, Activity,
Actor, Result, Decision, Assumption, Observation. The system architecture
conversation identified gaps in the epistemic chain — how organizations move
from raw evidence to tested understanding.

## What changed

### Becoming schema (v0.2.0)

Three new concept types:

1. **Interpretation** (Event) — meaning-making over observations
2. **Hypothesis** (Expectation) — testable propositions, candidates for assumptions
3. **Learning** (Event) — records of how understanding changed

Six new relation types: `interprets`, `tests`, `promotes_to`, `updates`,
`triggered_by`, `revises`.

The epistemic chain is now explicit:
```
Observation → Interpretation → Hypothesis → Assumption → Decision → Activity → Observation → Learning
```

### Strategic hierarchy projection

A new conceptual projection mapping Becoming types to the strategy-to-action
chain: Strategic Intent → Theme → Goal → Hypothesis → Capability → Initiative
→ Activity → Observation → Learning.

### Knowledge layer

A curated professional content system with:
- knowledge_topic, knowledge_concept, knowledge_method, knowledge_heuristic,
  knowledge_pattern, knowledge_example
- Editorial pipeline: draft → in_review → published → deprecated
- Context assembly for AI prompt enrichment
- Principle: "editorial before retrieval"

### Design principles

Ten core design principles captured, including:
- "The user works in language. The system works in models."
- "Store understandings, not truths."
- "Complex core, simple projections."
- "Accounting gives economic control. BKMNG gives strategic control."

## Consequences

- The `becoming` TypeScript package moves to v0.2.0
- Downstream consumers (bkmng-app) need to handle the new types
- Database schema design must include tables for all new types plus the knowledge layer
- The AI interface design (guided conversational transaction loop) can now reference the full epistemic chain
