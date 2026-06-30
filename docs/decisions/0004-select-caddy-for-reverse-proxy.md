# Decision: Select Caddy for Reverse Proxy and HTTPS Ingress

- Status: Accepted
- Date: 2026-06-30

## Context

The platform needs a simple reverse proxy for webhook ingress, service routing, and future HTTPS termination.

## Decision

Use Caddy as the initial reverse proxy.

## Alternatives Considered

- Nginx
- Traefik
- Cloudflare Tunnel as primary ingress
- Direct container port publishing

## Consequences

- Caddy keeps local configuration small and supports automatic HTTPS for public hostnames.
- Direct service exposure should be avoided once the platform Compose stack is introduced.
- Public DNS and certificate ownership still require operator confirmation.
