# Secrets and Configuration Standard

## Scope

This standard covers local development, demonstration, and future production configuration for AAA AI Automation.

## Rules

- Real secrets must never be committed.
- Commit sanitized examples only, such as `config/.env.example`.
- Local environment files must remain untracked.
- Workflow exports must be sanitized before they are committed.
- Credentials should be scoped to the least privilege needed by each service.
- Rotate credentials after accidental exposure or when an operator leaves the project.

## Git Ignore Coverage

The root `.gitignore` excludes common local secret and runtime files:

- `.env` and `.env.*`
- key and certificate file patterns such as `*.key`, `*.pem`, and `*.p12`
- `secrets/`, `private/`, `data/`, `backups/`, `logs/`, and generated workflow exports

The repository intentionally allows sanitized example files such as `.env.example` and `*.env.example`.

## Environment File Pattern

Use `config/.env.example` as the committed template. Operators should create local environment files from that template and store real values outside version control.

Recommended local paths:

| Environment | Suggested file | Git status |
| --- | --- | --- |
| Development | `.env.development` | Ignored |
| Demo | `.env.demo` | Ignored |
| Production | Managed secret store or protected host file | Ignored |

Production secret storage is not finalized. Requires operator confirmation.

## Rotation Standard

Rotate a credential when:

- It is suspected or confirmed to be exposed.
- A vendor API key is replaced.
- A team member or operator with access leaves the project.
- A demo environment is promoted to a customer-facing deployment.

Minimum rotation steps:

1. Create the replacement credential.
2. Update the protected runtime configuration.
3. Restart or reload only the affected services.
4. Verify the affected workflow succeeds.
5. Revoke the old credential.
6. Record the rotation date in the private operator log, not in this repository.

## Validation

Before committing configuration changes:

```bash
git status --short
git diff --check
git diff --cached --check
git grep -nE 'AKIA|BEGIN (RSA|OPENSSH|PRIVATE) KEY|sk-[A-Za-z0-9]|xox[baprs]-|ghp_' -- .
```

The pattern check is a baseline only. It does not prove that the repository contains no secrets. Requires operator confirmation before using real customer data.
