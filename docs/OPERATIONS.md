# Operations Runbook

## Health and Readiness

- Liveness: `GET /health`
- Readiness: `GET /ready`

## Recommended Alerts

1. API health endpoint non-200 for 2+ minutes
2. Readiness endpoint non-ready status
3. High drift ratio (drifted_features / total_features >= 0.4) sustained for N runs
4. Request failure rate > 2% over 5 minutes

## Incident Response Playbook

1. Confirm if issue is API availability, data quality, or model behavior.
2. Check current drift reports and identify top shifted features.
3. Verify upstream data pipeline changes in the drift window.
4. If concept drift is confirmed, trigger model rollback or retraining path.
5. Document root cause and add a regression check.

## Capacity and Performance Notes

- Drift calculations are memory-local and CPU-bound.
- For large windows, split requests by feature groups.
- Horizontal API scaling is safe because backend is stateless.

## Backup and Recovery

- This version stores no server-side state.
- Persist drift reports externally if historical trend audits are required.
