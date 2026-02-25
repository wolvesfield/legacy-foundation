# Procedural Memory — Process Library

> **Location:** `/memory/procedural/`
> **Purpose:** Documented, reusable processes and procedures that agents and team members follow when executing standard operations.
> **Maintenance:** Updated via PR. Agents read this directory to understand how to execute known processes.

---

## Process Index

| Process ID | Title | Owner | Trigger |
|-----------|-------|-------|---------|
| PROC-001 | Daily Platform Report | ops-infra / platform-reporter | Cron daily 00:00 UTC |
| PROC-002 | Onboarding a New Team Member | platform-admin | Manual |
| PROC-003 | Deploying a New Agent | automation-agents | Manual / PR merge |
| PROC-004 | Incident Response | ops-infra | Alert trigger |
| PROC-005 | Monthly Compliance Audit | compliance-risk / compliance-auditor | Cron monthly |

---

## PROC-001: Daily Platform Report

**Trigger:** Cron schedule, daily at 00:00 UTC
**Agent:** `platform-reporter`
**Output:** `/reports/YYYY-MM-DD-daily-report.md`

### Steps
1. Read last 24 hours of entries from `/memory/episodic/log.md`
2. Read current risk register from `/memory/semantic/knowledge-base.md`
3. Collect workflow run statuses from GitHub Actions API
4. Compile report with sections: Health Summary, Workflow Status, Agent Activity, Risk Items, Team Highlights
5. Write report to `/reports/YYYY-MM-DD-daily-report.md`
6. Append execution entry to `/memory/episodic/log.md`
7. Commit changes with message: `chore: daily report YYYY-MM-DD`

### Error Handling
- If episodic log is unavailable: report with warning, do not fail
- If GitHub API is unavailable: report workflow status as "unavailable", do not fail
- On any unhandled error: open GitHub issue tagged `ops-infra` + `agent-failure`

---

## PROC-002: Onboarding a New Team Member

**Trigger:** Manual (team lead initiates)
**Actor:** Platform admin + team lead
**Output:** New member has appropriate repository access

### Steps
1. Team lead submits onboarding request (GitHub issue or message to platform admin)
2. Platform admin adds member to GitHub repository with Team Member role
3. Team lead shares team workspace README: `/teams/<team>/README.md`
4. New member reads: `README.md`, `/docs/architecture.md`, `/docs/security.md`
5. New member reviews their team's `/teams/<team>/README.md`
6. Platform admin logs onboarding in `/memory/episodic/log.md`
7. Team lead assigns first task using task checklist

---

## PROC-003: Deploying a New Agent

**Trigger:** Manual (automation-agents team) or PR merge to agent spec
**Actor:** automation-agents team
**Output:** Agent registered, tested, and running in production

### Steps
1. Create agent spec in `/teams/automation-agents/agent-specs/<agent-id>.md`
2. Implement agent as GitHub Actions workflow or script
3. Add agent entry to `/docs/agents.md` via PR
4. Run agent in dry-run mode and verify output
5. Request review from automation-agents lead
6. Merge PR after approval
7. Enable production trigger
8. Monitor first 3 production runs
9. Log deployment in `/memory/episodic/log.md`

---

## PROC-004: Incident Response

**Trigger:** Alert from monitor agent or manual discovery
**Actor:** ops-infra on-call
**Output:** Incident resolved and post-mortem documented

### Steps
1. **Detect & Acknowledge** — Acknowledge alert within 5 minutes
2. **Assess Severity** — Determine impact level (Critical / High / Medium / Low)
3. **Contain** — Take immediate action to prevent escalation (e.g., pause workflows, revoke credentials)
4. **Communicate** — Notify relevant stakeholders based on severity level
5. **Investigate** — Review episodic memory logs for root cause
6. **Remediate** — Apply fix via PR with ops-infra lead review
7. **Verify** — Confirm resolution; monitor for recurrence
8. **Post-Mortem** — Document in `/memory/episodic/log.md` with `[INCIDENT]` prefix
9. **Update Controls** — Improve relevant SOPs or security controls

---

## PROC-005: Monthly Compliance Audit

**Trigger:** Cron schedule, 1st of month at 08:00 UTC
**Agent:** `compliance-auditor`
**Output:** `/reports/YYYY-MM-compliance-report.md`

### Steps
1. Read all episodic log entries from the previous month
2. Cross-reference actions against policies in `/docs/security.md`
3. Check risk register for unresolved items past due date
4. Verify access control matrix is current
5. Compile compliance report with: Findings, Policy Adherence Score, Open Risks, Recommendations
6. Write report to `/reports/YYYY-MM-compliance-report.md`
7. Update risk register in `/memory/semantic/knowledge-base.md`
8. Open GitHub issue for any compliance findings requiring action
9. Append execution entry to `/memory/episodic/log.md`

---

*Process Library v1.0 | Maintained by: automation-agents*
