# Decision: Use NFS Storage as the Initial Backup Target Candidate

- Status: Proposed
- Date: 2026-06-30

## Context

The development VM has `/mnt/storage` mounted from `192.168.1.150:/mnt/wbm-storage-01/storage` over NFS. The mount is writable and has substantial free space.

## Decision

Use `/mnt/storage/aaa-ai-automation/` as the initial backup target candidate for development backups.

## Alternatives Considered

- Local-only backups on the VM disk
- Object storage
- Hypervisor snapshots only
- Dedicated backup appliance

## Consequences

- The development backup path can be tested with local commands.
- NFS availability becomes part of restore readiness.
- Snapshot, retention, encryption, and offsite replication details require operator confirmation before this is accepted for production.
