# Infrastructure Assessment

**Assessment source:** User-provided read-only shell report  
**Assessment timestamp:** 2026-11-13 01:41 UTC  
**Target OS:** Ubuntu VPS  
**Status:** Initial baseline; re-check before deployment

## 1. Observed environment

| Component | Observed result |
|---|---|
| OS | Ubuntu 24.04.5 LTS |
| Kernel architecture | Linux x86_64 |
| CPU allocation | 1 vCPU |
| CPU model | Intel Xeon E-2288G |
| Memory | Approximately 961 MiB RAM |
| Swap | 2 GiB |
| Root disk | Approximately 19 GiB |
| Python | 3.12.3 |
| Codex CLI | 0.167.0 |
| Node.js / npm | Not installed |
| Docker Engine | 29.1.3 |
| Docker Compose | 2.40.3 |
| Existing Docker workload | One healthy container identified as a selfbot database |
| Nginx | Not active |
| UFW | Inactive |
| Existing projects | `/root/projects/selfbot` (~1.2 GiB) and `/root/projects/self` |
| SOVRAN directories | Not created at assessment time |

## 2. Important constraints

The VPS is very small for a full multi-service deployment. A 1-vCPU / ~1-GiB RAM host cannot safely run a heavy Next.js build, PostgreSQL, Redis, monitoring stack, multiple concurrent Codex agents, and the API all at once.

The initial design must therefore be resource-conscious:
- Avoid multiple concurrent coding agents.
- Do not install duplicate databases without checking existing workloads and resource usage.
- Prefer a lightweight dashboard build/deploy process; build frontend assets elsewhere if necessary.
- Add Redis only when a measured queue/locking need justifies its memory cost.
- Configure explicit memory and CPU limits for containers.
- Monitor disk usage and Docker image growth.
- Keep swap as an emergency buffer, not as a substitute for RAM.

## 3. Security observations

The supplied report showed:
- UFW inactive.
- SSH listening on public interfaces.
- Nginx inactive.
- Existing database listener bound to loopback.
- Existing Docker workload must be treated as out of scope.

These observations are not a complete security audit. Before public dashboard deployment:
1. Confirm provider firewall rules and current SSH access method.
2. Establish a safe firewall policy without locking out SSH.
3. Restrict SSH to trusted sources where practical and use key authentication.
4. Install and configure a reverse proxy with TLS.
5. Expose only required web ports.
6. Keep database, Redis, and internal API private.
7. Review Docker port publishing and container privileges.
8. Add MFA, rate limiting, secure sessions, and audit logging.

Do not change firewall or SSH settings without a tested rollback path and an active recovery session.

## 4. Existing workloads and data protection

The existing `/root/projects/selfbot` workspace and its database container are not SOVRAN resources. Do not move, rename, rebuild, stop, or modify them as part of SOVRAN setup.

Before any deployment:
- Inspect the existing Compose project and its volumes without printing secrets.
- Confirm available disk and memory under normal workload.
- Identify existing backup coverage.
- Keep SOVRAN data and services isolated.
- Avoid sharing databases or credentials between projects.

## 5. Assessment limitations

This report is based only on the output supplied by the user. It does not establish:
- Public IP or DNS state.
- Domain ownership or DNS records.
- Provider-level firewall rules.
- Actual available CPU guarantees.
- Database volume size or backup quality.
- Codex authentication validity.
- Existing service configuration details.
- TLS or certificate state.

Re-run a sanitized assessment before production deployment.
