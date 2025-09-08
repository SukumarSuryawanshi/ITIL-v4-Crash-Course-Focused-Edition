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