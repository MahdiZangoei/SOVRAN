# SOVRAN Project Status

**Last updated:** 2026-11-13  
**Overall state:** Kickoff / architecture baseline  
**Current phase:** Phase 1 — Foundation and Codex Execution  
**Production deployment:** Not started

## Verified repository state

- Private repository: `MahdiZangoei/SOVRAN`
- Main branch contains initial product and infrastructure documents.
- Kickoff work is being prepared on `codex/project-kickoff`.

## Verified VPS baseline (user-provided report)

- Ubuntu 24.04.5 LTS
- 1 vCPU
- Approximately 961 MiB RAM
- 2 GiB swap
- Approximately 19 GiB root filesystem
- Python 3.12.3
- Codex CLI 0.167.0
- Docker 29.1.3 / Compose 2.40.3
- Node.js/npm not installed at assessment time
- Existing selfbot project and database are out of SOVRAN scope

Re-assess before deployment.

## Product decisions

- Platform name: SOVRAN
- Central assistant identity: SOV
- Logo direction: AI Core + S monogram
- Dashboard direction: cinematic, mobile-first dark UI
- Greeting: "خوش آمدی. تمام سیستم‌ها فعال هستند. منتظر فرمان شما هستم."
- Deployment: hybrid Systemd + Docker Compose
- Proposed dashboard: `panel.sovran.digitalclassic.ir`
- Access: public HTTPS, strong authentication, MFA
- Backup: encrypted external storage; provider not selected
- Initial execution provider: Codex CLI
- Future providers: Claude Code, Gemini, local models

## Current blockers / not yet verified

- DNS record and public IP mapping
- TLS/reverse proxy configuration
- Backup provider and recovery-key custody
- Current Codex authentication and non-interactive CLI capabilities
- Current VPS resource availability
- Exact state of existing Docker volumes and backups

## Next actions

1. Clone repository into a dedicated `/root/projects/sovran` directory without touching existing projects.
2. Inspect environment and Codex CLI capabilities.
3. Implement Phase 1 foundation and tests.
4. Open a PR and report results.
5. Do not deploy public services in Phase 1.
