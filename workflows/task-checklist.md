# Task Execution Checklist

> Standard checklist for task execution across all Legacy Foundation teams.
> Copy this checklist into your issue, PR, or workflow documentation before starting any non-trivial task.

---

## Pre-Task Checklist

- [ ] Task has a clear, documented objective
- [ ] Acceptance criteria are defined and agreed upon
- [ ] Owner is assigned
- [ ] Dependencies are identified and available
- [ ] Relevant procedural memory has been reviewed (`/memory/procedural/`)
- [ ] Risk level has been assessed (Low / Medium / High / Critical)
- [ ] Compliance requirements have been checked (if applicable)
- [ ] Stakeholders have been notified

---

## During Execution

- [ ] Working in a dedicated branch or isolated environment
- [ ] Progress is being logged (in PR, issue, or episodic memory)
- [ ] Blockers are escalated promptly to team lead
- [ ] Scope creep is being avoided — changes outside original scope go to a new task
- [ ] Secrets and credentials are handled securely (not in code or logs)

---

## Code / Artifact Review

- [ ] Work product meets acceptance criteria
- [ ] Relevant tests have been written or updated
- [ ] Documentation has been updated (if applicable)
- [ ] Memory updates prepared (`/memory/semantic/` or `/memory/procedural/` if needed)
- [ ] Peer review requested

---

## Post-Task Checklist

- [ ] Changes merged / deployed
- [ ] Outcome logged in `/memory/episodic/` (for significant tasks)
- [ ] Knowledge base updated in `/memory/semantic/` (if new facts discovered)
- [ ] Stakeholders notified of completion
- [ ] Retrospective notes added (if applicable)
- [ ] Follow-up tasks created for any identified improvements
- [ ] Task marked complete in tracking system

---

## Escalation Triggers

Escalate immediately if any of the following occur:
- Unexpected data loss or corruption
- Security or compliance incident
- External dependency failure blocking the task
- Scope has expanded beyond 50% of original estimate
- Any doubt about whether to proceed with an action

---

*Template version: 1.0 | Maintained by: automation-agents*
