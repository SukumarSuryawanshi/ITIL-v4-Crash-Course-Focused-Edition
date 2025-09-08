# 🚀 ITIL v4 Crash Course – Focused Edition

## Shared Foundations

---

## 1) Incident Management

**Definition:** Restore normal service operation as quickly as possible to minimize impact.

### What is an incident?

 an unplanned interruption to a service, a reduction in service quality, or a component (CI) failure/event that has not yet impacted users but risks doing so (e.g., outage, severe latency, failed batch job, capacity threshold alarm needing action)


 
### Priority Matrix (Impact × Urgency)

| Impact \ Urgency | High | Medium | Low |
|------------------|------|--------|-----|
| **High** (Service down, revenue at risk) | **P1** | P2 | P3 |
| **Medium** (Degraded service, workaround exists) | P2 | **P3** | P4 |
| **Low** (Minor inconvenience) | P3 | P4 | **P5** |

**Example SLA targets:**
- **P1**: Response 15 min, Comms every 30 min, Restore ≤ 4h  
- **P2**: Response 1h, Comms every 2h, Restore ≤ 8h  
- **P3**: Response 4h, Restore ≤ 2 business days  
- **P4/P5**: Planned effort, usually 3–10 days  


**Workflow:**
1. Detect & Log (monitoring alert or user report)  
2. Triage → categorize, priority, CI, assignment  
3. Contain / Workaround  
4. Escalate / Swarm (L2/L3 teams)  
5. Communicate regularly  
6. Resolve / Restore  
7. Close with confirmation  
8. Post-Incident Review (for P1/P2)

**Real scenario:**  
Checkout API outage → rollback last feature flag → restored in 35 min.

**Manager’s Responsibilities:**
- Drive **major incident bridges**  
- Ensure **status updates** & SLA adherence  
- Maintain **incident quality** (categorization, closure notes)  
- Trigger **Problem records**  
- Track KPIs (MTTA, MTTR, SLA hit rate, FCR)

---

## 2) Problem Management

### What is a Problem Ticket?

A Problem ticket (Problem record) is a work item raised to investigate and eliminate the underlying cause(s) of one or more incidents, or to address a significant latent risk discovered proactively (trend, monitoring, major incident review). It captures: pattern/symptoms, impact, affected services/CIs, linked incidents, analysis tasks, root cause (once known), Known Error, workaround, and required corrective changes.

Raise a Problem when:
- Recurrent or related incidents (pattern emerging)
- Major (P1/P2) incident requiring RCA
- Significant risk or latent error detected (capacity, vulnerability, instability)
- High incident volume category needing reduction

Goal: reduce repeat incidents and improve service stability via documented root cause removal and knowledge reuse.



**Definition:** Identify and manage root causes of incidents to reduce recurrence.

**Workflow:**
1. Detect recurring issues  
2. Log & prioritize Problem record  
3. Root Cause Analysis (RCA)  
4. Document **Known Error** + **Workaround**  
5. Solution (may need CR/Release)  
6. Verify & close  

**Real scenario:**  
Recurring VPN drops → RCA reveals firewall memory leak → fix via firmware upgrade → no more VPN incidents.

**Manager’s Responsibilities:**
- Run **Problem Review Board**  
- Track **RCA quality & closure**  
- Maintain **Known Error DB (KEDB)**  
- Drive corrective CRs  
- KPIs: problem resolution time, reduction in repeat incidents

---

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

## 4) Release Management

### What is a Release?  
A Release is a versioned, deployable bundle of one or more approved change records (CRs) plus their required artifacts (code, infrastructure as code, configs, schema migrations, feature flags, scripts) moved together through environments to deliver defined business or technical value with controlled risk.

A Release Record (if your toolset supports it) typically captures:  
- Identifier / version & objective  
- Scope (services / components / platforms)  
- Included Change IDs / dependencies  
- Environments path (Dev → Test → Staging → Prod)  
- Deployment strategy (big bang, phased %, canary, blue/green, feature flag, dark launch)  
- Cutover plan & timing (who does what, when)  
- Validation & monitoring plan (KPIs, alarms, rollback triggers)  
- Rollback / remediation plan (fast, tested)  
- Early Life Support (ownership window)  
- Communications (stakeholders, status page, release notes)  

Lifecycle:  
1. Plan (select contents, align windows, risk assess)  
2. Assemble & Integrate (package, version, dependency checks)  
3. Verify (automated tests, security, performance, rollback test)  
4. Deploy (per strategy)  
5. Early Life Support (heightened monitoring, rapid fix path)  
6. Close (document outcomes, metrics, lessons, link incidents/problems)  

Create a distinct Release when:  
- Multiple coordinated changes must land together (shared schema, contract)  
- Platform / infrastructure upgrade spanning services  
- Fixed cadence train (e.g., monthly business bundle)  
- High-impact feature launch with staged exposure  

Usually NOT needed for:  
- Continuous small independently deployable changes (each CR flows alone)  
- Single emergency hotfix (handled as Emergency Change)  

Quality Gates (examples):  
- All CRs approved; tests ≥ threshold  
- Security / compliance scans clean or accepted  
- Rollback executed successfully in staging  
- Monitoring & alert thresholds defined pre-go  
- Release notes drafted and owners acknowledged  

Common Deployment Strategies (choose deliberately):  
- Phased % rollout (10/25/50/100)  
- Canary (small slice + auto-metrics guardrails)  
- Blue/Green (parallel prod env swap)  
- Feature Flag (decouple code deploy from feature exposure)  

Example: Release 2025.09.R1 bundles 8 microservice updates + payment DB migration behind a feature flag; deployed via canary 10% → 30% → 100% with automatic rollback if error rate >2% or p99 latency +25%. No rollback triggered; Early Life Support 24h; success logged.  

**Definition:** Plan, schedule, and control movement of releases into live environments.

**Essentials:**
- Release cadence & policy  
- Gate criteria (tests, security, rollback readiness)  
- Go/No-Go meetings  
- Release notes & comms

**Real scenario:**  
Monthly release train → tests passed → staged rollout (10%/50%/100%) → monitoring confirms stability.

**Manager’s Responsibilities:**
- Coordinate **release calendar**  
- Chair **Go/No-Go**  
- Ensure readiness checks  
- Track release success rate, rollback %, change-caused incidents

---

## 5) Ticket Triaging

**Definition:** Ticket triaging is the rapid, consistent evaluation of new tickets (incidents, service requests, alerts) to classify, prioritize, assign, and trigger the correct next action with minimal delay.

**Objectives:**
- Confirm: Is it an Incident or a Service Request?
- Determine impact (who / how many / business effect) and urgency (time sensitivity)
- Set priority using the Impact × Urgency matrix
- Capture clear, minimal reproducible info (symptoms, scope, recent change, timestamp)
- Route to the correct assignment group or initiate a P1/P2 swarm
- Identify duplicates, link related incidents, or raise a Problem if pattern emerges
- Apply any known workaround (from KEDB / KB) to accelerate restoration

**Minimum Data to Record Fast:**
- What is broken / requested?
- Who is affected? (users, service, region)
- When did it start? Ongoing vs historical
- What changed? (deploy, config, infra event)
- Error evidence (codes, logs, screenshot, alert ID)
- Interim workaround tried (yes/no)

**Good Triaging Signals:**
- Priority justified (impact + urgency stated)
- Clear ownership (no “unassigned” aging tickets)
- Linked to CI / service for trend analysis
- Known Error or KB suggested when applicable

**Anti-Patterns:**
- Over-gathering detail before assigning
- Auto-escalating everything to senior teams
- Ignoring recent change history
- Leaving ambiguous titles (“System not working”)

**Outcome:** A ticket exits triage only when it is: correctly typed, prioritized, assigned (or swarmed), and has enough context for the resolver to act without chasing basics.

**Techniques:**
- Use **triage script** (impact, scope, last change, workaround tried)  
- Apply **Impact × Urgency matrix**  
- Assign to right queue or **swarm** for P1/P2  
- Use KB & KEDB to improve first-contact resolution  
- Automate routine fixes

**Task Types:**
- **Incident:** outages, errors, degradation, alerts  
- **Service Request:** access, provisioning, info/how-to, standard changes

---

## 6) Reducing Incidents & Improving Service Requests

**Reduce incidents:**
- Improve change quality (tests, canary, rollback discipline)  
- Monitoring with actionable alerts  
- Problem mgmt → RCA → KE → CR  
- Auto-remediation & runbooks  
- Knowledge articles for frontline

**Improve service requests:**
- Clear service catalog with SLAs  
- Smart request forms (mandatory fields)  
- Automate fulfillment of standard requests  
- Post-fulfillment CSAT surveys  
- Measure **rework/returns** rate

---

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

## Manager Checklists (Daily)

**Incident Manager**
- Review last 24h incidents  
- Drive PIRs for P1/P2  
- Track SLA breaches  
- Ensure comms cadence  
- Top 3 categories → feed Problem Mgmt  

**Problem Manager**
- Track open RCA  
- Ensure Known Errors in KB  
- Link CRs for corrective actions  
- Trend analysis for reduction  

**Change Manager**
- Monitor change calendar  
- Approvals complete  
- Run CAB & document outcomes  
- Emergency CR retrospective  

**Release Manager**
- Check readiness of releases  
- Run Go/No-Go  
- Monitor post-release health  
- Publish release notes

---

## CAB Agenda (Sample)
1. Review upcoming high-risk changes  
2. Conflict/blackout window check  
3. Risk & rollback assessment  
4. Business timing review  
5. Decision & conditions  
6. Review emergency changes since last CAB  

---

## Quick Decision Flows

**Incident vs Service Request**


Is something broken now?
→ Yes → Incident
→ No → Request (access/provisioning/info)



**Change Type**


Is change low risk & pre-approved? → Standard
Is it urgent to fix a P1? → Emergency (eCAB)
Else → Normal (Minor or Significant)



---

## Key KPIs

- **Incidents:** MTTR, SLA %, FCR, incidents/change  
- **Problems:** time-to-KE, % repeat reduction  
- **Changes:** success rate, CFR, emergency %, lead time  
- **Releases:** release success, rollback %, post-release incidents  
