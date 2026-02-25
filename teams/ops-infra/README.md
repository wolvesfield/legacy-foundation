# Ops & Infrastructure Team

> **Team:** `ops-infra`
> **Mission:** Ensure platform reliability, manage cloud infrastructure, and own deployment pipelines.

---

## Responsibilities

- Cloud infrastructure provisioning and management
- CI/CD pipeline ownership and optimization
- Platform monitoring, alerting, and incident response
- Security patching and dependency updates
- Capacity planning and cost optimization
- On-call rotation management

---

## Team Workspace

```
teams/ops-infra/
├── README.md              # This file
├── runbooks/              # Operational runbooks for common scenarios
├── infrastructure/        # Infrastructure-as-code definitions
└── incidents/             # Post-mortem and incident documentation
```

---

## Key Contacts

| Role | Responsibility |
|------|---------------|
| Team Lead | Final decision on infrastructure changes |
| On-Call Engineer | First responder for alerts |
| Platform Architect | Technical design authority |

---

## Agent Coverage

- **Platform Reporter Agent** (`platform-reporter`) — Daily health reports
- **Infrastructure Health Monitor** (`infra-health-monitor`) — Continuous monitoring

---

## SLOs

| Metric | Target |
|--------|--------|
| Platform availability | 99.9% |
| Deployment success rate | 99% |
| Mean time to recovery (MTTR) | < 30 minutes |
| Alert response time | < 5 minutes |

---

*See the [SOP template](../../workflows/sop-template.md) for new runbooks.*
