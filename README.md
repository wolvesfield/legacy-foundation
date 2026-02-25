# Legacy Foundation

> **Enterprise-Grade Multi-Team Autonomy Platform**

## Mission

Legacy Foundation is a structured, scalable platform designed to empower independent teams to operate autonomously while maintaining alignment with organizational goals. Each team is equipped with dedicated workflows, AI agents, and shared memory systems that enable rapid decision-making, continuous improvement, and safe operations at scale.

---

## Team Structure

| Team | Directory | Purpose |
|------|-----------|---------|
| **Ops & Infrastructure** | `/teams/ops-infra` | Platform reliability, deployments, cloud infra |
| **Product Factory** | `/teams/product-factory` | Product development, roadmap execution, delivery |
| **Sales & Growth** | `/teams/sales-growth` | Revenue generation, partnerships, market expansion |
| **Research & Intelligence** | `/teams/research-intel` | Market research, data analysis, competitive intel |
| **Automation Agents** | `/teams/automation-agents` | AI agent development, workflow automation, tooling |
| **Compliance & Risk** | `/teams/compliance-risk` | Regulatory compliance, risk assessment, auditing |

---

## Repository Structure

```
legacy-foundation/
â”œâ”€â”€ README.md                  # This file
â”œâ”€â”€ docs/
â”‚   â”œâ”€â”€ architecture.md        # System overview and design principles
â”‚   â”œâ”€â”€ security.md            # Access control and safe operations
â”‚   â””â”€â”€ agents.md              # Agent roles and responsibilities
â”œâ”€â”€ teams/
â”‚   â”œâ”€â”€ ops-infra/             # Ops & Infrastructure team workspace
â”‚   â”œâ”€â”€ product-factory/       # Product Factory team workspace
â”‚   â”œâ”€â”€ sales-growth/          # Sales & Growth team workspace
â”‚   â”œâ”€â”€ research-intel/        # Research & Intelligence team workspace
â”‚   â”œâ”€â”€ automation-agents/     # Automation Agents team workspace
â”‚   â””â”€â”€ compliance-risk/       # Compliance & Risk team workspace
â”œâ”€â”€ workflows/
â”‚   â”œâ”€â”€ task-checklist.md      # Standard task execution checklist
â”‚   â””â”€â”€ sop-template.md        # Standard Operating Procedure template
â”œâ”€â”€ memory/
â”‚   â”œâ”€â”€ episodic/              # Event logs and session records
â”‚   â”œâ”€â”€ semantic/              # Knowledge base and fact stores
â”‚   â””â”€â”€ procedural/            # Step-by-step process memory
â”œâ”€â”€ reports/                   # Auto-generated daily reports (via CI)
â””â”€â”€ .github/
    â””â”€â”€ workflows/
        â””â”€â”€ daily-report.yml   # Cron job: daily platform report
```

---

## How Agents Work

Legacy Foundation uses a layered agent architecture to automate operations across all teams:

### 1. Agent Types
- **Task Agents** â€” Execute specific, bounded tasks (e.g., run a health check, generate a report)
- **Coordinator Agents** â€” Orchestrate multi-step workflows and delegate to task agents
- **Monitor Agents** â€” Continuously observe systems and trigger alerts or remediation
- **Orchestrator (Cipher)** â€” Central coordinator across all teams

### 2. Memory System
Agents share a structured memory system:
- **Episodic Memory** (`/memory/episodic/`) â€” Timestamped logs of events, decisions, and outcomes
- **Semantic Memory** (`/memory/semantic/`) â€” Structured knowledge, facts, and domain understanding
- **Procedural Memory** (`/memory/procedural/`) â€” Repeatable processes and standard operating procedures

### 3. Workflow Execution
1. A trigger (schedule, event, or manual) initiates a workflow
2. The coordinator agent selects the appropriate task agents
3. Agents execute tasks, writing outputs to `/reports/` and updating `/memory/`
4. Results are reviewed by the relevant team and fed back into semantic memory

### 4. Safety & Oversight
- All agent actions are logged in episodic memory
- Sensitive operations require human-in-the-loop approval (see `/docs/security.md`)
- Compliance checks run automatically before and after critical workflows

---

## Getting Started

1. **Explore the docs** â€” Start with [`/docs/architecture.md`](docs/architecture.md) for a system overview
2. **Review your team's workspace** â€” Navigate to your team folder under `/teams/`
3. **Follow the SOP template** â€” Use [`/workflows/sop-template.md`](workflows/sop-template.md) for new initiatives
4. **Check agent responsibilities** â€” See [`/docs/agents.md`](docs/agents.md) for what agents handle

---

## Contributing

- All changes must go through pull requests with at least one peer review
- Follow the SOP template for new workflows
- Update `/memory/semantic/` when adding new organizational knowledge
- Tag compliance-sensitive changes with the `compliance-review` label

---

*Legacy Foundation â€” Built for scale. Designed for autonomy. Ready for the future.*

