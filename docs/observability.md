# Logging and Health Check Baseline

## Goals

The development stack must make service failures, workflow failures, and unavailable dependencies visible without requiring deep container inspection.

## Minimum Container Health Checks

Every long-running service should define a health check in Docker Compose once the service is added under `infra/`.

Baseline expectations:

| Service type | Health signal |
| --- | --- |
| Reverse proxy | HTTP request to a local health endpoint or configuration test. |
| Workflow orchestrator | HTTP request to the orchestrator health endpoint. |
| PostgreSQL | `pg_isready` against the local database. |
| Custom application service | HTTP health endpoint or command that verifies required dependencies. |

Compose services should use `restart: unless-stopped` unless a service has a documented reason to exit.

## Service Status Visibility

Operators should be able to answer three questions quickly:

- Are containers running?
- Are containers healthy?
- Which workflow or dependency failed?

Baseline commands:

```bash
docker ps
docker compose ps
docker compose logs --tail=200
systemctl is-active docker
```

## Log Retention

Use Docker log rotation for local development and demo deployments.

Recommended default for Compose services:

```yaml
logging:
  driver: json-file
  options:
    max-size: "10m"
    max-file: "5"
```

Production log retention, centralization, and customer access policy: Requires operator confirmation.

## Workflow Failure Visibility

Workflow failures must not disappear into container logs only.

Minimum requirements for workflow implementations:

- Record failed workflow executions in the orchestrator.
- Include a correlation ID or lead ID in logs and notifications.
- Notify the operator when customer-facing acknowledgements, owner notifications, AI calls, or database writes fail.
- Make failed workflow executions retryable when the operation is safe to retry.
- Do not delete the original inbound payload until durable state is written.

## Dependency Availability

The stack should expose clear failure indicators for:

- Workflow orchestrator unavailable.
- PostgreSQL unavailable.
- AI provider timeout or authentication failure.
- Notification provider failure.
- Reverse proxy cannot reach upstream service.
- Backup target unavailable.

## Current Local Observations

Validated on 2026-06-30 UTC:

- Docker service is `active`.
- Docker is configured to start at boot.
- The `513propertyservices-web` container is running and reports healthy.
- No full platform Compose stack exists yet.

Future Compose files should include health checks before being considered complete.
