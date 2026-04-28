# Future Clarification Notes

These are intentional comment-style notes for future contributors and reviewers.

## Architecture Notes

1. We intentionally kept the backend stateless in v0.1.0 to simplify horizontal scaling.
2. Drift score fusion uses weighted PSI+KS for numeric features to balance stability and sensitivity.
3. Categorical drift uses Jensen-Shannon divergence because it is symmetric and bounded.

## Planned Upgrades

1. Add Kafka/Kinesis connector worker for streaming window ingestion.
2. Add webhook integrations (Slack, Teams, PagerDuty) for alert routing.
3. Add persisted drift history and trend visualizations.
4. Add tenant-aware auth and API keys for multi-team usage.

## Why These Notes Exist

- To reduce rework and clarify non-obvious trade-offs.
- To speed up onboarding for external contributors and recruiters reviewing the codebase.
- To preserve design intent when implementation expands.
