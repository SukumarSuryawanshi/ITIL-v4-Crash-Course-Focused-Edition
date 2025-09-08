## 3) Change Enablement (Change Management)

### What is a Change Record?

A Change Record (CR) is the formal, trackable artifact used to assess, authorize, schedule, implement, and review a change to a production (or production-bound) environment.

It captures:
- Purpose / business justification
- Scope (services / CIs affected)
- Type (Standard, Normal – Minor/Significant, Emergency)
- Risk & impact assessment
- Implementation plan (step-by-step)
- Validation / test evidence
- Backout (rollback) plan
- Schedule / window & dependencies
- Required approvals (owners, CAB, eCAB)
- Deployment method (manual, automated pipeline)
- Success criteria & monitoring plan
- Post-implementation results (actual impact, issues, lessons)

Lifecycle:
1. Draft (submitted)
2. Assessment (risk, impact, conflicts)
3. Authorization (approvals / CAB)
4. Implementation (execution + monitoring)
5. Review & Close (outcome, metrics, linkage to incidents/problems)

When to raise:
- Any non-trivial change to code, infrastructure, configuration, security posture, data structures, platform versions, or scheduled jobs that could affect live service
- Emergency fixes for active/high-impact incidents (flagged Emergency)
- Problem-driven corrective actions (linked to Problem Record)
- Release packaging (each deploy may reference multiple CRs, or a Release groups them)

Not a Change Record:
- Routine pre-approved Standard actions (unless outside catalog)
- Break/fix execution inside an active incident (unless follow-up remediation is needed)

Good practice:
- Single clear objective
- Measurable success criteria
- Tested rollback
- No approval gaps before window
- Post-change metrics reviewed (detect silent failures)

Key quality checks:
- Risk coherent with impact description
- Rollback independent, fast, and validated
- No blackout / conflict on calendar
- Monitoring in place before execution
- Linked incidents/problems closed or updated after completion
- CFR (Change Failure Rate) impact recorded if issues occurred

**Definition:** Ensure changes are assessed, authorized, and implemented with minimal risk.

**Types of Change:**
- **Standard** – low risk, pre-approved (e.g., adding user to AD group)  
- **Normal** – needs assessment & approval  
    - Minor (low risk, quick approval)  
    - Significant/Major (requires CAB review)  
- **Emergency** – urgent fix for P1 → eCAB approval

**Example CR SLAs:**

| Type | Decision SLA | Lead Time | Approval |
|------|--------------|-----------|----------|
| Standard | Pre-approved | Catalog-based | Custodian / Automation |
| Normal – Minor | ≤ 2 days | ≥ 2 days | Change Manager + Owner |
| Normal – Significant | ≤ 5 days | ≥ 5–10 days | CAB |
| Emergency | ≤ 60 min | Immediate | eCAB |

**Manager’s Responsibilities:**
- Own **Change calendar** & blackout policy  
- Run **CAB meetings**  
- Track **success rate & CFR (Change Failure Rate)**  
- Ensure **rollback plans** exist  
- KPIs: success %, emergency %, lead time

---