# Initial Architecture

## Overview

The initial platform will run on `wbm-cogs-01` and use containerized services. The design should remain simple enough for a single operator while preserving clear boundaries between ingress, orchestration, AI services, business data, and observability.

## Logical Flow

```text
Website / External Event
          |
          v
 Reverse Proxy / Webhook Ingress
          |
          v
 Workflow Orchestrator
     |       |       |
     |       |       +--> Notifications / Email
     |       +----------> LLM Provider
     +------------------> PostgreSQL / State
          |
          v
 Logs, Metrics, Alerts
```

## Proposed Components

### Host

- Ubuntu Server VM: `wbm-cogs-01`
- Docker Engine
- Docker Compose

### Core Services

- **Workflow orchestration:** n8n, subject to final decision
- **Database:** PostgreSQL
- **Ingress:** Caddy or another existing reverse-proxy standard
- **AI provider:** configurable external API initially; local models may be evaluated later
- **Observability:** container logs plus a lightweight health and alerting layer

## Architecture Boundaries

### Ingress

Responsible for TLS termination, request size limits, authentication where required, and routing traffic to workflow endpoints.

### Workflow Layer

Responsible for validation, orchestration, branching, retries, and human approval points. Business rules should be explicit and version-controlled where practical.

### AI Layer

Responsible for classification, summarization, drafting, or extraction. AI output must be validated before it changes durable business state or triggers high-impact actions.

### Data Layer

Responsible for leads, workflow state, audit history, configuration references, and operational metadata. Secrets must not be stored in source control or ordinary workflow payloads.

### Notification Layer

Responsible for customer acknowledgements and operator alerts. Notification failure must not silently erase the underlying lead or event.

### Observability Layer

Responsible for logs, workflow status, health checks, retry visibility, and alerting.

## Environment Strategy

Initial development may run on a single VM, but configurations should distinguish:

- Development
- Demo or staging
- Production customer deployments

Environment-specific values belong in secret stores or environment files excluded from Git.

## Security Baseline

- Use least-privilege credentials.
- Keep API keys out of repositories and workflow exports.
- Require TLS for externally reachable endpoints.
- Validate all inbound payloads.
- Record important state transitions.
- Avoid sending unnecessary customer data to AI providers.
- Define data retention before handling real customer information.

## Open Decisions

- Final workflow engine
- Reverse-proxy approach
- Initial LLM provider
- Notification provider
- Lead storage schema
- Monitoring stack
- Backup target and retention

Each material decision should be captured under `docs/decisions/`.
