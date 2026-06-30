# Development, Demo, and Production Boundaries

## Purpose

AAA AI Automation starts on one development VM, but the project must keep clear boundaries between development, demonstration, and future customer production use.

## Environment Comparison

| Area | Development | Demo | Production |
| --- | --- | --- | --- |
| Purpose | Build and validate platform behavior. | Show repeatable 513 Property Services workflow. | Run real customer workflows. |
| Data | Synthetic or scrubbed test data. | Synthetic or explicitly approved demo data. | Real customer data only after controls are in place. |
| Credentials | Local development credentials. | Demo-scoped credentials. | Customer or production-scoped credentials. |
| URLs | LAN hostnames, localhost, or temporary tunnels. | Stable demo hostname with HTTPS. | Customer-approved hostname with HTTPS. |
| Deployment config | Local ignored env file. | Demo ignored env file or protected host file. | Managed secret store or protected host configuration. |
| Backup | Local runbook and NFS target candidate. | Documented backup before demos. | Tested backup and restore with retention policy. |
| Monitoring | Local logs and health checks. | Operator-visible failures. | Alerting, retention, and support expectations. |

## Data Separation

- Development and demo must not share credentials with production.
- Production customer data must not be copied into development.
- Demo data should be resettable and clearly labeled as demo data.
- Workflow exports must be sanitized before commit.

## Credential Separation

Each environment needs separate values for:

- Database credentials.
- Workflow encryption keys.
- AI provider credentials.
- Notification provider credentials.
- Webhook shared secrets.
- Backup credentials.

Production secret storage and access approval process: Requires operator confirmation.

## URL and Ingress Separation

Development may use LAN-only HTTP while services are being built. Demo and production endpoints must use HTTPS before receiving external webhooks.

Minimum external endpoint controls:

- TLS certificate.
- Payload authentication or signed webhook verification.
- Request size limits.
- Logging with correlation IDs.
- Rate limiting or upstream protection where practical.

Public DNS and certificate owner: Requires operator confirmation.

## Minimum Controls Before Real Customer Data

Real customer data must not be used until these controls are complete:

- Environment-specific credentials are separated.
- Secrets are excluded from Git and backed up securely.
- HTTPS ingress is configured.
- Workflow failures are visible and retryable.
- Database backups and restore testing are documented.
- Data retention expectations are defined.
- Operator access is limited to approved users.
- AI provider data-use terms are reviewed for the customer use case.

AI provider contractual terms and customer data handling approval: Requires operator confirmation.
