# Repository Workflow

## Purpose

This repository is the source of record for the AAA AI Automation platform code, infrastructure, workflows, and operating documentation.

## Initial Layout

| Path | Contents |
| --- | --- |
| `app/` | Application source code for custom services, adapters, or internal tooling. |
| `config/` | Sanitized example configuration files only. |
| `docs/` | Project, architecture, operations, and runbook documentation. |
| `docs/decisions/` | Architecture decision records for material choices. |
| `infra/` | Docker Compose, reverse proxy, deployment, and host setup configuration. |
| `scripts/` | Repeatable setup, validation, backup, restore, and operator scripts. |
| `tests/` | Automated tests, validation fixtures, and smoke checks. |
| `workflows/` | Sanitized workflow definitions and workflow test fixtures. |

## Branch Naming

Use short, issue-focused branch names:

```text
docs/issue-3-repository-workflow
feature/issue-12-lead-webhook
fix/issue-18-notification-retry
chore/issue-22-dependency-update
```

## Pull Request Expectations

Each pull request should include:

- The issue number it resolves or advances.
- A concise summary of the change.
- Validation commands and results.
- Documentation updates when behavior, architecture, or operations change.
- Any remaining unknowns marked as `Requires operator confirmation`.

Pull requests should avoid unrelated cleanup. If a change reveals follow-up work, open or update a separate issue.

## Definition of Done

A task is done when:

- Acceptance criteria are met.
- The change has been tested or the validation gap is documented.
- Failure behavior is understood.
- Required documentation is updated.
- Secrets, tokens, private keys, and real customer data are not exposed.
- The final diff has been reviewed.
- The issue has a completion comment before it is closed.

## Local Validation Baseline

Before committing, run the relevant subset:

```bash
git status --short --branch
git diff --check
git diff --cached --check
```

For documentation-only changes, also confirm Markdown links point to existing files and that the rendered structure is readable.
