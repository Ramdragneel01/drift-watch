# API Reference

Base URL (local): `http://localhost:8000`

## GET /health

Liveness probe.

Response:

```json
{ "status": "ok" }
```

## GET /ready

Readiness probe.

Response:

```json
{ "status": "ready" }
```

## POST /api/v1/drift/evaluate

Evaluate feature drift from reference and current windows.

Request body:

```json
{
  "schema_name": "credit-risk-model-v1",
  "features": [
    { "name": "income", "kind": "numeric", "bins": 10, "alert_threshold": 0.15 },
    { "name": "region", "kind": "categorical", "alert_threshold": 0.12 }
  ],
  "reference_rows": [{ "income": 72000, "region": "east" }],
  "current_rows": [{ "income": 59000, "region": "south" }]
}
```

Response body:

```json
{
  "summary": {
    "schema_name": "credit-risk-model-v1",
    "evaluated_at": "2026-04-28T12:00:00Z",
    "total_features": 2,
    "drifted_features": 1,
    "status": "alert"
  },
  "results": [
    {
      "feature_name": "income",
      "kind": "numeric",
      "method": "psi+ks",
      "drift_score": 0.31,
      "threshold": 0.15,
      "drift_detected": true,
      "details": { "psi": 0.29, "ks": 0.35, "reference_count": 5000, "current_count": 5000 }
    }
  ]
}
```

## POST /api/v1/drift/concept

Evaluate concept drift on target and optional residual shift.

Request body:

```json
{
  "reference_target": [0.1, 0.2, 0.3],
  "current_target": [0.4, 0.5, 0.6],
  "reference_prediction": [0.15, 0.25, 0.35],
  "current_prediction": [0.45, 0.55, 0.65],
  "alert_threshold": 0.2
}
```

Response body:

```json
{
  "evaluated_at": "2026-04-28T12:00:00Z",
  "status": "stable",
  "results": [
    {
      "metric_name": "target_distribution_shift",
      "method": "psi+ks",
      "drift_score": 0.09,
      "threshold": 0.2,
      "drift_detected": false,
      "details": { "psi": 0.03, "ks": 0.11 }
    }
  ]
}
```
