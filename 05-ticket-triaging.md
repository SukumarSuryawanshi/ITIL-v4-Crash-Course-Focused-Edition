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