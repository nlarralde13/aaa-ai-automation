# Project Operating Model

## Systems of Record

- **GitHub Issues:** tasks, defects, and actionable work
- **GitHub Projects:** backlog status and milestone views
- **Repository documentation:** product, architecture, runbooks, and decisions
- **Pull requests:** implementation history and review
- **ChatGPT Project:** planning, decomposition, review, and working context

## Workflow States

1. Inbox
2. Backlog
3. Ready
4. In Progress
5. Blocked
6. Review / Test
7. Done

## Issue Requirements

Every implementation issue should include:

- Problem or desired outcome
- Scope
- Acceptance criteria
- Dependencies
- Testing notes
- Documentation impact

## Branch Convention

```text
feature/<short-name>
fix/<short-name>
docs/<short-name>
chore/<short-name>
```

## Pull Request Expectations

- Keep changes focused.
- Link the relevant issue.
- Explain what changed and why.
- Include validation steps.
- Update documentation when behavior changes.
- Prefer squash merges for small, focused work.

## Review Cadence

### Build Review

At least once per active work week:

- Review completed work.
- Identify blockers.
- Reorder the Ready queue.
- Confirm the next demonstrable outcome.

### Milestone Review

At each milestone boundary:

- Verify exit criteria.
- Record unresolved risks.
- Update the roadmap.
- Capture any architecture decisions.
- Decide whether to advance or extend the milestone.

## Definition of Done

A task is done when:

- Acceptance criteria are met.
- The change has been tested.
- Failure behavior is understood.
- Required documentation is updated.
- Secrets or customer data are not exposed.
- The change is merged into the main branch.
