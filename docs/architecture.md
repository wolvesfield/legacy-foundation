# System Architecture

> Legacy Foundation — Multi-Team Autonomy Platform

---

## Overview

Legacy Foundation is organized as a modular, event-driven platform where autonomous teams operate independently within a shared infrastructure. The architecture prioritizes reliability, scalability, and observability while minimizing inter-team dependencies.

---

## Core Design Principles

1. **Autonomy with Alignment** — Teams own their domains but share common standards, tooling, and memory systems.
2. **Event-Driven Operations** — Workflows are triggered by events (schedules, webhooks, human actions), not polling.
3. **Memory-Augmented Agents** — All agents read from and write to a shared, structured memory system.
4. **Immutable Audit Logs** — Every agent action is recorded in episodic memory; logs are append-only.
5. **Fail-Safe Defaults** — Agents default to safe states on errors; critical operations require explicit confirmation.

---

## Platform Layers

```
┌─────────────────────────────────────────────────────────┐
│                    HUMAN OVERSIGHT                       │
│        (PR reviews, approval gates, dashboards)          │
└──────────────────────────┬──────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────┐
│               COORDINATOR AGENT LAYER                    │
│   Orchestrates workflows, delegates to task agents,      │
│   manages inter-team communication                       │
└──────┬──────────────────────────────────────┬───────────┘
       │                                      │
┌──────▼──────────┐                ┌──────────▼──────────┐
│  TASK AGENTS    │                │  MONITOR AGENTS     │
│  Execute bounded│                │  Watch systems,     │
│  discrete tasks │                │  trigger alerts     │
└──────┬──────────┘                └──────────┬──────────┘
       │                                      │
┌──────▼──────────────────────────────────────▼──────────┐
│                    MEMORY SYSTEM                         │
│  Episodic │ Semantic │ Procedural                        │
└─────────────────────────┬───────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────┐
│               SHARED INFRASTRUCTURE                      │
│  GitHub Actions │ Artifact Storage │ Reporting Engine    │
└─────────────────────────────────────────────────────────┘
```

---

## Team Domains

Each team operates within a defined domain with clear ownership:

| Team | Domain | Key Interfaces |
|------|--------|----------------|
| ops-infra | Platform infrastructure, reliability, deployments | Memory writes, incident logs |
| product-factory | Product delivery, feature development | Roadmap data, release notes |
| sales-growth | Revenue, partnerships, GTM strategy | CRM data, pipeline reports |
| research-intel | Market data, competitive analysis | Knowledge base, briefings |
| automation-agents | Agent development, tooling, automation | Agent registry, workflow library |
| compliance-risk | Regulatory compliance, risk management | Audit logs, risk registers |

---

## Data Flow

```
Trigger (cron / webhook / manual)
        │
        ▼
Coordinator Agent reads Procedural Memory
        │
        ▼
Task Agents execute (read Semantic Memory as context)
        │
        ▼
Results written to /reports/ and Episodic Memory
        │
        ▼
Monitor Agents validate outputs
        │
        ▼
Human review (if required by policy)
        │
        ▼
Semantic Memory updated with new knowledge
```

---

## Workflow Engine

Workflows are defined as GitHub Actions YAML files in `.github/workflows/`. Each workflow:
- Has a clear trigger (schedule, push, workflow_dispatch)
- Runs in an isolated, reproducible environment
- Writes structured output to `/reports/` with a timestamp
- Updates episodic memory with execution metadata

---

## Reporting

Daily reports are generated automatically via the `daily-report.yml` workflow and stored in `/reports/` with the format:

```
reports/
└── YYYY-MM-DD-daily-report.md
```

Reports include:
- Platform health summary
- Active workflow statuses
- Agent activity metrics
- Open risk items (from compliance-risk)
- Team highlight notes

---

## Scalability Considerations

- **Horizontal scaling** — New teams are added by creating a `/teams/<name>/` directory and registering agents in `/docs/agents.md`
- **Workflow reuse** — SOP templates in `/workflows/` are parameterized for reuse across teams
- **Memory growth** — Episodic logs are rotated monthly; semantic memory is versioned via git history
- **Agent federation** — Future support for external agent APIs via standardized interfaces

---

*See also: [Security](security.md) | [Agents](agents.md)*
