# Compliance & Risk Team

> **Team:** `compliance-risk`
> **Mission:** Ensure the platform operates within legal, regulatory, and ethical boundaries while managing organizational risk.

---

## Responsibilities

- Regulatory compliance monitoring and reporting
- Risk identification, assessment, and mitigation
- Policy development and enforcement
- Audit preparation and management
- Data governance and privacy oversight
- Security incident escalation and post-mortem review

---

## Team Workspace

```
teams/compliance-risk/
├── README.md              # This file
├── policies/              # Compliance policies and standards
├── risk-register/         # Active and historical risk register
└── audits/                # Audit records and findings
```

---

## Key Contacts

| Role | Responsibility |
|------|---------------|
| Compliance Lead | Policy ownership and regulatory relationships |
| Risk Manager | Risk register maintenance and escalation |
| Data Privacy Officer | Data governance and privacy compliance |

---

## Agent Coverage

- **Compliance Auditor Agent** (`compliance-auditor`) — Monthly automated compliance scans

---

## Compliance Framework

All platform operations are assessed against the following:
- **Data Handling** — Minimum data collection, clear retention policies
- **Access Control** — Least privilege, documented in `/docs/security.md`
- **Audit Trails** — All actions logged in `/memory/episodic/`
- **Change Management** — All changes via PR with required reviews
- **Incident Response** — Defined process in `/docs/security.md`

---

## Risk Levels

| Level | Response Time | Escalation |
|-------|--------------|------------|
| Critical | Immediate (< 1 hour) | CEO + all team leads |
| High | Same day | Compliance lead + relevant team lead |
| Medium | Within 3 days | Compliance lead |
| Low | Within 2 weeks | Risk manager review |

---

*Risk register is maintained in `/memory/semantic/risk-register.md` and updated monthly.*
