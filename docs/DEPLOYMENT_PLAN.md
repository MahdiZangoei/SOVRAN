# SOVRAN Deployment Plan

**Target:** Ubuntu 24.04 VPS  
**Model:** Hybrid Systemd + Docker Compose  
**Domain:** `sovran.digitalclassic.ir`  
**Proposed dashboard:** `panel.sovran.digitalclassic.ir`  
**Dashboard exposure:** Public HTTPS with strong authentication and MFA  
**Backup:** Encrypted, provider-neutral remote storage

## 1. Deployment topology

### Host-managed services (Systemd)
- SOVRAN API
- Telegram bot
- Mission/agent worker
- Scheduler
- Backup orchestration

These services need controlled host integration, access to the Codex CLI, and narrowly scoped project workspaces.

### Containerized services (Docker Compose)
- Dashboard static/runtime service when justified
- PostgreSQL only if a separate SOVRAN database is justified after inspecting existing workloads
- Redis only if measured queue/lock requirements justify it

Do not assume all listed services should run on the initial 1-GiB VPS. Begin with the smallest viable footprint.

### Reverse proxy
Nginx or another maintained reverse proxy terminates TLS and forwards only the dashboard/API routes required by the deployment.

## 2. Domain and network

- Configure DNS for `panel.sovran.digitalclassic.ir` only after confirming the intended VPS address.
- Obtain and renew TLS certificates automatically.
- Redirect HTTP to HTTPS.
- Use secure headers and request size limits.
- Apply rate limiting to authentication and sensitive endpoints.
- Keep API, PostgreSQL, Redis, worker control ports, and metrics private.
- Telegram bot should use outbound polling initially; no inbound Telegram webhook port is required.

DNS and TLS are not configured merely by documenting these hostnames.

## 3. Public dashboard security baseline

- Disable public registration.
- Require strong authentication and MFA (TOTP or passkey).
- Use secure, HttpOnly, SameSite cookies.
- Rotate and revoke sessions.
- Rate-limit login and recovery flows.
- Log authentication and administrative events.
- Enforce CSRF protections where cookie authentication is used.
- Validate authorization on every API operation.
- Consider an additional IP allowlist or access gateway for administrative routes.
- Do not expose internal APIs directly.
- Never use a model prompt as the sole permission enforcement mechanism.

## 4. Codex execution isolation

- Run Codex under a dedicated non-root service account where feasible.
- Grant access only to registered project workspaces.
- Use per-project execution directories and explicit environment allowlists.
- Record command, working directory, task, provider session reference, exit status, and artifact references.
- Prevent arbitrary path traversal and unrestricted host command execution.
- Separate development permissions from production operations.
- Require explicit approval for destructive operations and production deployment.
- Do not store provider credentials in project reports or Git.

Codex CLI invocation and resume semantics must be validated against the installed version before implementation. A provider session is not a substitute for SOVRAN's own task and conversation archive.

## 5. Backup architecture

Use a provider-neutral storage adapter. Candidate protocols include S3-compatible object storage, SFTP, or WebDAV; the actual provider remains undecided.

Recommended backup content:
- PostgreSQL consistent backups
- SOVRAN configuration templates (never plaintext secrets)
- Project metadata and portable documentation
- Mission/task/report records
- Conversation archives selected by retention policy
- Export manifests and checksums

Recommended approach:
- Use Restic or an equivalent audited encrypted backup tool.
- Encrypt before remote upload.
- Keep recovery keys outside the VPS in a secure offline location.
- Use separate credentials with least privilege.
- Enable retention and repository integrity checks.
- Perform periodic restore drills.
- Maintain a local short-retention copy only as a convenience, not as the only backup.

## 6. Resource strategy for current VPS

Observed capacity is approximately 1 vCPU, 1 GiB RAM, 2 GiB swap, and 19 GiB root disk.

Initial deployment constraints:
- One active Codex task at a time.
- No always-on multi-agent fan-out.
- No heavyweight monitoring stack initially.
- Avoid building the frontend on the VPS if it creates memory pressure.
- Set container memory limits and log rotation.
- Monitor disk, memory, swap, and process restarts.
- Keep adequate free disk for backups and rollback.

A larger VPS may be needed before enabling a full dashboard build pipeline, multiple providers, parallel agents, or voice services.

## 7. Rollout sequence

1. Re-check host resources and existing Docker volumes/configuration without exposing secrets.
2. Confirm DNS ownership and target address.
3. Establish firewall/SSH rollback plan.
4. Create dedicated SOVRAN service account and directories.
5. Establish secret handling and backup recovery key custody.
6. Implement minimal API and health endpoint.
7. Implement Telegram bot with user allowlist.
8. Implement Codex adapter and workspace restrictions.
9. Add durable project/mission/report storage.
10. Configure encrypted backup and verify a restore.
11. Deploy dashboard behind TLS and MFA.
12. Run security, integration, and recovery tests.

## 8. Rollback requirements

Every infrastructure change must have:
- A recorded pre-change state.
- A tested rollback command or procedure.
- A backup of modified configuration.
- A check that existing workloads remain healthy.
- A post-change verification report.

Never overwrite or stop unrelated services during SOVRAN deployment.
