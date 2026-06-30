# AAA AI Automation

AAA AI Automation is a self-hosted AI workflow and automation platform. The first reference implementation is for 513 Property Services.

The platform will receive business events, enrich them with AI, route work through reliable workflows, record state, and produce clear customer-facing and operator-facing outcomes.

## Repository Layout

| Path | Purpose |
| --- | --- |
| `app/` | Application code and service-specific source files. |
| `config/` | Sanitized configuration examples. Real environment files stay out of Git. |
| `docs/` | Product, architecture, operations, and runbook documentation. |
| `docs/decisions/` | Architecture decision records. |
| `infra/` | Reproducible infrastructure and deployment configuration. |
| `scripts/` | Operator and developer scripts. |
| `tests/` | Automated tests and validation fixtures. |
| `workflows/` | Workflow definitions and sanitized workflow exports. |

## Current Documentation

- [Documentation Index](docs/README.md)
- [Project Charter](docs/project-charter.md)
- [Initial Architecture](docs/architecture.md)
- [Development Environment Setup](docs/development-setup.md)
- [Host Inventory](docs/host-inventory.md)
- [Repository Workflow](docs/repository-workflow.md)
- [Secrets and Configuration](docs/secrets-and-config.md)

## Git Workflow

- Use GitHub Issues as the task backlog.
- Work from a task-specific branch, for example `docs/issue-3-repository-workflow`.
- Keep each branch focused on the issue being addressed.
- Reference issue numbers in commits and pull requests.
- Do not commit credentials, private keys, API tokens, or real customer data.
- Review the final diff before committing.

## Definition of Done

A change is done when:

- The issue acceptance criteria are met.
- Documentation is updated for behavior, architecture, or operations changes.
- Relevant validation commands have been run.
- Secrets and customer data have been excluded from the diff.
- Remaining unknowns are explicitly documented as `Requires operator confirmation`.
- The pull request explains what changed, why, and how it was validated.
