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

## Docker Engine and Compose

Docker Engine and the Docker Compose plugin are installed on `wbm-cogs-01`.
The installed packages are sourced from Docker's official Ubuntu `noble`
repository at `https://download.docker.com/linux/ubuntu`.

Validated on 2026-06-30 UTC:

| Check | Command | Result |
| --- | --- | --- |
| Current user | `whoami` | `mediacontrol` |
| Docker group access | `id -nG` | User belongs to `docker` group |
| Docker Engine version | `docker --version` | Docker 29.5.2, build `79eb04c` |
| Docker Compose plugin version | `docker compose version` | Docker Compose v5.1.4 |
| Docker service starts at boot | `systemctl is-enabled docker` | `enabled` |
| Docker service running | `systemctl is-active docker` | `active` |
| Docker daemon access without `sudo` | `docker info` | Succeeded for user `mediacontrol` |
| Test container | `docker run --rm hello-world` | Succeeded; printed `Hello from Docker!` |

Relevant daemon details from `docker info`:

| Item | Value |
| --- | --- |
| Server version | 29.5.2 |
| Storage driver | `overlayfs` |
| Cgroup driver | `systemd` |
| Cgroup version | 2 |
| Operating system | Ubuntu 24.04.4 LTS |
| Architecture | `x86_64` |
| CPUs visible to Docker | 8 |

Currently running container observed during validation:

| Container | Image | Status | Ports |
| --- | --- | --- | --- |
| `513propertyservices-web` | `nginx:1.27-alpine` | Up 3 days, healthy | `0.0.0.0:80->80/tcp`, `[::]:80->80/tcp` |

The `hello-world:latest` image was pulled during validation. Reboot behavior for
application containers has not been tested locally. Requires operator
confirmation.

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
- [x] Docker and Compose are installed
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
