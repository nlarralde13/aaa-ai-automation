# Networking, DNS, and Ingress

Collected from `wbm-cogs-01` on 2026-06-30 UTC.

## Current VM Network

| Item | Value |
| --- | --- |
| Primary interface | `ens18` |
| Hostname | `wbm-cogs-01` |
| VM address | `192.168.1.23/24` |
| Default gateway | `192.168.1.1` |
| DNS resolver | `systemd-resolved` stub at `127.0.0.53` |
| Upstream DNS | `192.168.1.5`, `1.1.1.1` |
| Active NFS mount | `192.168.1.150:/mnt/wbm-storage-01/storage` at `/mnt/storage` |

Static reservation, internal DNS record for `wbm-cogs-01`, and upstream firewall ownership: Requires operator confirmation.

## Observed Listening Ports

| Port | Protocol | Observed service | Expected exposure |
| --- | --- | --- | --- |
| `22` | TCP | OpenSSH | Internal administration only |
| `80` | TCP | Docker-published web container | Internal demo HTTP until HTTPS ingress is configured |
| `111` | TCP/UDP | `rpcbind` | Host/NFS support; restrict to trusted LAN |
| `3128` | TCP | Squid proxy | Internal only |
| `53` | TCP/UDP on loopback | `systemd-resolved` | Local host only |

Dynamic NFS/RPC ports were also present because `/mnt/storage` is mounted over NFSv3.

## Ingress Approach

Initial local ingress should use a single reverse proxy in front of application services.

Recommended baseline:

- Use Caddy as the initial reverse proxy.
- Terminate HTTPS at the reverse proxy for externally reachable endpoints.
- Route `/webhook/*` or a service-specific hostname to the workflow orchestrator.
- Keep administrative UIs internal or behind explicit authentication.
- Do not expose databases or internal service ports directly.

The currently observed HTTP listener is an Nginx demo container on port `80`. Future platform ingress should replace ad hoc published application ports with a documented reverse-proxy configuration.

## Required Ports

| Use | Port | Direction | Notes |
| --- | --- | --- | --- |
| SSH administration | `22/tcp` | Inbound from trusted admin networks | Required for VM operation. |
| HTTP redirect or internal demo | `80/tcp` | Inbound as approved | Should redirect to HTTPS when external. |
| HTTPS webhooks and UI | `443/tcp` | Inbound as approved | Required before real customer webhooks. |
| Outbound package and API access | `443/tcp` | Outbound | Required for package repositories and AI/provider APIs. |
| NFS storage | NFSv3 RPC ports | Internal LAN | Used for `/mnt/storage`; firewall policy requires operator confirmation. |

## Webhook Strategy

Development:

- Prefer LAN-only webhook testing.
- Use temporary tunnels only for short-lived tests.
- Do not put real customer data through temporary tunnels.

Demo:

- Use HTTPS with a stable demo hostname.
- Route inbound website events through the reverse proxy.
- Validate payload shape and authentication before invoking workflows.

Production:

- Use customer-specific hostnames or paths.
- Require TLS, payload authentication, request size limits, logging, and alerting.
- Keep production credentials and data separate from development and demo.

Public DNS names and certificate ownership: Requires operator confirmation.
