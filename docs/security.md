# Security — Access Control & Safe Operations

> Legacy Foundation — Security Policy v1.0

---

## Overview

Security in Legacy Foundation is built on the principle of **least privilege with full transparency**. Every agent, team member, and automated process operates with the minimum permissions required, and all actions are logged immutably.

---

## Access Control

### Role Definitions

| Role | Description | Permissions |
|------|-------------|-------------|
| **Platform Admin** | Full platform control | Read/write all resources, manage roles |
| **Team Lead** | Leads a specific team | Read/write own team directory, read shared docs |
| **Team Member** | Contributor within a team | Read/write own team directory, read docs |
| **Agent (Automated)** | Automated process | Scoped per workflow definition, no admin access |
| **Auditor** | Compliance reviewer | Read-only across all resources |
| **External Collaborator** | Partner or contractor | Read-only, specific directories only |

### Directory Access Matrix

| Directory | Admin | Team Lead | Team Member | Agent | Auditor |
|-----------|-------|-----------|-------------|-------|---------|
| `/teams/<own-team>/` | RW | RW | RW | Scoped | R |
| `/teams/<other-team>/` | RW | R | — | — | R |
| `/docs/` | RW | R | R | R | R |
| `/workflows/` | RW | RW | R | R | R |
| `/memory/episodic/` | RW | R | R | W | R |
| `/memory/semantic/` | RW | RW | R | R | R |
| `/memory/procedural/` | RW | RW | R | R | R |
| `/reports/` | RW | R | R | W | R |
| `/.github/workflows/` | RW | — | — | — | R |

*R = Read, W = Write (append), RW = Read/Write, — = No access*

---

## Authentication & Authorization

### GitHub Repository Access
- Repository visibility: **Private**
- Branch protection on `main`: require PR reviews + status checks
- Required reviewers: minimum 1 peer + 1 team lead for changes to `/docs/`, `/.github/`, or `/memory/semantic/`
- Direct pushes to `main` are disabled

### Secrets Management
- No secrets are stored in repository files
- GitHub Actions secrets are used for all sensitive values (API keys, tokens)
- Secrets are scoped to specific workflows where possible
- Rotate secrets at minimum every 90 days

### Agent Authentication
- Agents use GitHub Actions `GITHUB_TOKEN` with the minimum required scopes
- External API calls use short-lived tokens stored as GitHub Secrets
- Agent identity is logged in every episodic memory entry

---

## Safe Operations

### Human-in-the-Loop Requirements

The following operations **always require human approval** before execution:

- Deletion of any files in `/memory/` or `/reports/`
- Changes to `.github/workflows/` files
- Any workflow that writes to external systems
- Compliance-critical changes (flagged by `compliance-review` label)
- Infrastructure changes in `ops-infra`

### Agent Safety Rules

1. **Read before write** — Agents must read current state before modifying any resource
2. **Dry-run first** — All destructive operations support a dry-run mode; use it
3. **Idempotency** — Agent actions must be safely re-runnable without side effects
4. **Bounded scope** — Agents operate only on explicitly listed directories
5. **Error halting** — On unexpected errors, agents halt and alert; they do not auto-retry destructive operations
6. **No credential leakage** — Agents must never log secrets, tokens, or PII

### Incident Response

1. **Detect** — Monitor agent alerts or manual discovery
2. **Contain** — Immediately revoke affected credentials; pause related workflows
3. **Investigate** — Review episodic memory logs for the affected time window
4. **Remediate** — Apply fixes via PR with compliance-risk team review
5. **Post-Mortem** — Document in `/memory/episodic/` with `[INCIDENT]` prefix
6. **Update Controls** — Improve security controls and update this document

---

## Audit & Compliance

### Audit Logging
- All agent executions are logged in `/memory/episodic/` with: timestamp, agent ID, action taken, outcome
- GitHub Actions run logs are retained for 90 days (GitHub default)
- Critical operations append a structured entry to the episodic log immediately

### Compliance Reviews
- Monthly: compliance-risk team reviews open risk register
- Quarterly: full audit of access control matrix against actual permissions
- Annually: external security review (if applicable)

### Data Retention
| Data Type | Retention Period | Location |
|-----------|-----------------|----------|
| Episodic logs | 12 months rolling | `/memory/episodic/` |
| Daily reports | 6 months rolling | `/reports/` |
| Semantic knowledge | Indefinite (versioned) | `/memory/semantic/` |
| Procedural memory | Indefinite (versioned) | `/memory/procedural/` |
| GitHub Actions logs | 90 days | GitHub (platform-managed) |

---

## Security Contacts

- **Security Incidents**: Tag `compliance-risk` team lead in a private GitHub issue
- **Access Requests**: Submit PR to update this document with justification
- **Vulnerability Reports**: Use GitHub's private vulnerability reporting feature

---

*See also: [Architecture](architecture.md) | [Agents](agents.md)*
