# AAA AI Automation — Project Charter

## Purpose

Build a reusable, self-hosted AI automation platform that can be demonstrated, operated, and adapted for small-business customers. The first reference implementation will use 513 Property Services as the internal customer and proof of concept.

## Primary Objective

Create a working automation system that receives business events, enriches them with AI, routes work through reliable workflows, records state, and produces clear customer-facing and operator-facing outcomes.

## Initial Reference Use Case

A prospective customer submits a request through the 513 Property Services website. The platform should:

1. Receive and validate the lead.
2. Classify the request by service type, urgency, and likely next action.
3. Send an acknowledgement to the customer.
4. Notify the business owner with a concise summary.
5. Create or update a lead record.
6. Track follow-up status and failures.

## Project Principles

- Prefer open-source and self-hosted components where practical.
- Use trial or low-cost services only where they materially accelerate delivery.
- Build one complete workflow before expanding scope.
- Keep customer data, secrets, and operational state separated.
- Make every workflow observable, testable, and recoverable.
- Treat 513 Property Services as a real customer implementation, not a throwaway demo.

## Success Criteria

The first demonstrable release is successful when:

- A real website form can trigger the workflow.
- The system produces a useful AI-generated classification and summary.
- Customer and operator notifications are delivered reliably.
- Workflow state is stored and reviewable.
- Failures are logged and can be retried.
- The demo can be reset and repeated predictably.
- A new customer implementation can be estimated from the reference architecture.

## Current Environment

- Development VM: `wbm-cogs-01`
- Repository: `nlarralde13/aaa-ai-automation`
- Reference customer: 513 Property Services
- Initial operating model: single builder, self-hosted development environment

## Out of Scope for the First Demo

- Full multi-tenant SaaS architecture
- Autonomous financial or legal decisions
- Complex CRM replacement
- Large-scale model training
- Mobile application development
- Production-grade billing

## Governance

- GitHub Issues are the authoritative task backlog.
- Pull requests are the preferred path for changes after repository initialization.
- Architecture decisions are recorded under `docs/decisions/`.
- Milestone status is maintained in `docs/product-roadmap.md` and GitHub Projects.
