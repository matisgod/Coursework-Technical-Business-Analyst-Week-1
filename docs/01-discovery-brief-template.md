# Legacy-Trust Bank

Legacy-Trust Bank is looking to update its debt recovery system using the Smart-Recovery Initiative. Currently, the debt recovery system has not been modernised in 20 years, with over 100,000 accounts being managed by over 50 agents working across several spreadsheets, email trails and agent/team-specific workarounds. This brief aims to summarise the extent of current problems, identify areas that can be automated and project whether a self-serve portal can deliver measurable results within 12 months.

## What problem is Legacy-Trust trying to solve?

As the number of recovery accounts has increased, it has been increasingly difficult to handle the recovery process as a whole. Agents are spending large amounts of time checking previous communications and compiling information across multiple sources. This causes the following issues:

* Missed follow-ups
* Duplicated activity (20% duplicate activities in the tracked activities)
* Inconsistent status updates

This is causing a lack of visibility from managers checking on follow-ups and customers being pushed into slow, repetitive contact cycles. Legacy-Trust bank leadership would prefer if agents were able to focus on handling more complex cases that require human judgement/negotiation and let a self-serve portal handle trivial cases, with a clear distinction between these cases and a path to agents if the case becomes messy.

## Why is the current way of working failing at scale?

The current system has been incrementally changed through small agent edits, with the introduction of additional spreadsheets, templates and a memorisation of cases to compensate for the limitations of the system. These manual insertions may have been effective when volumes of accounts were lower, they are starting to pose significant issues for both customers and agents. This is because now the process of accessing a customer's account depends on individual knowledge, manual extraction of emails and spreadsheets, and repeated data entry across multiple platforms. This can be seen by the even split of the recovery activity source system, none of which are connected. 

As the system scales:
* Errors become more difficult to spot and prevent.
* More agent time is spent on searching through administration (duplicate work accounts for ~20% total agent time spent).
* Managers have less visibility on agent work.
* It becomes more difficult to maintain consistent performancem, especially as agents are spending similar amounts of time on cases regardless of delinquency stage and risk tier (all averages are within 20-22.5 minutes). 
* Additional staffing is required to maintain the same amount of open cases.

The overall issue is that the current system cannot scale efficiently as it grows due to compounding administration duties. 

## What evidence would leadership expect before approving Phase 1?

Leadership will require a clear business case that depends on concrete evidence, rather than using assumptions about the benefits of automation. 
This case should clarify:
1. Where the current process breaks down:
    * Recovery performance bottlenecks affecting customer experience.
    * Any sources of wasted handling time, duplicated work and missed follow-ups.
2. Where automation can/should be implemented:
    * Identification of simple recovery tasks that can be completed by customers using self-service.
    * Clear separation of tasks that require human intervention.
3. Expected financial and operational benefits:
    * Quantified time savings.
    * Significant reduction in manual effort.
    * Improvement in collection performance. 
    * Transparency when using assumptions to predict growth of Legacy-Trust.
4. Clear future-state process:
    * Well-defined roles for customers, agents and automated systems.
    * Realistic hand-offs for messy and difficult cases.
5. A realistic Phase 1 ROI:
    * Automation opportunities.
    * Implementation cost estimates.
    * Sensible sensitivity testing

This discovery should aid leadership in deciding whether a seld-serve recovery portal is commercially viable and operationally practical without introducing new risks to collection.


## 2. Stakeholder overview

| Stakeholder group | What they care about | How success is measured | Main worry | Evidence they will trust 
|---|---|---|---|---|
| Operations leadership   | - Making sure the team's effort goes where it actually matters.<br>- Separating simple cases from complex ones.<br>- Utilising agents for cases that require human judgement.     | - Recovery rate as a percentage of outstanding debt.<br>- Recovering more with less wasted effort.                                                                                              | - A system that looks good on paper but does not actually work in practice.                                                                                                                     | - Data from our own operations, not just industry benchmarks or theoretical projections.<br>- Evidence of where the current process actually breaks down, using activity tracker and account data.<br>- Realistic assumptions about what a self-service portal could absorb. |
| Team leaders and agents | - Team capacity and wellbeing.<br>- Having sufficient context to handle customer cases effectively.<br>- Reducing unnecessary administrative work.                                | - Fewer hand-off errors.<br>- Agents spending less time on routine balance queries.                                                                                                             | - Building a system that looks good but leaves awkward cases landing with agents who have even less context than before.                                                                        | - Operational data showing where work is currently being duplicated or delayed.<br>- Evidence from existing processes and account data.<br>- Realistic assumptions about the impact of self-service.                                                                         |
| Finance                 | - Ensuring any investment made delivers measurable and defensible returns.<br>- Having a financial model with transparent assumptions.                                            | - A business case that holds up under scrutiny.<br>- Sensible sensitivity testing.                                                                                                              | - Committing resources to a portal that looks good on paper but does not significantly improve collections performance.<br>- Introducing compliance exposure.                                   | - Operational data tied to real outcomes.<br>- Evidence that delayed follow-ups correlate with lower recovery rates in actual account data.                                                                                                                                  |
| Product and delivery    | - Ensuring discovery outputs are usable downstream.<br>- Understanding the rationale behind recommendations.                                                                      | - A discovery package that allows someone to pick up Phase 1 outputs and clearly understand why recommendations were made.                                                                      | - Incrementally patching problems rather than fixing them properly.                                                                                                                             | - Traceable statistics.<br>- Clear assumptions.<br>- Evidence-based recommendations.                                                                                                                                                                                         |
| Customers               | - Understanding what they owe.<br>- Seeing available payment options.<br>- Having visibility of their case status.<br>- Convenience and the ability to self-serve where possible. | - Debts being resolved quickly.<br>- Information only needing to be provided once.<br>- Progress being easy to track.<br>- Being able to manage repayments without repeated calls or transfers. | - Receiving inconsistent information.<br>- Having to repeat their circumstances multiple times.<br>- Delays in resolving cases.<br>- Uncertainty about whether balances or actions are correct. | - Accurate balances.<br>- Visible repayment options.<br>- Case status updates.<br>- Confirmation of completed actions.<br>- A consistent record of previous interactions that can be independently verified.                                                                 |




## 3. Discovery questions


**1. Where does the actual work happen vs where the process says it happens?**

What do we see when we reconstruct end-to-end case journeys from raw activity logs (emails, spreadsheets, CRM notes), and how often does the “real” workflow differ from the documented process?

**2. Where is effort being hidden by system fragmentation and data reconciliation?**

How much agent time is spent resolving conflicts between sources (spreadsheets vs CRM vs email), and which specific fields or decisions most frequently require manual reconciliation?

**3. Which parts of the portfolio drive disproportionate operational load?**

How does agent time, rework, and follow-up frequency vary across account segments (balance bands, delinquency stage, risk tier), and where is effort highest relative to recoverable value?

**4. Where does the system create rework rather than resolution?**

At what points do cases most frequently return to earlier stages (not just reopen, but loop back due to missing info, customer confusion, or process gaps), and what typically triggers that loop?

**5. What are customers trying to do themselves but failing to complete?**

What inbound contact patterns indicate attempted self-service (e.g. repeated balance checks, payment attempts, status queries), and where do these attempts consistently break down?

**6. Where does agent deviation from process systematically occur — and why?**

Which steps in the current recovery workflow are most frequently bypassed or modified by agents, and what underlying conditions (case complexity, tooling gaps, policy mismatch) drive that behaviour?

**7. Where is the highest concentration of avoidable effort per case?**

When breaking down handling time at task level, which activities (searching, data validation, communication, updating systems) consume the most time without directly changing case outcome?

**8. What is the true cost of inconsistency across systems?**

For cases involving conflicting data sources, what is the measurable impact on resolution time, follow-up frequency, and recovery outcome compared to cases with consistent data?

**9. What does “good” look like in measurable terms — and can we baseline it now?**

Which metrics (e.g. time-to-first-action, follow-up adherence, resolution time, recovery rate by segment) can be reliably reconstructed from existing data to establish a pre-transformation baseline?

## 4. Final problem statement

Legacy-Trust Bank's debt recovery system has been constrained by the fragmentation of a 20-year-old system that comprises a legacy system, spreadsheets and email trails, causing agents to spend a significant amount of time collating information about each case rather than being able to focus on complex cases that require human judgement. This messy system leads to further duplicated work, missed follow-ups and inconsistent case statuses, which limits scalability given the volume of accounts (exceeding 100,000 cases). 

This results in recovery performance being driven by administration skills and memorisation of cases rather than case complexity or value. This lack of separation leads to a muddy idea of automation opportunities and inefficiency costs.

The core problem is therefore a lack of scalable process clarity and data consistency, making it difficult to reliably automate low-complexity recovery activity or demonstrate a robust, evidence-based return on investment for a self-serve recovery model. 