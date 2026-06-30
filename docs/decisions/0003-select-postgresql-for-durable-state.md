# Decision: Select PostgreSQL for Durable State

- Status: Accepted
- Date: 2026-06-30

## Context

The platform needs durable state for leads, workflow metadata, audit history, and operational records.

## Decision

Use PostgreSQL as the initial durable database.

## Alternatives Considered

- SQLite
- MySQL or MariaDB
- Workflow-engine internal storage only
- Hosted database service

## Consequences

- PostgreSQL provides a reliable baseline for structured data and backups.
- The database can support both workflow engine state and custom application state.
- Backup and restore procedures must include database dumps.
- Schema ownership must be defined as application code is added.
