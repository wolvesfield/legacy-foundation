# Automation Agents Team

> **Team:** `automation-agents`
> **Mission:** Build, maintain, and improve the AI agents and automation workflows that power the Legacy Foundation platform.

---

## Responsibilities

- Agent design, development, and testing
- Workflow automation and optimization
- Agent registry maintenance (`/docs/agents.md`)
- Tooling and internal developer experience
- Agent performance monitoring and tuning
- Automation platform roadmap

---

## Team Workspace

```
teams/automation-agents/
├── README.md              # This file
├── agent-specs/           # Specifications for each agent
├── tooling/               # Internal tools and utilities
└── experiments/           # Agent experiments and prototypes
```

---

## Key Contacts

| Role | Responsibility |
|------|---------------|
| Automation Lead | Agent strategy and platform direction |
| Agent Engineer | Agent implementation and testing |
| Platform Engineer | Infrastructure for automation systems |

---

## Agent Coverage

- **Workflow Automation Agent** (`workflow-automation-agent`) — Deploys and manages workflows

---

## Development Standards

- All agents must be registered in `/docs/agents.md` before production use
- Agents are tested with dry-run mode before live deployment
- Every agent must have defined escalation paths
- Agent changes require code review from at least one team member
- Agents are versioned with the repository

---

## Platform Metrics

| Metric | Target |
|--------|--------|
| Agent uptime | > 99.5% |
| Workflow success rate | > 98% |
| Mean time to deploy new agent | < 3 days |
| Automation coverage | Growing week-over-week |

---

*New agent proposals start with a spec in `agent-specs/` and a PR for `/docs/agents.md`.*
