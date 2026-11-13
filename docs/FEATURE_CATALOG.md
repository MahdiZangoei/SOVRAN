# SOVRAN Feature Catalog

**Version:** 1.0  
**Status:** Product requirements baseline  
**Owner:** Mahdi Zangoei

This catalog records the intended product scope. Items are planned unless explicitly marked implemented and verified.

## A. Identity and interaction

- [ ] Stable assistant identity: SOVRAN platform, SOV central assistant.
- [ ] Hybrid personality: professional, friendly, calm, strategic, technically precise.
- [ ] Persian-first communication with English support.
- [ ] Configurable greeting, tone, verbosity, and language.
- [ ] Conversation continuity across Telegram and web.
- [ ] Text chat in first release.
- [ ] Voice messages, speech-to-text, and text-to-speech in later releases.
- [ ] Clear distinction between suggestions, plans, running actions, and verified results.

## B. Interfaces

### Telegram
- [ ] Owner allowlist based on Telegram numeric user ID.
- [ ] Private command interface.
- [ ] Natural-language conversation.
- [ ] Project and mission selection.
- [ ] Start, pause, resume, cancel, and inspect tasks.
- [ ] Progress notifications and final reports.
- [ ] Send/receive documents, logs, screenshots, and export archives.
- [ ] Inline approvals for sensitive actions.
- [ ] Voice message support in a later release.
- [ ] Bot must remain responsive while long-running work executes in background workers.

### Web dashboard
- [ ] Mobile-first, cinematic dark interface.
- [ ] Proposed URL: `panel.sovran.digitalclassic.ir`.
- [ ] Secure login, MFA, session management, and account recovery.
- [ ] Command Center with health, active missions, projects, agent status, and recent events.
- [ ] Conversation interface.
- [ ] Projects and project detail pages.
- [ ] Mission board and mission detail pages.
- [ ] Agent/provider registry and execution status.
- [ ] Memory browser and search.
- [ ] Reports and activity timeline.
- [ ] Infrastructure health view.
- [ ] Archive, backup, export, and restore management.
- [ ] Security, permissions, approvals, and audit log.
- [ ] Settings and integrations.
- [ ] Realtime status updates.
- [ ] Responsive desktop, tablet, and mobile layouts.

## C. Projects

- [ ] Project registry independent of provider sessions.
- [ ] Project name, description, repository URL, workspace path, branch, status, tags, and owner.
- [ ] Per-project context and technical decisions.
- [ ] Per-project task and mission history.
- [ ] Per-project reports and next steps.
- [ ] Workspace allowlist and filesystem boundary.
- [ ] Git status, branch, commit, and PR visibility.
- [ ] Project onboarding and repository inspection.
- [ ] Project archive and portable ZIP export.
- [ ] Project import and recovery.
- [ ] Multiple independent projects.
- [ ] No accidental cross-project context or file access.

## D. Missions and task management

- [ ] Natural-language request converted into a mission proposal.
- [ ] Mission objective and measurable acceptance criteria.
- [ ] Task decomposition and dependency graph.
- [ ] Priority, schedule, optional budget/resource limits.
- [ ] Assignment to one or more logical agent roles.
- [ ] State machine: PLANNED, ANALYZING, READY, EXECUTING, WAITING, REVIEWING, COMPLETED, FAILED, CANCELLED.
- [ ] Task queue and durable execution state.
- [ ] Progress events and user notifications.
- [ ] Retry policy for transient failures.
- [ ] Cancellation and safe interruption.
- [ ] Resume after process/server restart.
- [ ] Replanning after failure.
- [ ] Final report with changed files, commits, tests, risks, and next steps.
- [ ] No fabricated progress or completion claims.

## E. Codex provider — first execution engine

- [ ] Detect Codex CLI path and version.
- [ ] Detect authentication state without exposing credentials.
- [ ] Provider capability declaration.
- [ ] Start Codex task in a registered workspace.
- [ ] Persistent SOVRAN task/session mapping.
- [ ] Capture stdout, stderr, exit code, timestamps, and artifacts.
- [ ] Resume supported Codex sessions where the installed CLI supports it.
- [ ] Timeout, cancellation, and process supervision.
- [ ] Safe handling of non-interactive execution.
- [ ] Explicit policy for network, shell, filesystem, and approval modes.
- [ ] One active Codex task at a time on the current VPS.
- [ ] Never rely solely on `codex resume --last` as durable task identity; persist explicit session/task references and SOVRAN-side history.
- [ ] Provider migration without losing SOVRAN memory or reports.

## F. Multi-agent orchestration — future staged capability

- [ ] Logical roles: Technical Lead, Developer, Reviewer, QA, Security, DevOps, Research, Documentation.
- [ ] Supervisor and independent result evaluator.
- [ ] Task delegation and handoff.
- [ ] Agent capability registry.
- [ ] Per-agent permissions and budgets.
- [ ] Bounded concurrency and resource-aware scheduling.
- [ ] Agent messages and decision trace.
- [ ] Conflict resolution and integration of parallel changes.
- [ ] Human escalation for ambiguous or sensitive decisions.
- [ ] Initial release may simulate roles sequentially using one Codex provider.

## G. Provider independence

- [ ] Common provider adapter contract.
- [ ] Codex adapter first.
- [ ] Claude Code adapter later.
- [ ] Gemini CLI/API adapter later.
- [ ] Local LLM adapter later.
- [ ] Provider capability discovery.
- [ ] Provider health and availability.
- [ ] Per-provider configuration and secret references.
- [ ] Routing by task type, cost, capability, and availability.
- [ ] Provider-neutral conversation and task archives.
- [ ] Provider switching without data loss.

## H. Memory and knowledge

- [ ] Personal preferences memory.
- [ ] Project memory.
- [ ] Operational memory.
- [ ] Strategic memory.
- [ ] Search and retrieval.
- [ ] Source attribution and timestamps.
- [ ] Memory versioning and correction.
- [ ] Context snapshots.
- [ ] Retention and privacy controls.
- [ ] Explicit export and deletion.
- [ ] Portable Markdown/JSON representations.
- [ ] Conversation archive independent of provider history.

## I. Reports and observability

- [ ] Per-task execution report.
- [ ] Per-mission report.
- [ ] Per-project living report.
- [ ] Daily/weekly activity summaries.
- [ ] Error and incident log.
- [ ] Provider usage and runtime metrics where available.
- [ ] CPU, RAM, disk, swap, and service health.
- [ ] Git commit and PR references.
- [ ] Backup success/failure reports.
- [ ] Notifications for blockers and completed work.
- [ ] Report retention and export.

## J. Backup, archive, and portability

- [ ] Encrypted local staging backup.
- [ ] Encrypted external backup adapter.
- [ ] Provider-neutral target support: S3-compatible, SFTP, WebDAV, or other supported backend.
- [ ] Database-consistent backups.
- [ ] Project source and documentation export.
- [ ] Conversation and mission archive export.
- [ ] Full SOVRAN export.
- [ ] Checksums and manifests.
- [ ] Retention policies.
- [ ] Offline recovery key custody.
- [ ] Restore verification and scheduled restore drills.
- [ ] Import to a new VPS.
- [ ] No secrets in normal ZIP exports by default.

## K. Infrastructure and integrations

- [ ] Hybrid deployment: Systemd host services + Docker Compose where justified.
- [ ] Health endpoints and service supervision.
- [ ] Nginx/TLS reverse proxy.
- [ ] Public dashboard with private internal APIs.
- [ ] Resource-aware execution and concurrency.
- [ ] GitHub integration.
- [ ] SSH/host operations with allowlists.
- [ ] Docker integration with no default Docker socket exposure.
- [ ] WordPress/custom API integrations later.
- [ ] Email/calendar/browser integrations later.
- [ ] Integration credential references stored securely.
- [ ] Infrastructure monitoring and safe self-healing.

## L. Security and governance

- [ ] Central policy engine outside model prompts.
- [ ] User and service identity.
- [ ] Role/capability permissions.
- [ ] Project workspace isolation.
- [ ] Command allowlist/validation and execution sandbox.
- [ ] MFA and secure sessions.
- [ ] Rate limiting and brute-force controls.
- [ ] CSRF protection where applicable.
- [ ] Audit log for actions, approvals, and permission changes.
- [ ] Secret management and rotation procedures.
- [ ] Approval gates for destructive, production, financial, credential, and external communication actions.
- [ ] Backup encryption and recovery key separation.
- [ ] Dependency and container scanning.
- [ ] Security incident and recovery procedures.

## M. Quality and engineering operations

- [ ] Unit, integration, and end-to-end tests.
- [ ] Linting, formatting, and type checking.
- [ ] CI on pull requests.
- [ ] Database migrations and rollback notes.
- [ ] Structured logs and correlation IDs.
- [ ] Health/readiness checks.
- [ ] Release notes and version tags.
- [ ] Feature flags for risky modules.
- [ ] Resource budgets and load tests appropriate to VPS size.
- [ ] Documentation updated with every meaningful feature.

## N. Explicit non-goals for initial MVP

- Unrestricted root execution.
- Automatic production deployment.
- Unlimited parallel agents.
- Publicly exposed database, Redis, or internal API.
- Storing secrets in Git.
- Depending on Codex chat/session history as the only memory.
- Running expensive local LLM inference on the current VPS.
