# Product Roadmap

## Product Goal

Deliver a reusable AI automation platform with a polished 513 Property Services reference implementation that can be demonstrated to prospective customers and adapted into paid engagements.

## Milestone 0 — Development Foundation

**Outcome:** `wbm-cogs-01` is a repeatable and documented development environment.

### Objectives

- Confirm VM sizing, storage, networking, DNS, and backup approach.
- Install Docker Engine and Docker Compose.
- Establish repository workflow and branch conventions.
- Define secrets handling and local environment configuration.
- Add baseline logging, health checks, and backup procedures.
- Document development and future production separation.

### Exit Criteria

- Repository can be cloned and initialized from documentation.
- Core containers start consistently after reboot.
- Secrets are excluded from Git.
- Basic health and backup checks are documented.

## Milestone 1 — Automation Platform Foundation

**Outcome:** A minimal but reliable workflow platform is running.

### Objectives

- Deploy n8n or the selected workflow engine.
- Deploy PostgreSQL for durable state.
- Configure webhook ingress.
- Configure one LLM provider through a replaceable abstraction.
- Add structured logs and workflow error handling.
- Build a simple end-to-end test workflow.

### Exit Criteria

- A test webhook triggers a workflow.
- The workflow calls an LLM and stores a result.
- Failures are visible and retryable.
- Setup and recovery steps are documented.

## Milestone 2 — 513 Property Services Lead Workflow

**Outcome:** A real lead can flow from website submission through classification and follow-up.

### Objectives

- Define the website lead payload.
- Validate and normalize submissions.
- Classify service type, urgency, and intent.
- Generate an operator summary.
- Send customer acknowledgement.
- Send owner notification.
- Store lead status and workflow history.
- Add manual review and override points.

### Exit Criteria

- A production-like form submission completes successfully.
- Duplicate or malformed submissions are handled safely.
- Lead history is reviewable.
- The workflow can be demonstrated repeatedly.

## Milestone 3 — Demonstrable Product

**Outcome:** The platform can be shown to a prospective customer without developer intervention.

### Objectives

- Create resettable demo data.
- Add a concise demo script.
- Add operational dashboards or status views.
- Document the architecture and workflow lifecycle.
- Record a demonstration video.
- Prepare before-and-after business value messaging.

### Exit Criteria

- Demo can be run from a known starting state.
- Common failure scenarios are covered.
- Screenshots, diagrams, and demo instructions are current.
- The value proposition is understandable to a non-technical customer.

## Milestone 4 — Pilot Ready

**Outcome:** The solution can be deployed for a first external pilot with controlled risk.

### Objectives

- Define customer onboarding and discovery checklists.
- Establish credential and secret handling.
- Define tenant separation strategy.
- Add backup, restore, and rollback procedures.
- Define support boundaries and service levels.
- Draft pricing and implementation packages.

### Exit Criteria

- A customer deployment can be scoped and repeated.
- Customer data boundaries are documented.
- Rollback and support procedures are tested.
- Commercial assumptions are documented.

## Later Roadmap

- Additional lead sources and channels
- CRM integrations
- Scheduling automation
- Quote drafting
- Customer follow-up sequences
- Internal knowledge retrieval
- Multi-customer deployment tooling
- Usage reporting and billing support
