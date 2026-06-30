# Backup and Recovery Runbook

## Scope

This runbook covers the development VM and the future local demo stack for AAA AI Automation.

## Data Requiring Backup

| Data | Backup requirement |
| --- | --- |
| Git repository | Source of record is GitHub; local branches must be pushed or exported before VM rebuild. |
| Environment files | Back up protected host copies outside Git. |
| Workflow definitions | Commit sanitized exports; back up live workflow state once the orchestrator exists. |
| PostgreSQL data | Back up with `pg_dump` or service-specific dump job once PostgreSQL exists. |
| Reverse proxy config | Keep reproducible config under `infra/`; back up any host-only overrides. |
| Operator notes | Keep non-secret operational notes in docs; private notes require protected backup. |

## Current Backup Indicators

Local inventory found:

- `/mnt/storage` mounted from `192.168.1.150:/mnt/wbm-storage-01/storage` over NFS.
- `/mnt/storage` is writable from the current VM.
- Standard package metadata backups exist under `/var/backups`.
- `dpkg-db-backup.timer` is present.
- Backup-named directories exist on `/mnt/storage`.

Whether `/mnt/storage` is the official backup target and whether it has its own redundancy, snapshots, offsite replication, and retention policy: Requires operator confirmation.

## Recommended Backup Target

Use a project-specific directory on the mounted NFS storage:

```text
/mnt/storage/aaa-ai-automation/
```

Suggested layout:

```text
/mnt/storage/aaa-ai-automation/
  env/
  postgres/
  workflows/
  restore-tests/
```

Do not store unencrypted production secrets on shared storage. Production backup encryption and key custody: Requires operator confirmation.

## Retention Expectations

Recommended development baseline:

| Backup type | Retention |
| --- | --- |
| Environment file backup | Keep the latest known-good copy and one previous copy. |
| PostgreSQL dumps | Keep 7 daily dumps and 4 weekly dumps once PostgreSQL exists. |
| Workflow exports | Keep one export per released demo version. |
| Restore-test artifacts | Keep only the latest successful restore-test notes; remove temporary extracted data. |

Final retention, encryption, offsite copy, and deletion policy: Requires operator confirmation.

## Development Backup Procedure

1. Confirm the NFS target is mounted:

   ```bash
   findmnt /mnt/storage
   ```

2. Confirm the repository state is clean or intentionally documented:

   ```bash
   git status --short --branch
   ```

3. Push committed work or create an operator-approved export of unpushed work.

4. Back up protected environment files from their host location to the approved target.

5. When PostgreSQL is added, create a dump:

   ```bash
   pg_dump --format=custom --file=/backup/path/aaa-ai-automation.dump "$DATABASE_URL"
   ```

6. Record the backup date, scope, and restore test status in the private operator log.

## Restore Procedure

1. Provision a clean Ubuntu VM.
2. Install Docker Engine and Docker Compose.
3. Clone this repository.
4. Restore protected environment files from the approved backup target.
5. Restore workflow engine state and PostgreSQL data when those services exist.
6. Start the Compose stack.
7. Validate service health checks.
8. Run the demo workflow smoke test.

## Restore Validation

Validated locally on 2026-06-30 UTC:

- `/mnt/storage` is mounted and writable.
- A documentation-only archive restore can be tested without exposing secrets by archiving tracked docs to `/tmp`, extracting them into a temporary restore directory, and comparing the restored file list.

Commands used for the documentation-only restore validation:

```bash
tmpdir="$(mktemp -d)"
git ls-files docs > "$tmpdir/docs-files.txt"
tar -czf "$tmpdir/docs.tgz" -T "$tmpdir/docs-files.txt"
mkdir "$tmpdir/restore"
tar -xzf "$tmpdir/docs.tgz" -C "$tmpdir/restore"
(cd "$tmpdir/restore" && find docs -type f | sort) > "$tmpdir/restored-files.txt"
diff -u <(sort "$tmpdir/docs-files.txt") "$tmpdir/restored-files.txt"
rm -rf "$tmpdir"
```

Full application restore cannot be validated until the orchestrator, database, and backup jobs exist. Requires operator confirmation.
