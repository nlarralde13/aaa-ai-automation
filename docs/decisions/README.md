# Architecture Decision Records

Use this directory for material technical and product decisions.

## Naming

Use `NNNN-short-decision-title.md`.

Example: `0001-select-workflow-orchestrator.md`

## Template

```markdown
# Decision: Title

- Status: Proposed | Accepted | Superseded
- Date: YYYY-MM-DD

## Context

What problem or decision is being addressed?

## Decision

What was selected?

## Alternatives Considered

What other options were evaluated?

## Consequences

What becomes easier, harder, or constrained because of this decision?
```

## Records

- [0001: Use GitHub as the Project System of Record](0001-project-system-of-record.md)
- [0002: Select n8n for Workflow Orchestration](0002-select-n8n-for-workflow-orchestration.md)
- [0003: Select PostgreSQL for Durable State](0003-select-postgresql-for-durable-state.md)
- [0004: Select Caddy for Reverse Proxy and HTTPS Ingress](0004-select-caddy-for-reverse-proxy.md)
- [0005: Use a Configurable External AI Provider Interface](0005-use-configurable-external-ai-provider-interface.md)
- [0006: Use SMTP-Compatible Notifications Initially](0006-use-smtp-compatible-notifications-initially.md)
- [0007: Use Docker Health Checks and Logs for Baseline Monitoring](0007-use-docker-health-checks-and-logs-for-baseline-monitoring.md)
- [0008: Use NFS Storage as the Initial Backup Target Candidate](0008-use-nfs-storage-as-initial-backup-target-candidate.md)
