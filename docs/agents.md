# Agent Roles & Responsibilities

> Legacy Foundation — Agent Registry v1.0

---

## Overview

Agents in Legacy Foundation are automated processes that execute bounded, well-defined tasks. Each agent is registered here with its role, responsibilities, memory access, and escalation behavior. Agents are implemented as GitHub Actions steps or external automation scripts triggered by workflows.

---

## Agent Taxonomy

```
Agents
├── Coordinator Agents     — Orchestrate multi-step workflows
├── Task Agents            — Execute specific discrete tasks
└── Monitor Agents         — Observe systems and trigger responses
```

---

## Registered Agents

---

### 1. Platform Reporter Agent

| Field | Value |
|-------|-------|
| **ID** | `platform-reporter` |
| **Type** | Task Agent |
| **Team** | ops-infra |
| **Trigger** | Daily cron (00:00 UTC) |
| **Workflow** | `.github/workflows/daily-report.yml` |

**Responsibilities:**
- Generates a daily platform health and activity report
- Aggregates data from `/memory/episodic/` (last 24 hours)
- Writes structured report to `/reports/YYYY-MM-DD-daily-report.md`
- Logs its own execution to `/memory/episodic/`

**Memory Access:**
- Read: `/memory/episodic/`, `/memory/semantic/`
- Write: `/reports/`, `/memory/episodic/`

**Escalation:** On failure, opens a GitHub issue tagged `ops-infra` and `agent-failure`.

---

### 2. Infrastructure Health Monitor

| Field | Value |
|-------|-------|
| **ID** | `infra-health-monitor` |
| **Type** | Monitor Agent |
| **Team** | ops-infra |
| **Trigger** | Continuous / on-demand |

**Responsibilities:**
- Monitors platform resource utilization and availability
- Writes health snapshots to `/memory/episodic/`
- Triggers alerts when thresholds are breached
- Updates `/memory/semantic/infra-status.md` with current state

**Memory Access:**
- Read: `/memory/semantic/`
- Write: `/memory/episodic/`, `/memory/semantic/`

**Escalation:** Pages on-call ops-infra team member via configured alert channel.

---

### 3. Product Release Coordinator

| Field | Value |
|-------|-------|
| **ID** | `product-release-coordinator` |
| **Type** | Coordinator Agent |
| **Team** | product-factory |
| **Trigger** | Release workflow dispatch |

**Responsibilities:**
- Coordinates multi-step release process for product factory
- Validates release checklist completion before proceeding
- Notifies relevant teams of upcoming releases
- Writes release notes to `/memory/semantic/releases.md`
- Logs release events to `/memory/episodic/`

**Memory Access:**
- Read: `/memory/procedural/release-process.md`, `/memory/semantic/`
- Write: `/memory/episodic/`, `/memory/semantic/`

**Escalation:** Halts release and notifies product-factory lead if any checklist item fails.

---

### 4. Sales Pipeline Reporter

| Field | Value |
|-------|-------|
| **ID** | `sales-pipeline-reporter` |
| **Type** | Task Agent |
| **Team** | sales-growth |
| **Trigger** | Weekly cron (Monday 06:00 UTC) |

**Responsibilities:**
- Generates weekly sales pipeline summary
- Reads pipeline data from configured source
- Writes summary to `/reports/` and `/memory/semantic/`
- Flags deals requiring leadership attention

**Memory Access:**
- Read: `/memory/semantic/sales-context.md`
- Write: `/reports/`, `/memory/episodic/`

**Escalation:** Notifies sales-growth lead if pipeline data is unavailable or stale.

---

### 5. Research Synthesizer Agent

| Field | Value |
|-------|-------|
| **ID** | `research-synthesizer` |
| **Type** | Task Agent |
| **Team** | research-intel |
| **Trigger** | On PR merge to `/teams/research-intel/` |

**Responsibilities:**
- Synthesizes new research findings into the semantic knowledge base
- Extracts key facts and updates `/memory/semantic/knowledge-base.md`
- Tags findings by domain (market, competitor, technology)
- Writes a synthesis summary to `/memory/episodic/`

**Memory Access:**
- Read: `/teams/research-intel/`, `/memory/semantic/`
- Write: `/memory/semantic/`, `/memory/episodic/`

**Escalation:** Flags conflicting knowledge claims for human review.

---

### 6. Workflow Automation Agent

| Field | Value |
|-------|-------|
| **ID** | `workflow-automation-agent` |
| **Type** | Task Agent |
| **Team** | automation-agents |
| **Trigger** | On demand / workflow dispatch |

**Responsibilities:**
- Deploys new workflow templates from `/workflows/` into active processes
- Validates workflow YAML syntax and safety before deployment
- Maintains the agent registry (this document)
- Logs all deployments to `/memory/episodic/`

**Memory Access:**
- Read: `/workflows/`, `/memory/procedural/`
- Write: `/memory/episodic/`

**Escalation:** Requires human approval for any changes to `.github/workflows/`.

---

### 7. Compliance Auditor Agent

| Field | Value |
|-------|-------|
| **ID** | `compliance-auditor` |
| **Type** | Monitor Agent |
| **Team** | compliance-risk |
| **Trigger** | Monthly cron (1st of month, 08:00 UTC) |

**Responsibilities:**
- Scans episodic memory for compliance-flagged events
- Cross-references actions against policy in `/docs/security.md`
- Generates monthly compliance report to `/reports/`
- Updates risk register in `/memory/semantic/risk-register.md`
- Escalates unresolved risks to compliance-risk team lead

**Memory Access:**
- Read: `/memory/episodic/`, `/memory/semantic/`, `/docs/security.md`
- Write: `/reports/`, `/memory/semantic/risk-register.md`, `/memory/episodic/`

**Escalation:** Opens a compliance issue tagged `compliance-review` for any policy breach.

---

## Agent Standards

All agents must comply with the following standards:

1. **Logging** — Write a structured entry to `/memory/episodic/` on every execution (success or failure)
2. **Idempotency** — Running the same agent twice with the same inputs produces the same output without side effects
3. **Scope** — Agents only access directories explicitly listed in their Memory Access section
4. **Secrets** — Never log, echo, or write secrets or tokens to any file
5. **Versioning** — Agent configurations are versioned in git; changes require PR review
6. **Timeouts** — All agent operations have explicit timeouts; agents do not run indefinitely
7. **Human Escalation** — All agents have a defined escalation path for failures and anomalies

---

## Adding a New Agent

1. Define the agent's role, trigger, and memory access
2. Implement the agent as a GitHub Actions workflow or script
3. Add an entry to this file (via PR with automation-agents team review)
4. Add a procedural memory entry in `/memory/procedural/` for the agent's process
5. Test with a dry-run before enabling the production trigger

---

*See also: [Architecture](architecture.md) | [Security](security.md)*
