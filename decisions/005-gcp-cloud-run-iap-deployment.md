---
id: decision-005
becoming_type: Decision
label: Deploy private demo on GCP Cloud Run with IAP authentication
occurred_at: "2026-03-10"
status: active
made_by: actor-founding-team
rationale: >
  IAP (Identity-Aware Proxy) provides Google-account-based access control
  without building authentication into the application. Cloud Run handles
  containerised static serving at low cost. GCP was already the chosen
  cloud platform and fits the expected trajectory toward server-side features.
based_on:
  - assumption-d005-1
  - assumption-d005-2
  - assumption-d005-3
commits_to:
  - activity-demo-construction
  - activity-nhh-engagement
eliminates: []
assumptions:
  - id: assumption-d005-1
    becoming_type: Assumption
    assumption_type: resource
    predicate: >
      GCP Cloud Run + IAP is operationally manageable for a small team
      without dedicated DevOps — infra-as-code scripts suffice.
    confidence: high
    formed_at: "2026-03-10"
    attached_to: activity-demo-construction
  - id: assumption-d005-2
    becoming_type: Assumption
    assumption_type: actor
    predicate: >
      NHH collaborators and pilot participants will have Google accounts
      and can be granted IAP access without friction.
    confidence: medium
    formed_at: "2026-03-10"
    attached_to: actor-nhh-faculty
  - id: assumption-d005-3
    becoming_type: Assumption
    assumption_type: activity
    predicate: >
      A static site served via Cloud Run is sufficient for the demo at this stage —
      no server-side rendering or database connectivity is needed yet.
    confidence: high
    formed_at: "2026-03-10"
    attached_to: activity-demo-construction
---

## Context

The private demo needs to be hosted somewhere that is not publicly accessible
but is shareable with specific collaborators. Options were Firebase Hosting
with auth, Vercel with password protection (Pro plan), and GCP Cloud Run + IAP.

## Options considered

1. Vercel Pro — password protection, simple but no per-user access control
2. Firebase Hosting + Firebase Auth — more app complexity
3. GCP Cloud Run + IAP — infrastructure complexity, but per-user access control and aligns with GCP strategy

## Decision

GCP Cloud Run with:
- HTTPS load balancer at `app.bkmng.com`
- Google-managed SSL certificate
- IAP on the backend service — access granted per Google account
- CI/CD via Cloud Build triggered on push to `bkmng/bkmng-app:main`

## Infrastructure

All setup scripted in `bkmng-infra/gcp/`:
- `setup.sh` — APIs, Artifact Registry, IAM
- `iap.sh` — load balancer, SSL cert, IAP, service account provisioning
