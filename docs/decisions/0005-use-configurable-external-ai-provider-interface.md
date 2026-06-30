# Decision: Use a Configurable External AI Provider Interface

- Status: Accepted
- Date: 2026-06-30

## Context

The initial workflow needs AI classification, summarization, and drafting, but the project should not be locked to one provider or require local model hosting before the first demo.

## Decision

Use a configurable external AI provider interface for the initial platform. Provider credentials and model names belong in environment-specific configuration, not source control.

## Alternatives Considered

- Hard-code one AI provider.
- Run local models only.
- Defer AI integration until after workflow plumbing.

## Consequences

- The first demo can use a managed provider quickly.
- Provider changes should be isolated to configuration and adapter logic.
- Customer-data handling depends on the selected provider's terms and must be reviewed before production use.
