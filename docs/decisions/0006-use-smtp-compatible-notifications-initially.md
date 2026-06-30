# Decision: Use SMTP-Compatible Notifications Initially

- Status: Accepted
- Date: 2026-06-30

## Context

The reference workflow needs customer acknowledgements and operator notifications without introducing a large messaging stack.

## Decision

Use SMTP-compatible email notifications for the initial implementation. Keep provider-specific values in environment configuration.

## Alternatives Considered

- Twilio SMS first
- Slack or Teams only
- Provider-specific email API first
- Manual notification during the demo

## Consequences

- Email covers both customer and operator notification paths for the first demo.
- SMS or chat notifications can be added later as separate integrations.
- Delivery failures must be visible in workflow execution history and operator alerts.
