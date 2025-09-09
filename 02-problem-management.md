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

