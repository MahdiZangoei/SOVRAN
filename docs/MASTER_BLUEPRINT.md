# SOVRAN Master Blueprint

**Version:** 1.0  
**Status:** Proposed architecture  
**Owner:** Mahdi Zangoei

## 1. Vision

SOVRAN is a personal AI operating system with a stable identity, durable memory, project awareness, mission orchestration, and multiple interchangeable AI execution providers.

SOV is the central conversational assistant. Agents are workers. Providers are replaceable engines. Missions are units of work. SOVRAN-owned storage provides continuity.

## 2. Core principles

- Provider independence: no provider session is the canonical source of project truth.
- Data ownership: projects, memory, reports, decisions, and archives remain portable.
- Autonomous by default within explicit policy boundaries.
- Least privilege and approval gates for sensitive operations.
- Auditable actions and truthful progress reporting.
- Modular services and reversible deployment.
- Recoverability through encrypted backups and tested restores.

## 3. Logical architecture

### Interfaces
- Telegram Bot (initial mobile interface)
- Responsive web dashboard
- Voice interface (future)
- Desktop/mobile native clients (future)

### SOVRAN Core
- Identity and personality
- Conversation and intent routing
- Context and memory retrieval
- Mission planning and lifecycle
- Decision and policy enforcement
- Scheduler and notifications
- Audit and reporting

### Agent orchestration
- Agent and provider registries
- Dispatcher and queue
- Session manager
- Context builder
- Supervisor and result evaluator
- Workflow and retry manager

### Execution providers
- Initial: OpenAI Codex CLI
- Future candidates: Claude Code, Gemini CLI, local model adapters, custom tools

### Integrations
- Git and GitHub
- Linux host operations
- Docker
- WordPress and custom APIs
- Browser, email, and calendar (future, permission-gated)

### Storage
- PostgreSQL for structured source-of-truth records
- Redis where queueing, locks, or transient coordination are justified
- Filesystem/object storage for documents, artifacts, and archives
- Git for source history
- Encrypted remote backup repository

## 4. Domain modules

### Identity
Owns stable assistant identity, language, tone, greeting, and user preferences.

### Memory
Separates personal preferences, project knowledge, operational events, and strategic objectives. Supports retrieval, versioning, export, restore, retention, and explicit deletion.

### Projects
Tracks repositories, workspace paths, architecture, decisions, current state, reports, and next steps. Each project has isolated context and access policy.

### Missions
Each mission records objective, success criteria, priority, budget/time constraints, dependencies, assigned agents, approvals, state, events, and final report.

Suggested states: PLANNED, ANALYZING, READY, EXECUTING, WAITING, REVIEWING, COMPLETED, FAILED, CANCELLED.

### Agents
Roles may include technical lead, developer, reviewer, QA, security, DevOps, research, and documentation. In the first release these may be logical roles backed by one Codex provider.

### Providers
Expose a normalized capability and execution interface. Provider sessions are references and execution details, not the canonical conversation archive.

### Permissions
Trusted application code enforces capabilities, workspace boundaries, command policies, approval requirements, and audit records. Model instructions alone are never a security boundary.

## 5. Permission model

- Read: inspect authorized files, logs, and project state.
- Development: modify authorized workspace files, run tests, and use approved dependencies.
- Operations: manage explicitly allowlisted development services.
- Sensitive: production deploys, destructive migrations, permanent deletion, credential changes, financial actions, and public communications.

Sensitive actions require explicit, scoped approval. Approval must identify the action, target, and relevant parameters and expire after a defined period.

## 6. Portability

Each project should maintain portable records such as:
- PROJECT_REPORT.md
- PROJECT_CONTEXT.md
- ARCHITECTURE.md
- DECISIONS.md
- CHANGELOG.md
- TASK_HISTORY.md
- SESSION_HISTORY.md
- NEXT_STEPS.md
- project.json

Project export should include source, documentation, reports, selected conversation archives, and metadata. Secrets and provider credentials are excluded by default.

## 7. Initial release boundary

The first release should prove:
1. Telegram-to-SOV conversation.
2. Project registry and isolated workspace configuration.
3. Codex CLI adapter with persistent task tracking.
4. Mission/task lifecycle and progress reporting.
5. Durable reports and conversation archival.
6. Safe command execution and audit log.
7. Encrypted backup and verified restore path.

The web dashboard can initially be a lightweight operational interface and grow after the core API is stable.

## 8. Non-goals for the first release

- Unrestricted autonomous root access.
- Automatic production deployment.
- Multiple full model providers before the adapter contract is tested.
- Expensive always-on multi-agent concurrency on the current small VPS.
- Storing secrets in Git or ordinary project exports.

## 9. Definition of done

A feature is complete only when implementation, tests, security review, documentation, error handling, observability, and recovery implications have been addressed and acceptance criteria pass.
