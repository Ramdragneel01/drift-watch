# drift-watch Architecture

## System Goals

- Detect data drift before model quality degrades
- Provide deterministic, explainable drift scores
- Keep runtime footprint small and deployment simple

## Logical Components

1. API Gateway Layer (FastAPI)
- Request validation and input size controls
- Health/readiness probes
- Drift evaluation orchestration

2. Drift Engine
- Numeric drift: PSI and KS statistic
- Categorical drift: Jensen-Shannon divergence
- Concept drift: target distribution drift and residual-shift checks

3. Dashboard (React)
- Request composition and submission
- Drift summary visualization
- Feature-level metric display and triage guidance

4. Deployment and Operations Layer
- Docker-based packaging
- CI and release automation via GitHub Actions
- Optional GitHub Pages publication of frontend build

## Request Flow

1. Client submits schema + reference/current payloads.
2. API validates fields, dimensions, and limits.
3. Drift engine computes per-feature metrics.
4. Alert decisions are evaluated per feature threshold.
5. Response returns summary + detailed metric payload.

## Security Controls

- Trusted host middleware
- CORS allowlist (default explicit hosts)
- Payload size limit middleware
- Optional HSTS header injection in production

## Reliability Controls

- `/health` for liveness
- `/ready` for readiness checks
- Deterministic scoring functions with bounded complexity

## Scalability Notes

- Stateless API instances scale horizontally
- Drift evaluation is O(n log n) for sorted numeric checks and O(n) for distribution counting
- Streaming ingestion can be integrated through a dedicated worker in a later milestone
