# Decision: Use Docker Health Checks and Logs for Baseline Monitoring

- Status: Accepted
- Date: 2026-06-30

## Context

The development stack needs basic observability before a full monitoring system exists.

## Decision

Use Docker Compose health checks, container status, workflow execution history, and rotated Docker logs as the initial monitoring baseline.

## Alternatives Considered

- Prometheus and Grafana immediately
- Hosted monitoring service
- System logs only

## Consequences

- Operators can validate the stack with standard Docker commands.
- Compose services must include health checks as they are added.
- Production monitoring, alerting, and log retention require a later decision.
