## 1) Incident Management

### Index

- [Definition](#definition)
- [What is an Incident?](#what-is-an-incident)
- [What is an Outage](#what-is-an-outage)
- [Service Degradation](#what-is-service-degradation-impact-clarification)
- [Priority Matrix](#priority-matrix-impact--urgency)
- [Workflow](#workflow)
- [Manager’s Responsibilities](#managers-responsibilities)

### Definition

Restore normal service operation as quickly as possible to minimize impact.

### What is an incident?

An unplanned interruption to a service, a reduction in service quality, or a component (CI) failure/event that has or hasn't yet impacted users.

### What is an Outage
A complete or near-complete loss of a production service or critical user journey so the intended business function cannot be performed.

Typical signals:

- All or majority of requests failing (e.g., sustained 5xx spike, health checks red)
- Zero successful transactions over a defined interval
- Critical dependency unreachable (DB not writable, auth service down)
- Core batch/job pipeline halted with business impact

Examples:

1. Checkout API returning 500s across regions
2. Identity service unreachable (no logins)
3. Payment processor queue consumers all stalled
4. Primary database down and failover not succeeding

Usually classified P1 (broad/user-facing) or P2 (contained scope).  
First actions: declare major incident, open bridge, stop risky changes, identify last change, rollback / failover / disable feature flag, restore service before root cause deep-dive.

### What is "Service Degradation" (Impact Clarification)
A service is degraded when it is partially functional but not meeting normal performance, reliability, correctness, or capacity expectations. Users can still perform the core journey, but with friction, delay, reduced quality, or limited scope.

Key attributes:

- Partial failure (subset of endpoints / regions / features)
- Elevated error rate (success path remains)
- Performance regression (latency above SLO)
- Capacity constraint (throttling, backlog growth)
- Functional impairment (non-blocking step broken)

Examples:

- 10–30% of login attempts failing in one AZ
- Image uploads intermittently timing out
- Increased payment retries; eventual success
- Search slower but still returns results
- Data freshness lag (dashboards 30 min behind)

Impact vs outage:

- Outage: Business function cannot complete (hard stop)
- Degradation: Function completes with reduced quality (soft failure)

Typical priority mapping:

- Broad, revenue-impacting, trending worse → P2
- Localized, short-lived, workaround exists → P3
- Minor / cosmetic / low traffic → P4/P5

Rapid severity assessment:

1. User-facing?
2. % traffic / feature surface affected
3. Revenue / regulatory / reputation risk
4. SLO/SLA breach likelihood window
5. Workaround or retry success?

Responder actions:

- Quantify blast radius (requests/min, error % trend)
- Check last deploy / infra / flags
- Compare SLO dashboards (latency, error budget burn)
- Escalate if trending to outage
- Apply reversible mitigations first (rollback, fail open, shed non-critical load)
- Communicate clearly: degraded vs outage

Metrics to track:

- Error budget burn rate
- % impacted sessions
- Retry success delta
- Latency shift (p50/p95/p99)
- Queue backlog age

When to open a Problem record:

- Repeat pattern
- Hidden SPOF exposed
- Error budget overspend
- Manual mitigation required

Comms template snippet:
Current state: Service degraded (not full outage). Impact: ~18% checkout retries; success on retry (<2 min). Mitigation: Rolling back payment adapter update. Next update: 20 min or sooner.

In short: Degradation = partial function with measurable impairment; treat seriously if escalation risk or SLO at risk.

### Priority Matrix (Impact × Urgency)

| Impact \ Urgency | High | Medium | Low |
|------------------|------|--------|-----|
| High (Service down, revenue at risk) | P1 | P2 | P3 |
| Medium (Degraded, workaround exists) | P2 | P3 | P4 |
| Low (Minor inconvenience) | P3 | P4 | P5 |

Example SLA targets:

- P1: Response 15 min; comms every 30 min; restore ≤ 4h
- P2: Response 1h; comms every 2h; restore ≤ 8h
- P3: Response 4h; restore ≤ 2 business days
- P4/P5: Planned effort (3–10 days)

### Workflow

1. Detect & log  
2. Triage (categorize, priority, CI, assign)  
3. Contain / workaround  
4. Escalate / swarm (L2/L3)  
5. Communicate  
6. Resolve / restore  
7. Close (confirmation)  
8. Post-incident review (P1/P2)

Real scenario: Checkout API outage → rollback last feature flag → restored in 35 min.

### Manager’s Responsibilities

- Run major incident bridges
- Ensure timely status updates & SLA adherence
- Maintain incident data quality
- Trigger Problem records
- Track KPIs (MTTA, MTTR, SLA hit rate, FCR)