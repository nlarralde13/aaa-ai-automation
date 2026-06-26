# Decision: Use GitHub as the Project System of Record

- Status: Accepted
- Date: 2026-06-26

## Context

The project needs a durable place for source code, documentation, actionable tasks, milestone tracking, and implementation history. Chat conversations alone are not sufficiently structured for filtering, audit, or automation.

## Decision

Use GitHub as the authoritative project system of record:

- GitHub Issues for actionable work
- GitHub Projects for status and roadmap views
- Pull requests for implementation and review
- Repository Markdown for product, architecture, runbooks, and decisions

Use the ChatGPT Project as the planning, reasoning, decomposition, and review layer.

## Alternatives Considered

- Jira
- Linear
- Notion
- A custom self-hosted project tracker

## Consequences

- Project work remains close to the code.
- The operating model stays lightweight for a single builder.
- GitHub permissions and repository hygiene become important.
- A separate business-document system may still be useful for customer-facing assets.
