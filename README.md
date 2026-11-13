# SOVRAN

**Autonomous Personal AI Operating System**  
**Central assistant:** SOV  
**Motto:** ONE CORE. INFINITE POSSIBILITIES.

SOVRAN is a provider-independent personal AI command platform. It connects conversational interfaces (initially Telegram and a mobile-first web dashboard) to projects, persistent memory, missions, and interchangeable execution providers.

> Status: **Architecture and planning stage.** No production services have been deployed from this repository yet.

## Product principles

- SOVRAN owns its identity, memory, project records, reports, and archives.
- AI providers are replaceable execution engines, not the system of record.
- Codex CLI is the first execution adapter; future adapters may include Claude Code, Gemini CLI, and local models.
- Missions have explicit objectives, acceptance criteria, state, and audit history.
- Autonomous work is bounded by centrally enforced permissions and policies.
- Sensitive or destructive actions require explicit approval.
- Backups must be encrypted, portable, and periodically restore-tested.

## Initial deployment decisions

| Area | Decision |
|---|---|
| Deployment | Hybrid: Systemd for host-integrated services; Docker Compose for isolated infrastructure |
| Base domain | `sovran.digitalclassic.ir` |
| Proposed dashboard | `panel.sovran.digitalclassic.ir` |
| Dashboard access | Public HTTPS with strong authentication and MFA |
| Backup | Encrypted, provider-neutral remote storage adapter |
| Initial provider | OpenAI Codex CLI |
| Primary interfaces | Telegram + responsive web dashboard |

The dashboard hostname is a proposal and must not be considered live until DNS and TLS are configured.

## Repository map

```text
.
├── AGENTS.md
├── docs/
│   ├── MASTER_BLUEPRINT.md
│   ├── INFRASTRUCTURE_ASSESSMENT.md
│   ├── DEPLOYMENT_PLAN.md
│   └── ROADMAP.md
├── .env.example
└── .gitignore
```

## Development status

This repository currently contains the initial product blueprint and deployment plan. Runtime code, database migrations, API contracts, and deployment automation will be added in reviewed phases.

## Security

- Never commit credentials, tokens, private keys, session files, database dumps, or real `.env` files.
- Keep internal APIs and databases off public interfaces.
- Do not mount the Docker socket into application containers.
- Run agents with least privilege and project-scoped filesystem access.
- Treat model output as untrusted input; enforce permissions outside the model.
- Keep an offline recovery copy of backup encryption keys.

See [Security and deployment requirements](docs/DEPLOYMENT_PLAN.md).

## Owner

Private project owned by **Mahdi Zangoei**.
