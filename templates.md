## Templates

### A) Incident (INC)

**Opening:**

- Title: Checkout API returns 500 for all customers
- Service/CI: E-Commerce API Gateway
- Impact: High – orders blocked
- Urgency: High
- Priority: P1
- Symptoms: HTTP 500 errors, CloudWatch alarms at 14:03 ET
- Scope: All customers, all regions
- Recent Changes: Feature flag rollout at 17:50 UTC
- Assignment Group: AppOps L2
- Initial Comms: Status page updated at 14:15 ET

**Closing:**

- Resolution: [Rolled back feature flag; service restored]
- Root Cause: [Misconfigured rule]
- Corrective Actions: [Pre-prod validation, staged rollout]
- User Confirmation: [Yes]
- Outage Duration: [35 minutes]

---

### B) Service Request (SR)

**Opening:**

- Title: [Grant read-only DataLake access for Finance]
- Catalog Item: [DataLake Access – ReadOnly]
- Requester: [Jane Doe]
- Needed By: [2025-09-10]
- Approvals: [Manager + Data Owner]
- Fulfillment Steps: [Add to AD group; validate permissions]

**Closing:**
Delivered: [Read-only IAM policy applied]  
Verification: [Requester validated access]  
SLA Met: [Yes]  
Docs Updated: [KBA-456]

---

### C) Change Request (CR)

**Opening:**

Change Type: [Normal – Significant]  
Title: [Upgrade PostgreSQL 13.8 → 14.6 on prod cluster]  
Risk: [Medium-High]  
Impact: [Read-only 5 min; maintenance 30 min]  
Plan: [Step-by-step with rollback]  
Evidence: [Perf test passed; rollback tested]  
Schedule: [2025-09-14 02:00–03:00 ET]  
Comms: [Status page 48h prior]  
Approvals: [DBA Lead, Service Owner, CAB]

**Closing:**  
Outcome: [Successful]  
Duration: [26 min, within window]  
Impact: [Minimal]  
Backout Used: [No]  
Post-Review: [Screenshots attached]

---