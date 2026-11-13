# Autonomous Operating Mode

Owner authorization: Mahdi Zangoei
Applies to: Codex and future SOVRAN execution providers
Default: autonomous development without routine user interruptions

## 1. Autonomy granted

The owner authorizes Codex to proceed without routine confirmation on work required to build SOVRAN, including:
- Inspecting this repository and the dedicated SOVRAN workspace.
- Making architectural and implementation decisions consistent with repository requirements.
- Creating, editing, moving, and deleting files inside the SOVRAN repository/workspace when required for development.
- Installing project-scoped dependencies and tools when safe and resource-appropriate.
- Running tests, linters, formatters, local builds, and disposable development services.
- Debugging and fixing failures.
- Creating feature branches, commits, pushing branches, creating/updating issues and pull requests.
- Updating documentation, project status, changelog, reports, and task checklists.
- Continuing to the next unblocked Phase 1 task after checkpointing the current task.
- Restarting its own SOVRAN development worker when it fails, with bounded retry/backoff.
- Choosing reasonable reversible defaults and documenting assumptions instead of interrupting the owner for minor decisions.

Codex should not ask whether it may continue after each task. It should continue through safe, unblocked work and send concise progress reports.

## 2. Hard safety boundaries

Autonomy does not authorize actions that could compromise the owner's accounts, unrelated data, public infrastructure, or finances. Without fresh explicit authorization for the specific action, Codex must not:
- Delete or overwrite data outside the dedicated SOVRAN workspace.
- Touch /root/projects/selfbot, its database, containers, volumes, credentials, or services.
- Run destructive commands against the host or unrelated projects.
- Change SSH access, firewall rules, provider firewall, DNS, or public routing.
- Publish or deploy a public production service.
- Run migrations against an existing production database.
- Change, reveal, export, or rotate ChatGPT, GitHub, Telegram, server, or provider credentials.
- Send messages to third parties, make purchases, spend money, or create paid infrastructure.
- Disable security controls, expose internal APIs/databases, or grant unrestricted root access.
- Use --yolo / --dangerously-bypass-approvals-and-sandbox on the shared VPS host.

If a hard-boundary action is necessary, continue all other work, create a blocker issue with the exact reason and safe alternatives, and leave that action unperformed.

## 3. Execution containment

- Run Codex as a dedicated non-root account where feasible.
- Limit writable paths to the SOVRAN repository and explicitly registered development workspaces.
- Keep secrets outside Git and redact them from logs.
- Keep databases and internal APIs private.
- Use one active Codex coding task on the currently assessed 1-vCPU / ~1-GiB VPS.
- Do not spawn parallel model agents until a fresh resource assessment supports it.
- Use bounded command timeouts, log rotation, and disk checks.
- Never pass arbitrary model-generated strings directly to a privileged shell.
- Use workspace-write or an equivalent bounded sandbox for unattended development; do not disable the sandbox to avoid prompts.

## 4. Approval-free operation design

Prefer operations that stay inside the approved workspace and configured sandbox. If a command is blocked by the sandbox, do not escalate to unrestricted host access. Find a safer route, use a project-local tool, or record a blocker.

Network access for package downloads and Git operations must be configured deliberately. Do not silently broaden host-wide network or filesystem permissions. Use existing authenticated Git remotes and least-privilege credentials.

## 5. Long-running operation and recovery

The development runner must survive SSH disconnects and terminal closure:
- Use a persistent supervisor (systemd service is preferred for reboot recovery; tmux is acceptable for a manually managed session).
- Persist task state and checkpoints to GitHub and local project reports.
- Use restart policies with backoff to avoid restart loops.
- On startup, inspect Git state and recover the last incomplete task from issue/task records.
- Never start a duplicate Codex process for a task already running.
- Write logs to a dedicated SOVRAN log directory with rotation.
- On SIGTERM, stop accepting new tasks, checkpoint current state, and exit gracefully.
- A host reboot should restart the worker only after network, filesystem, and required dependencies are ready.

A detached terminal alone does not guarantee reboot recovery. Validate the supervisor and recovery path before claiming continuous operation.

## 6. Required reporting

After every checkpoint, update docs/PROJECT_STATUS.md and report active issue/task state, work completed, commit SHA and PR URL, tests and exact results, blockers, and next task.
Do not fabricate progress. If blocked, continue independent tasks and clearly report the blocker.

## 7. Initial instruction

Start Phase 1 from docs/PHASE_1_EXECUTION.md. Work autonomously through all safe, unblocked tasks. Do not deploy publicly. Do not modify unrelated workloads. Do not stop merely because the user is offline or the SSH terminal disconnects.