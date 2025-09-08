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