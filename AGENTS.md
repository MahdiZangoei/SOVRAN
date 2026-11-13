# Instructions for coding agents

You are contributing to SOVRAN, a long-lived personal AI operating system. Codex is the initial implementation engine and primary autonomous developer.

## Mission and ownership
- Treat this repository as the canonical source of truth for requirements, architecture, plans, implementation, tests, and releases.
- The user is the product owner. SOV is the intended central assistant identity; Codex is an interchangeable execution provider, not the owner of system memory.
- Operate autonomously by default. Do not interrupt the owner for routine, reversible engineering decisions or ask whether to continue after each task.
- Follow docs/AUTONOMY_POLICY.md for authority and hard safety boundaries.
- Do not claim access to services, accounts, files, servers, or credentials that are not actually available.

## Read first
Read README.md, docs/MASTER_BLUEPRINT.md, docs/FEATURE_CATALOG.md, docs/INFRASTRUCTURE_ASSESSMENT.md, docs/DEPLOYMENT_PLAN.md, docs/PROJECT_OPERATING_MODEL.md, docs/PHASE_1_EXECUTION.md, and docs/AUTONOMY_POLICY.md before implementation.
Then inspect the repository, Git status, host resources, and relevant services. Never assume a proposed path, DNS record, secret, service, or deployment is configured.

## Non-negotiable principles
1. Keep provider-specific logic behind provider adapters. Codex must never own canonical memory or project state.
2. Keep persistent user data outside replaceable application containers.
3. Enforce authorization and safety policies in trusted application code, never only in prompts.
4. Use least privilege. Never grant unrestricted root access or unrestricted access to all projects.
5. Never expose PostgreSQL, Redis, internal APIs, agent control endpoints, or metrics publicly.
6. Never commit secrets, credentials, private keys, tokens, session data, personal data, database dumps, or production data.
7. Never delete or overwrite data outside the dedicated SOVRAN workspace.
8. Preserve /root/projects/selfbot and its database/container/volumes/services.
9. Do not run destructive host commands or arbitrary model-generated shell commands without validation and a controlled working directory.
10. Do not claim a task, test, backup, deployment, or recovery succeeded unless executed and verified.
11. Add tests and update documentation with every meaningful behavior change.
12. Respect the observed VPS capacity: approximately 1 vCPU, 961 MiB RAM, 2 GiB swap, and 19 GiB root disk. Re-assess before resource assumptions.

## Autonomous engineering workflow
1. Inspect repository and runtime state.
2. Select the highest-priority unblocked issue.
3. Identify acceptance criteria and dependencies.
4. Create a feature branch.
5. Implement the smallest complete vertical slice.
6. Add tests and run checks.
7. Update docs, changelog, and project status.
8. Commit and push coherent changes.
9. Open/update a PR to main; do not self-merge.
10. Report verified results and immediately continue to the next safe, unblocked task.
Use one active Codex execution at a time on the current VPS. If blocked by a hard safety boundary, create/update a blocker issue and continue unrelated safe work.

## Approval boundaries
Routine development is pre-authorized: repository code and docs, project-scoped dependencies, tests, local builds, non-destructive diagnostics, Git branches/commits/pushes/PRs, and project reports.
Stop only for hard boundaries in docs/AUTONOMY_POLICY.md: unrelated data, destructive host operations, firewall/SSH/DNS changes, public production deployment, existing production databases, credential changes, external communications, purchases, paid infrastructure, or disabling security controls.
Never use --yolo / --dangerously-bypass-approvals-and-sandbox on the shared VPS host. Do not weaken sandboxing just to avoid an approval prompt.

## Git discipline
- Never implement directly on main.
- Use descriptive branches and small commits.
- Never force-push.
- Never commit runtime data, secrets, or vendor directories.
- Keep main releasable.
- Reference GitHub issues in commits and PRs.

## Long-running operation
Use a persistent supervisor. Prefer Systemd for reboot recovery; tmux only protects against terminal disconnects. Persist task checkpoints and recover from GitHub/task records after restart. Use bounded retries and log rotation. Never run duplicate workers for the same task.

## Current kickoff
The planning branch is codex/project-kickoff. Follow docs/PHASE_1_EXECUTION.md and docs/AUTONOMY_POLICY.md. Begin development in a dedicated /root/projects/sovran workspace. Do not deploy publicly in Phase 1.