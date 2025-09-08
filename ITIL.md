# 🚀 ITIL v4 Crash Course – Focused Edition
**Author Information**  
- Name: [Sukumar Suryawanshi]  
- Role: IT Service Management Lead  
- Contact: [email or Teams handle]  
- Version: 1.0  
- Last Updated: 2025-09-08  
- Source Control Tag: itil-v4-focused-v1.0  
- License / Usage: Internal enablement guide (adapt before external sharing)  
- Attribution Note: Condensed for rapid onboarding; align with your org’s governance, security, and compliance standards before adoption.  
- Improvement Log: Track edits (process deltas, KPI definitions, tooling changes) in CHANGELOG.md  

> Update Last Updated + Version whenever substantive process, KPI, or template changes are made.  
## Index
- [Shared Foundations](shared-foundations.md)

- [1) Incident Management](01-incident-management.md)
    - [What is an incident?](01-incident-management.md#what-is-an-incident)
    - [Priority Matrix (Impact × Urgency)](01-incident-management.md#priority-matrix-impact--urgency)
    - [Workflow](01-incident-management.md#workflow)
    - [Real scenario](01-incident-management.md#real-scenario)
    - [Manager’s Responsibilities](01-incident-management.md#managers-responsibilities)

- [2) Problem Management](02-problem-management.md)
    - [What is a Problem Ticket?](02-problem-management.md#what-is-a-problem-ticket)
    - [Workflow](02-problem-management.md#workflow)
    - [Real scenario](02-problem-management.md#real-scenario)
    - [Manager’s Responsibilities](02-problem-management.md#managers-responsibilities)

- [3) Change Enablement (Change Management)](03-change-enablement.md)
    - [What is a Change Record?](03-change-enablement.md#what-is-a-change-record)
    - [Types of Change](03-change-enablement.md#types-of-change)
    - [Example CR SLAs](03-change-enablement.md#example-cr-slas)
    - [Manager’s Responsibilities](03-change-enablement.md#managers-responsibilities)

- [4) Release Management](04-release-management.md)
    - [What is a Release?](04-release-management.md#what-is-a-release)
    - [Essentials](04-release-management.md#essentials)
    - [Real scenario](04-release-management.md#real-scenario)
    - [Manager’s Responsibilities](04-release-management.md#managers-responsibilities)

- [5) Ticket Triaging](05-ticket-triaging.md)
    - [Objectives](05-ticket-triaging.md#objectives)
    - [Minimum Data to Record Fast](05-ticket-triaging.md#minimum-data-to-record-fast)
    - [Good Triaging Signals](05-ticket-triaging.md#good-triaging-signals)
    - [Anti-Patterns](05-ticket-triaging.md#anti-patterns)
    - [Outcome](05-ticket-triaging.md#outcome)
    - [Techniques](05-ticket-triaging.md#techniques)
    - [Task Types](05-ticket-triaging.md#task-types)

- [6) Reducing Incidents & Improving Service Requests](06-reduction-and-requests.md)
    - [Reduce incidents](06-reduction-and-requests.md#reduce-incidents)
    - [Improve service requests](06-reduction-and-requests.md#improve-service-requests)

- [Templates](templates.md)
    - [Incident (INC)](templates.md#a-incident-inc)
    - [Service Request (SR)](templates.md#b-service-request-sr)
    - [Change Request (CR)](templates.md#c-change-request-cr)

- [Manager Checklists (Daily)](manager-checklists.md)
- [CAB Agenda (Sample)](cab-agenda.md)
- [Quick Decision Flows](quick-decision-flows.md)
    - [Incident vs Service Request](quick-decision-flows.md#incident-vs-service-request)
    - [Change Type](quick-decision-flows.md#change-type)
- [Key KPIs](key-kpis.md)

## Shared Foundations




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
