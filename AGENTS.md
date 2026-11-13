# Instructions for coding agents

You are contributing to SOVRAN, a long-lived personal AI operating system.

## Non-negotiable principles

1. Read the relevant documents in `docs/` before proposing or implementing architectural changes.
2. Keep provider-specific logic behind provider adapters. The Codex adapter must not become the owner of memory or project state.
3. Keep persistent user data outside replaceable application containers.
4. Enforce authorization and safety policies in trusted application code, never only in prompts.
5. Default to least privilege. Never grant an agent unrestricted root access or unrestricted access to all projects.
6. Never expose PostgreSQL, Redis, internal APIs, or agent control endpoints publicly.
7. Never commit secrets, credentials, private keys, tokens, session data, or production data.
8. Do not perform destructive operations, production deployments, credential rotations, or irreversible migrations without explicit user approval.
9. Do not claim a task, test, backup, deployment, or recovery succeeded unless it was actually executed and verified.
10. Add tests and update documentation with every meaningful behavior change.

## Engineering workflow

- Inspect before modifying.
- Present a concise plan for changes spanning multiple modules.
- Prefer small, reversible changes.
- Add or update tests.
- Run relevant checks and report exact outcomes.
- Document migration and rollback steps for infrastructure or database changes.
- Preserve existing project data and unrelated services.

## Current stage

SOVRAN is in the architecture/planning stage. Do not assume that production paths, DNS, TLS, secrets, or services have been configured. Validate the target environment before deployment.
