# Semantic Memory — Knowledge Base

> **Location:** `/memory/semantic/`
> **Purpose:** Structured, versioned knowledge base containing facts, domain knowledge, and organizational intelligence.
> **Maintenance:** Updated by agents and team members via PR. All updates are versioned in git history.

---

## Platform Knowledge

### Platform Overview
- **Name:** Legacy Foundation
- **Type:** Multi-team autonomy platform
- **Repository:** Private GitHub repository
- **Teams:** ops-infra, product-factory, sales-growth, research-intel, automation-agents, compliance-risk
- **Automation:** GitHub Actions cron workflows
- **Memory System:** Episodic, Semantic, Procedural (this directory)

### Technology Stack
- **Workflow Engine:** GitHub Actions
- **Version Control:** Git / GitHub (private)
- **Documentation Format:** Markdown
- **Report Storage:** `/reports/` (git-tracked, auto-generated)

---

## Team Knowledge

### ops-infra
- Primary responsibility: Platform reliability and cloud infrastructure
- SLO targets: 99.9% availability, < 30 min MTTR
- On-call: Rotating weekly, team lead as backup

### product-factory
- Primary responsibility: Product feature delivery
- Delivery cadence: Bi-weekly releases minimum
- Quality gate: QA sign-off required before any release

### sales-growth
- Primary responsibility: Revenue growth and partnerships
- Pipeline tool: Configured separately (credentials in GitHub Secrets)
- Reporting cadence: Weekly pipeline summary (automated)

### research-intel
- Primary responsibility: Market and competitive intelligence
- Output format: Reports in `/teams/research-intel/reports/`, synthesized to semantic memory
- Tagging taxonomy: `market`, `competitor`, `technology`, `customer`

### automation-agents
- Primary responsibility: Agent and workflow development
- Deployment process: Dry-run → PR review → Production
- Registry: `/docs/agents.md`

### compliance-risk
- Primary responsibility: Regulatory compliance and risk management
- Risk register: `/memory/semantic/risk-register.md`
- Audit cycle: Monthly automated + quarterly manual

---

## Domain Knowledge

### Agent Architecture Patterns
- **Task Agents:** Bounded, single-purpose, idempotent
- **Coordinator Agents:** Stateful orchestrators; read procedural memory to drive multi-step processes
- **Monitor Agents:** Event-triggered; write to episodic memory; escalate via defined channels

### Memory System Design
- **Episodic:** Append-only event log; never edited after write
- **Semantic:** Versioned facts and knowledge; updated via PR
- **Procedural:** Step-by-step processes; source of truth for agent execution plans

### Security Model
- Principle: Least privilege
- Authentication: GitHub repository permissions + Actions GITHUB_TOKEN
- Secrets: GitHub Secrets only; never in files
- Audit: All agent actions logged in episodic memory

---

## Risk Register

> See `/memory/semantic/risk-register.md` for the full risk register.

| ID | Risk | Level | Owner | Status |
|----|------|-------|-------|--------|
| R-001 | Unreviewed agent deployment | Medium | automation-agents | Mitigated (PR process) |
| R-002 | Secret exposure in logs | High | ops-infra | Mitigated (agent standards) |
| R-003 | Knowledge base staleness | Low | research-intel | Monitoring |

---

*Last updated: 2026-02-01 | Updated by: platform-admin*
