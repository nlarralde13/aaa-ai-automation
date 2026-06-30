# Decision: Select n8n for Workflow Orchestration

- Status: Accepted
- Date: 2026-06-30

## Context

The platform needs a self-hosted workflow engine that can receive webhooks, call external APIs, branch on business rules, support retries, and remain practical for a single operator.

## Decision

Use n8n as the initial workflow orchestrator for the development and demo platform.

## Alternatives Considered

- Node-RED
- Temporal
- Windmill
- Custom application code only

## Consequences

- Webhook-first workflows can be built quickly.
- Operators get a visual workflow execution history.
- n8n credential handling and workflow exports must be managed carefully.
- More complex long-running orchestration may require custom services later.
