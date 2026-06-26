# Development Environment Setup

## Target Host

- Hostname: `wbm-cogs-01`
- Purpose: development and demonstration environment for AAA AI Automation

## Host Inventory to Record

- Operating system and version
- CPU and memory allocation
- Root and data disk capacity
- Static IP or DHCP reservation
- DNS record
- Backup method
- Administrative users

## Recommended Repository Location

`/home/mediacontrol/aaa-ai-automation`

Adjust the account or path if the VM uses a different administrative user.

## Environment Files

Runtime secrets and host-specific values should use local environment files or a protected secrets directory. These must be excluded from Git. Only sanitized examples such as `.env.example` should be committed.

## Planned Local Services

- Workflow orchestrator
- PostgreSQL
- Reverse proxy
- Optional database administration UI
- Logging and health checks

## Validation Checklist

- [ ] Host resolves by name
- [ ] SSH access is working
- [ ] System packages are current
- [ ] Repository is cloned
- [ ] Docker and Compose are installed
- [ ] Secrets are stored outside Git
- [ ] Containers start after reboot
- [ ] Backup target is configured
- [ ] Health checks are visible

## Recovery Expectations

The environment should be recoverable using:

1. A clean Ubuntu VM
2. This repository
3. A protected secrets backup
4. A database backup
5. The documented deployment procedure
