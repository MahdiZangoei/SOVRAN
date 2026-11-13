# SOVRAN Project Operating Model

## 1. Source of truth

GitHub repository `MahdiZangoei/SOVRAN` is the canonical source for:
- Requirements and feature catalog
- Architecture decisions
- Roadmap and issue backlog
- Source code and tests
- Deployment templates
- Operational documentation
- Release notes

The VPS is an execution environment, not the only place project knowledge exists.

## 2. Roles

### Product owner — Mahdi
Sets goals, priorities, product preferences, and approvals for sensitive actions.

### Central assistant identity — SOV
Future user-facing coordinator. Maintains continuity and translates goals into missions.

### Primary implementation agent — Codex
Implements code, tests, documentation, fixes, and routine project management tasks. Codex works from GitHub issues and repository instructions.

### Future logical team
Technical Lead, Developer, Reviewer, QA, Security, DevOps, Research, Documentation. On the current VPS these roles should be executed sequentially or with very limited concurrency, not as many simultaneously running processes.

## 3. Work intake

Every substantial request becomes a GitHub issue or a task linked to an existing issue. Each task should include:
- Context and motivation
- Scope
- Non-goals
- Acceptance criteria
- Dependencies
- Security/resource constraints
- Test expectations
- Documentation expectations

## 4. Execution lifecycle

1. Select the highest-priority unblocked issue.
2. Read relevant architecture and feature requirements.
3. Inspect code and environment.
4. Write an implementation plan.
5. Create a feature branch.
6. Implement a small complete slice.
7. Add tests and documentation.
8. Run checks and record exact results.
9. Commit and push.
10. Open a PR to main.
11. Report summary, tests, risks, and next task.
12. Continue with the next unblocked issue when safe.

Codex must not merge its own PRs to main by default. A human approval or an explicitly configured repository policy is required.

## 5. Reporting format

Every completed work session must update:
- `docs/PROJECT_STATUS.md`
- Relevant issue checklist
- `CHANGELOG.md` once implementation begins

The user-facing report must include:
- What changed
- Files changed
- Tests executed and exact result
- Commit and PR links
- Current blockers
- Next recommended task
- Any action requiring owner approval

## 6. Autonomous work policy

Codex may autonomously perform reversible development work, tests, local builds, documentation, and Git operations within this repository.

Codex must stop before:
- Production deployment
- DNS or firewall changes
- SSH changes that may lock out access
- Destructive data operations
- Modifying unrelated project directories or containers
- Credential changes
- Public communications or financial actions

A long-running task must be checkpointed. On restart, Codex should recover from GitHub issues, task records, commits, and project reports rather than relying on process memory.

## 7. Current VPS constraints

The supplied assessment shows approximately 1 vCPU, 961 MiB RAM, 2 GiB swap, and 19 GiB root disk. Use one active Codex execution at a time. Avoid heavyweight always-on services until resource measurements justify them.

The existing `/root/projects/selfbot` directory and its database are unrelated workloads and must remain untouched.

## 8. Definition of done

A task is done only when acceptance criteria pass, tests are recorded, docs are updated, changes are committed, and the user receives an accurate report. A GitHub issue should be closed only when its acceptance criteria are verified.
