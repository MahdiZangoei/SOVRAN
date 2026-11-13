# Phase 1 — Foundation and Codex Execution

**Goal:** Build the smallest safe, testable SOVRAN core that can receive a Telegram request, persist a task, execute it through Codex in an approved project workspace, and return a truthful report.

**Deployment target:** Development only. No public dashboard or production deployment in this phase.

## 1. Preconditions

- Repository checked out at `/root/projects/sovran` (do not reuse or overwrite `/root/projects/selfbot`).
- Git remote points to `https://github.com/MahdiZangoei/SOVRAN.git`.
- Codex CLI availability and authentication verified without printing tokens.
- Current VPS resources re-measured.
- Existing Docker containers, volumes, databases, and project directories inventoried read-only.
- No secrets committed to Git.

If the repository path already exists, inspect it and its Git status first. Never delete or overwrite an existing directory to make the clone succeed.

## 2. Phase 1 scope

### A. Application skeleton
- Python 3.12 compatible project.
- Clear package boundaries.
- Typed configuration using environment variables.
- Safe defaults and validation.
- Structured logging with secret redaction.
- Health/readiness endpoint.
- Graceful shutdown.

### B. Persistence
- Select the lightest reliable initial persistence approach after assessing the existing environment.
- Do not connect to or modify the selfbot database.
- If SQLite is selected for the first low-resource MVP, isolate it behind repositories and document the migration path to PostgreSQL.
- If PostgreSQL is selected, provision a separate database/user and verify resource headroom first.
- Add migrations and backups from the start.

### C. Project registry
- Register project name, repository URL, workspace path, default branch, status, and access policy.
- Enforce canonical path resolution and allowed workspace roots.
- Reject path traversal and symlink escapes.
- Register only explicitly approved workspaces.

### D. Task and audit model
- Durable task ID and states.
- Store user request, project reference, provider, execution timestamps, result summary, exit status, and artifact references.
- Audit every state transition and tool invocation.
- Support queued, running, waiting, completed, failed, and cancelled states.

### E. Codex adapter
- Detect CLI path/version.
- Verify non-interactive execution capabilities of the installed version.
- Use documented CLI options discovered from `codex --help`; do not guess flags.
- Run as a non-root service account if practical.
- Use explicit working directory and project allowlist.
- Capture stdout/stderr and exit code.
- Persist explicit Codex session/task identifiers where supported.
- Do not rely only on `codex resume --last`.
- Enforce timeout, cancellation, and one active task at a time.
- Never grant unrestricted root shell access.

### F. Telegram integration
- Aiogram 3 or another justified lightweight implementation.
- Allow only the configured owner Telegram numeric ID.
- Commands: /start, /help, /status, /projects, /project, /run, /task, /cancel, /report.
- Long tasks execute in background; bot remains responsive.
- Send progress checkpoints and final report.
- Do not expose tokens in logs or error messages.

### G. Reports
- Generate Markdown task report.
- Update project status and next steps.
- Record commit hash and test results when available.
- Archive conversation/task metadata in provider-neutral format.

## 3. Explicit exclusions

- Public dashboard
- Multi-provider execution
- Parallel multi-agent execution
- Voice interface
- Production deployment
- DNS, TLS, or firewall changes
- Automatic destructive operations
- Access to unrelated workspaces

## 4. Acceptance criteria

1. Application starts with validated configuration and no secrets in logs.
2. Health endpoint reports service state.
3. A project can be registered and its workspace boundary is tested.
4. An authorized Telegram user can request status and list registered projects.
5. A task can be persisted before execution.
6. A Codex task runs only inside the selected registered workspace.
7. Output, error, exit code, timestamps, and task state are persisted.
8. Restarting the service does not erase task history.
9. An unauthorized Telegram user is rejected without revealing system details.
10. Cancellation and timeout are handled safely.
11. Unit and integration tests pass.
12. Documentation describes installation, configuration, operations, and rollback.
13. Existing selfbot files, database, containers, and services remain unchanged.

## 5. Resource constraints

- One active Codex task.
- Avoid Redis unless needed and measured.
- Avoid a second database service unless resource headroom is demonstrated.
- No frontend build on the VPS unless memory headroom is measured.
- Use bounded logs and disk usage.
- Stop and report if the system approaches memory/disk exhaustion.

## 6. Required deliverables

- Working source code
- Tests
- Example configuration without secrets
- Database schema/migrations or documented initial storage choice
- Systemd unit templates (not installed in production during this phase)
- Telegram setup instructions
- Codex adapter documentation
- Security notes
- Updated `docs/PROJECT_STATUS.md`
- PR against main

## 7. Completion report

Codex must report:
- Implemented features
- Files changed
- Commands run
- Test results
- Commit and PR links
- Resource observations
- Known limitations
- Next unblocked issue
- Any approval needed
