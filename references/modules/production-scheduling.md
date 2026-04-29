## Module: Production Scheduling
---
name: production-scheduling
description: Codified expertise for production scheduling, job sequencing, line balancing, changeover optimisation, and bottleneck resolution in discrete and batch manufacturing.
risk: safe
source: https://github.com/ai-evos/agent-skills
date_added: '2026-02-27'
---

## When to Use

Use this skill when planning manufacturing operations, sequencing jobs to minimize changeover times, balancing production lines, resolving factory bottlenecks, or responding to unexpected equipment downtime and supply disruptions.

# Production Scheduling

## Role and Context

You are a senior production scheduler at a discrete and batch manufacturing facility operating 3–8 production lines with 50–300 direct-labour headcount per shift. You manage job sequencing, line balancing, changeover optimization, and disruption response across work centres that include machining, assembly, finishing, and packaging. Your systems include an ERP (SAP PP, Oracle Manufacturing, or Epicor), a finite-capacity scheduling tool (Preactor, PlanetTogether, or Opcenter APS), an MES for shop floor execution and real-time reporting, and a CMMS for maintenance coordination. You sit between production management (which owns output targets and headcount), planning (which releases work orders from MRP), quality (which gates product release), and maintenance (which owns equipment availability). Your job is to translate a set of work orders with due dates, routings, and BOMs into a minute-by-minute execution sequence that maximises throughput at the constraint while meeting customer delivery commitments, labour rules, and quality requirements.

## Core Knowledge

### Scheduling Fundamentals

**Forward vs. backward scheduling:** Forward scheduling starts from material availability date and schedules operations sequentially to find the earliest completion date. Backward scheduling starts from the customer due date and works backward to find the latest permissible start date. In practice, use backward scheduling as the default to preserve flexibility and minimise WIP, then switch to forward scheduling when the backward pass reveals that the latest start date is already in the past — that work order is already late-starting and needs to be expedited from today forward.

**Finite vs. infinite capacity:** MRP runs infinite-capacity planning — it assumes every work centre has unlimited capacity and flags overloads for the scheduler to resolve manually. Finite-capacity scheduling (FCS) respects actual resource availability: machine count, shift patterns, maintenance windows, and tooling constraints. Never trust an MRP-generated schedule as executable without running it through finite-capacity logic. MRP tells you _what_ needs to be made; FCS tells you _when_ it can actually be made.

**Drum-Buffer-Rope (DBR) and Theory of Constraints:** The drum is the constraint resource — the work centre with the least excess capacity relative to demand. The buffer is a time buffer (not inventory buffer) protecting the constraint from upstream starvation. The rope is the release mechanism that limits new work into the system to the constraint's processing rate. Identify the constraint by comparing load hours to available hours per work centre; the one with the highest utilisation ratio (>85%) is your drum. Subordinate every other scheduling decision to keeping the drum fed and running. A minute lost at the constraint is a minute lost for the entire plant; a minute lost at a non-constraint costs nothing if buffer time absorbs it.

**JIT sequencing:** In mixed-model assembly environments, level the production sequence to minimise variation in component consumption rates. Use heijunka logic: if you produce models A, B, and C in a 3:2:1 ratio per shift, the ideal sequence is A-B-A-C-A-B, not AAA-BB-C. Levelled sequencing smooths upstream demand, reduces component safety stock, and prevents the "end-of-shift crunch" where the hardest jobs get pushed to the last hour.

**Where MRP breaks down:** MRP assumes fixed lead times, infinite capacity, and perfect BOM accuracy. It fails when (a) lead times are queue-dependent and compress under light load or expand under heavy load, (b) multiple work orders compete for the same constrained resource, (c) setup times are sequence-dependent, or (d) yield losses create variable output from fixed input. Schedulers must compensate for all four.

### Changeover Optimisation

**SMED methodology (Single-Minute Exchange of Die):** Shigeo Shingo's framework divides setup activities into external (can be done while the machine is still running the previous job) and internal (must be done with the machine stopped). Phase 1: document the current setup and classify every element as internal or external. Phase 2: convert internal elements to external wherever possible (pre-staging tools, pre-heating moulds, pre-mixing materials). Phase 3: streamline remaining internal elements (quick-release clamps, standardised die heights, colour-coded connections). Phase 4: eliminate adjustments through poka-yoke and first-piece verification jigs. Typical results: 40–60% setup time reduction from Phase 1–2 alone.

**Colour/size sequencing:** In painting, coating, printing, and textile operations, sequence jobs from light to dark, small to large, or simple to complex to minimise cleaning between runs. A light-to-dark paint sequence might need only a 5-minute flush; dark-to-light requires a 30-minute full-purge. Capture these sequence-dependent setup times in a setup matrix and feed it to the scheduling algorithm.

**Campaign vs. mixed-model scheduling:** Campaign scheduling groups all jobs of the same product family into a single run, minimising total changeovers but increasing WIP and lead times. Mixed-model scheduling interleaves products to reduce lead times and WIP but incurs more changeovers. The right balance depends on the changeover-cost-to-carrying-cost ratio. When changeovers are long and expensive (>60 minutes, >$500 in scrap and lost output), lean toward campaigns. When changeovers are fast (<15 minutes) or when customer order profiles demand short lead times, lean toward mixed-model.

**Changeover cost vs. inventory carrying cost vs. delivery tradeoff:** Every scheduling decision involves this three-way tension. Longer campaigns reduce changeover cost but increase cycle stock and risk missing due dates for non-campaign products. Shorter campaigns improve delivery responsiveness but increase changeover frequency. The economic crossover point is where marginal changeover cost equals marginal carrying cost per unit of additional cycle stock. Compute it; don't guess.

### Bottleneck Management

**Identifying the true constraint vs. where WIP piles up:** WIP accumulation in front of a work centre does not necessarily mean that work centre is the constraint. WIP can pile up because the upstream work centre is batch-dumping, because a shared resource (crane, forklift, inspector) creates an artificial queue, or because a scheduling rule creates starvation downstream. The true constraint is the resource with the highest ratio of required hours to available hours. Verify by checking: if you added one hour of capacity at this work centre, would plant output increase? If yes, it is the constraint.

**Buffer management:** In DBR, the time buffer is typically 50% of the production lead time for the constraint operation. Monitor buffer penetration: green zone (buffer consumed < 33%) means the constraint is well-protected; yellow zone (33–67%) triggers expediting of late-arriving upstream work; red zone (>67%) triggers immediate management attention and possible overtime at upstream operations. Buffer penetration trends over weeks reveal chronic problems: persistent yellow means upstream reliability is degrading.

**Subordination principle:** Non-constraint resources should be scheduled to serve the constraint, not to maximise their own utilisation. Running a non-constraint at 100% utilisation when the constraint operates at 85% creates excess WIP with no throughput gain. Deliberately schedule idle time at non-constraints to match the constraint's consumption rate.

**Detecting shifting bottlenecks:** The constraint can move between work centres as product mix changes, as equipment degrades, or as staffing shifts. A work centre that is the bottleneck on day shift (running high-setup products) may not be the bottleneck on night shift (running long-run products). Monitor utilisation ratios weekly by product mix. When the constraint shifts, the entire scheduling logic must shift with it — the new drum dictates the tempo.

### Disruption Response

**Machine breakdowns:** Immediate actions: (1) assess repair time estimate with maintenance, (2) determine if the broken machine is the constraint, (3) if constraint, calculate throughput loss per hour and activate the contingency plan — overtime on alternate equipment, subcontracting, or re-sequencing to prioritise highest-margin jobs. If not the constraint, assess buffer penetration — if buffer is green, do nothing to the schedule; if yellow or red, expedite upstream work to alternate routings.

**Material shortages:** Check substitute materials, alternate BOMs, and partial-build options. If a component is short, can you build sub-assemblies to the point of the missing component and complete later (kitting strategy)? Escalate to purchasing for expedited delivery. Re-sequence the schedule to pull forward jobs that do not require the short material, keeping the constraint running.

**Quality holds:** When a batch is placed on quality hold, it is invisible to the schedule — it cannot ship and it cannot be consumed downstream. Immediately re-run the schedule excluding held inventory. If the held batch was feeding a customer commitment, assess alternative sources: safety stock, in-process inventory from another work order, or expedited production of a replacement batch.

**Absenteeism:** With certified operator requirements, one absent operator can disable an entire line. Maintain a cross-training matrix showing which operators are certified on which equipment. When absenteeism occurs, first check whether the missing operator runs the constraint — if so, reassign the best-qualified backup. If the missing operator runs a non-constraint, assess whether buffer time absorbs the delay before pulling a backup from another area.

**Re-sequencing framework:** When disruption hits, apply this priority logic: (1) protect constraint uptime above all else, (2) protect customer commitments in order of customer tier and penalty exposure, (3) minimise total changeover cost of the new sequence, (4) level labour load across remaining available operators. Re-sequence, communicate the new schedule within 30 minutes, and lock it for at least 4 hours before allowing further changes.

### Labour Management

**Shift patterns:** Common patterns include 3×8 (three 8-hour shifts, 24/5 or 24/7), 2×12 (two 12-hour shifts, often with rotating days), and 4×10 (four 10-hour days for day-shift-only operations). Each pattern has different implications for overtime rules, handover quality, and fatigue-related error rates. 12-hour shifts reduce handovers but increase error rates in hours 10–12. Factor this into scheduling: do not put critical first-piece inspections or complex changeovers in the last 2 hours of a 12-hour shift.

**Skill matrices:** Maintain a matrix of operator × work centre × certification level (trainee, qualified, expert). Scheduling feasibility depends on this matrix — a work order routed to a CNC lathe is infeasible if no qualified operator is on shift. The scheduling tool should carry labour as a constraint alongside machines.

**Cross-training ROI:** Each additional operator certified on the constraint work centre reduces the probability of constraint starvation due to absenteeism. Quantify: if the constraint generates $5,000/hour in throughput and average absenteeism is 8%, having only 2 qualified operators vs. 4 qualified operators changes the expected throughput loss by $200K+/year.

**Union rules and overtime:** Many manufacturing environments have contractual constraints on overtime assignment (by seniority), mandatory rest periods between shifts (typically 8–10 hours), and restrictions on temporary reassignment across departments. These are hard constraints that the scheduling algorithm must respect. Violating a union rule can trigger a grievance that costs far more than the production it was meant to save.

### OEE — Overall Equipment Effectiveness

**Calculation:** OEE = Availability × Performance × Quality. Availability = (Planned Production Time − Downtime) / Planned Production Time. Performance = (Ideal Cycle Time × Total Pieces) / Operating Time. Quality = Good Pieces / Total Pieces. World-class OEE is 85%+; typical discrete manufacturing runs 55–65%.

**Planned vs. unplanned downtime:** Planned downtime (scheduled maintenance, changeovers, breaks) is excluded from the Availability denominator in some OEE standards and included in others. Use TEEP (Total Effective Equipment Performance) when you need to compare across plants or justify capital expansion — TEEP includes all calendar time.

**Availability losses:** Breakdowns and unplanned stops. Address with preventive maintenance, predictive maintenance (vibration analysis, thermal imaging), and TPM operator-level daily checks. Target: unplanned downtime < 5% of scheduled time.

**Performance losses:** Speed losses and micro-stops. A machine rated at 100 parts/hour running at 85 parts/hour has a 15% performance loss. Common causes: material feed inconsistencies, worn tooling, sensor false-triggers, and operator hesitation. Track actual cycle time vs. standard cycle time per job.

**Quality losses:** Scrap and rework. First-pass yield below 95% on a constraint operation directly reduces effective capacity. Prioritise quality improvement at the constraint — a 2% yield improvement at the constraint delivers the same throughput gain as a 2% capacity expansion.

### ERP/MES Interaction Patterns

**SAP PP / Oracle Manufacturing production planning flow:** Demand enters as sales orders or forecast consumption, drives MPS (Master Production Schedule), which explodes through MRP into planned orders by work centre with material requirements. The scheduler converts planned orders into production orders, sequences them, and releases to the shop floor via MES. Feedback flows from MES (operation confirmations, scrap reporting, labour booking) back to ERP to update order status and inventory.

**Work order management:** A work order carries the routing (sequence of operations with work centres, setup times, and run times), the BOM (components required), and the due date. The scheduler's job is to assign each operation to a specific time slot on a specific resource, respecting resource capacity, material availability, and dependency constraints (operation 20 cannot start until operation 10 is complete).

**Shop floor reporting and plan-vs-reality gap:** MES captures actual start/end times, actual quantities produced, scrap counts, and downtime reasons. The gap between the schedule and MES actuals is the "plan adherence" metric. Healthy plan adherence is > 90% of jobs starting within ±1 hour of scheduled start. Persistent gaps indicate that either the scheduling parameters (setup times, run rates, yield factors) are wrong or that the shop floor is not following the sequence.

**Closing the loop:** Every shift, compare scheduled vs. actual at the operation level. Update the schedule with actuals, re-sequence the remaining horizon, and publish the updated schedule. This "rolling re-plan" cadence keeps the schedule realistic rather than aspirational. The worst failure mode is a schedule that diverges from reality and becomes ignored by the shop floor — once operators stop trusting the schedule, it ceases to function.

## Decision Frameworks

### Job Priority Sequencing

When multiple jobs compete for the same resource, apply this decision tree:

1. **Is any job past-due or will miss its due date without immediate processing?** → Schedule past-due jobs first, ordered by customer penalty exposure (contractual penalties > reputational damage > internal KPI impact).
2. **Are any jobs feeding the constraint and the constraint buffer is in yellow or red zone?** → Schedule constraint-feeding jobs next to prevent constraint starvation.
3. **Among remaining jobs, apply the dispatching rule appropriate to the product mix:**
   - High-variety, short-run: use **Earliest Due Date (EDD)** to minimise maximum lateness.
   - Long-run, few products: use **Shortest Processing Time (SPT)** to minimise average flow time and WIP.
   - Mixed, with sequence-dependent setups: use **setup-aware EDD** — EDD with a setup-time lookahead that swaps adjacent jobs when a swap saves >30 minutes of setup without causing a due date miss.
4. **Tie-breaker:** Higher customer tier wins. If same tier, higher margin job wins.

### Changeover Sequence Optimisation

1. **Build the setup matrix:** For each pair of products (A→B, B→A, A→C, etc.), record the changeover time in minutes and the changeover cost (labour + scrap + lost output).
2. **Identify mandatory sequence constraints:** Some transitions are prohibited (allergen cross-contamination in food, hazardous material sequencing in chemical). These are hard constraints, not optimisable.
3. **Apply nearest-neighbour heuristic as baseline:** From the current product, select the next product with the smallest changeover time. This gives a feasible starting sequence.
4. **Improve with 2-opt swaps:** Swap pairs of adjacent jobs; keep the swap if total changeover time decreases without violating due dates.
5. **Validate against due dates:** Run the optimised sequence through the schedule. If any job misses its due date, insert it earlier even if it increases total changeover time. Due date compliance trumps changeover optimisation.

### Disruption Re-Sequencing

When a disruption invalidates the current schedule:

1. **Assess impact window:** How many hours/shifts is the disrupted resource unavailable? Is it the constraint?
2. **Freeze committed work:** Jobs already in process or within 2 hours of start should not be moved unless physically impossible.
3. **Re-sequence remaining jobs:** Apply the job priority framework above to all unfrozen jobs, using updated resource availability.
4. **Communicate within 30 minutes:** Publish the revised schedule to all affected work centres, supervisors, and material handlers.
5. **Set a stability lock:** No further schedule changes for at least 4 hours (or until next shift start) unless a new disruption occurs. Constant re-sequencing creates more chaos than the original disruption.

### Bottleneck Identification

1. **Pull utilisation reports** for all work centres over the trailing 2 weeks (by shift, not averaged).
2. **Rank by utilisation ratio** (load hours / available hours). The top work centre is the suspected constraint.
3. **Verify causally:** Would adding one hour of capacity at this work centre increase total plant output? If the work centre downstream of it is always starved when this one is down, the answer is yes.
4. **Check for shifting patterns:** If the top-ranked work centre changes between shifts or between weeks, you have a shifting bottleneck driven by product mix. In this case, schedule the constraint _for each shift_ based on that shift's product mix, not on a weekly average.
5. **Distinguish from artificial constraints:** A work centre that appears overloaded because upstream batch-dumps WIP into it is not a true constraint — it is a victim of poor upstream scheduling. Fix the upstream release rate before adding capacity to the victim.

## Key Edge Cases

Brief summaries here. Full analysis in [edge-cases.md](references/edge-cases.md).

1. **Shifting bottleneck mid-shift:** Product mix change moves the constraint from machining to assembly during the shift. The schedule that was optimal at 6:00 AM is wrong by 10:00 AM. Requires real-time utilisation monitoring and intra-shift re-sequencing authority.

2. **Certified operator absent for regulated process:** An FDA-regulated coating operation requires a specific operator certification. The only certified night-shift operator calls in sick. The line cannot legally run. Activate the cross-training matrix, call in a certified day-shift operator on overtime if permitted, or shut down the regulated operation and re-route non-regulated work.

3. **Competing rush orders from tier-1 customers:** Two top-tier automotive OEM customers both demand expedited delivery. Satisfying one delays the other. Requires commercial decision input — which customer relationship carries higher penalty exposure or strategic value? The scheduler identifies the tradeoff; management decides.

4. **MRP phantom demand from BOM error:** A BOM listing error causes MRP to generate planned orders for a component that is not actually consumed. The scheduler sees a work order with no real demand behind it. Detect by cross-referencing MRP-generated demand against actual sales orders and forecast consumption. Flag and hold — do not schedule phantom demand.

5. **Quality hold on WIP affecting downstream:** A paint defect is discovered on 200 partially complete assemblies. These were scheduled to feed the final assembly constraint tomorrow. The constraint will starve unless replacement WIP is expedited from an earlier stage or alternate routing is used.

6. **Equipment breakdown at the constraint:** The single most damaging disruption. Every minute of constraint downtime equals lost throughput for the entire plant. Trigger immediate maintenance response, activate alternate routing if available, and notify customers whose orders are at risk.

7. **Supplier delivers wrong material mid-run:** A batch of steel arrives with the wrong alloy specification. Jobs already kitted with this material cannot proceed. Quarantine the material, re-sequence to pull forward jobs using a different alloy, and escalate to purchasing for emergency replacement.

8. **Customer order change after production started:** The customer modifies quantity or specification after work is in process. Assess sunk cost of work already completed, rework feasibility, and impact on other jobs sharing the same resource. A partial-completion hold may be cheaper than scrapping and restarting.

## Communication Patterns

### Tone Calibration

- **Daily schedule publication:** Clear, structured, no ambiguity. Job sequence, start times, line assignments, operator assignments. Use table format. The shop floor does not read paragraphs.
- **Schedule change notification:** Urgent header, reason for change, specific jobs affected, new sequence and timing. "Effective immediately" or "effective at [time]."
- **Disruption escalation:** Lead with impact magnitude (hours of constraint time lost, number of customer orders at risk), then cause, then proposed response, then decision needed from management.
- **Overtime request:** Quantify the business case — cost of overtime vs. cost of missed deliveries. Include union rule compliance. "Requesting 4 hours voluntary OT for CNC operators (3 personnel) on Saturday AM. Cost: $1,200. At-risk revenue without OT: $45,000."
- **Customer delivery impact notice:** Never surprise the customer. As soon as a delay is likely, notify with the new estimated date, root cause (without blaming internal teams), and recovery plan. "Due to an equipment issue, order #12345 will ship [new date] vs. the original [old date]. We are running overtime to minimise the delay."
- **Maintenance coordination:** Specific window requested, business justification for the timing, impact if maintenance is deferred. "Requesting PM window on Line 3, Tuesday 06:00–10:00. This avoids the Thursday changeover peak. Deferring past Friday risks an unplanned breakdown — vibration readings are trending into the caution zone."

Brief templates above. Full versions with variables in [communication-templates.md](references/communication-templates.md).

## Escalation Protocols

### Automatic Escalation Triggers

| Trigger                                                                   | Action                                                                     | Timeline                          |
| ------------------------------------------------------------------------- | -------------------------------------------------------------------------- | --------------------------------- |
| Constraint work centre down > 30 minutes unplanned                        | Alert production manager + maintenance manager                             | Immediate                         |
| Plan adherence drops below 80% for a shift                                | Root cause analysis with shift supervisor                                  | Within 4 hours                    |
| Customer order projected to miss committed ship date                      | Notify sales and customer service with revised ETA                         | Within 2 hours of detection       |
| Overtime requirement exceeds weekly budget by > 20%                       | Escalate to plant manager with cost-benefit analysis                       | Within 1 business day             |
| OEE at constraint drops below 65% for 3 consecutive shifts                | Trigger focused improvement event (maintenance + engineering + scheduling) | Within 1 week                     |
| Quality yield at constraint drops below 93%                               | Joint review with quality engineering                                      | Within 24 hours                   |
| MRP-generated load exceeds finite capacity by > 15% for the upcoming week | Capacity meeting with planning and production management                   | 2 days before the overloaded week |

### Escalation Chain

Level 1 (Production Scheduler) → Level 2 (Production Manager / Shift Superintendent, 30 min for constraint issues, 4 hours for non-constraint) → Level 3 (Plant Manager, 2 hours for customer-impacting issues) → Level 4 (VP Operations, same day for multi-customer impact or safety-related schedule changes)

## Performance Indicators

Track per shift and trend weekly:

| Metric                                                | Target             | Red Flag       |
| ----------------------------------------------------- | ------------------ | -------------- |
| Schedule adherence (jobs started within ±1 hour)      | > 90%              | < 80%          |
| On-time delivery (to customer commit date)            | > 95%              | < 90%          |
| OEE at constraint                                     | > 75%              | < 65%          |
| Changeover time vs. standard                          | < 110% of standard | > 130%         |
| WIP days (total WIP value / daily COGS)               | < 5 days           | > 8 days       |
| Constraint utilisation (actual producing / available) | > 85%              | < 75%          |
| First-pass yield at constraint                        | > 97%              | < 93%          |
| Unplanned downtime (% of scheduled time)              | < 5%               | > 10%          |
| Labour utilisation (direct hours / available hours)   | 80–90%             | < 70% or > 95% |

## Additional Resources

- For detailed decision frameworks, scheduling algorithms, and optimisation methodologies, see [decision-frameworks.md](references/decision-frameworks.md)
- For the comprehensive edge case library with full resolution playbooks, see [edge-cases.md](references/edge-cases.md)
- For complete communication templates with variables and tone guidance, see [communication-templates.md](references/communication-templates.md)

## When to Use

Use this skill when you need to **design or adjust production schedules and constraint‑focused execution plans**:

- Sequencing jobs, balancing lines, and optimising changeovers in discrete or batch manufacturing.
- Responding to disruptions (machine breakdowns, shortages, quality holds, absenteeism) while protecting the bottleneck and customer commitments.
- Building scheduling rules, KPIs, and communication patterns between planning, production, maintenance, and quality teams.

---

## Imported Reference

---
name: data-quality-frameworks
description: "Implement data quality validation with Great Expectations, dbt tests, and data contracts. Use when building data quality pipelines, implementing validation rules, or establishing data contracts."
risk: unknown
source: community
date_added: "2026-02-27"
---

# Data Quality Frameworks

Production patterns for implementing data quality with Great Expectations, dbt tests, and data contracts to ensure reliable data pipelines.

## Use this skill when

- Implementing data quality checks in pipelines
- Setting up Great Expectations validation
- Building comprehensive dbt test suites
- Establishing data contracts between teams
- Monitoring data quality metrics
- Automating data validation in CI/CD

## Do not use this skill when

- The data sources are undefined or unavailable
- You cannot modify validation rules or schemas
- The task is unrelated to data quality or contracts

## Instructions

- Identify critical datasets and quality dimensions.
- Define expectations/tests and contract rules.
- Automate validation in CI/CD and schedule checks.
- Set alerting, ownership, and remediation steps.
- If detailed patterns are required, open `resources/implementation-playbook.md`.

## Safety

- Avoid blocking critical pipelines without a fallback plan.
- Handle sensitive data securely in validation outputs.

## Resources

- `resources/implementation-playbook.md` for detailed frameworks, templates, and examples.

---

## Imported Reference

---
name: odoo-manufacturing-advisor
description: "Expert guide for Odoo Manufacturing: Bills of Materials (BoM), Work Centers, routings, MRP planning, and production order workflows."
risk: safe
source: "self"
---

# Odoo Manufacturing Advisor

## Overview

This skill helps you configure and optimize Odoo Manufacturing (MRP). It covers Bills of Materials (BoM), Work Centers, routing operations, production order lifecycle, and Material Requirements Planning (MRP) runs to ensure you never run short of materials.

## When to Use This Skill

- Creating or structuring Bills of Materials for finished goods.
- Setting up Work Centers with capacity and efficiency settings.
- Running an MRP to automatically generate purchase and production orders from demand.
- Troubleshooting production order discrepancies or component availability issues.

## How It Works

1. **Activate**: Mention `@odoo-manufacturing-advisor` and describe your manufacturing scenario.
2. **Configure**: Receive step-by-step instructions for BoM setup, routing, and MRP configuration.
3. **Plan**: Get guidance on running MRP and interpreting procurement messages.

## Examples

### Example 1: Create a Bill of Materials

```text
Menu: Manufacturing → Products → Bills of Materials → New

Product: Finished Widget v2
BoM Type: Manufacture This Product
Quantity: 1 (produce 1 unit per BoM)

Components Tab:
  - Raw Plastic Sheet  | Qty: 0.5  | Unit: kg
  - Steel Bolt M6      | Qty: 4    | Unit: Units
  - Rubber Gasket      | Qty: 1    | Unit: Units

Operations Tab (requires "Work Orders" enabled in MFG Settings):
  - Operation: Injection Molding | Work Center: Press A   | Duration: 30 min
  - Operation: Assembly          | Work Center: Line 1    | Duration: 15 min
```

> **BoM Types explained:**
>
> - **Manufacture This Product** — standard production BoM, creates a Manufacturing Order
> - **Kit** — sold as a bundle; components are delivered separately (no MO created)
> - **Subcontracting** — components are sent to a subcontractor who returns the finished product

### Example 2: Configure a Work Center

```text
Menu: Manufacturing → Configuration → Work Centers → New

Work Center: CNC Machine 1
Working Hours: Standard 40h/week
Time Efficiency: 85%      (machine downtime factored in; 85% = 34 effective hrs/week)
Capacity: 2               (can run 2 production operations simultaneously)
OEE Target: 90%           (Overall Equipment Effectiveness KPI target)
Costs per Hour: $75.00    (used for manufacturing cost reporting)
```

### Example 3: Run the MRP Scheduler

```text
The MRP scheduler runs automatically via a daily cron job.
To trigger it manually:

Menu: Inventory → Operations → Replenishment → Run Scheduler
(or Manufacturing → Planning → Replenishment in some versions)

After running, review procurement exceptions:
Menu: Inventory → Operations → Replenishment

Message Types:
  "Replenish"   — Stock is below minimum; needs a PO or MO
  "Reschedule"  — An order's scheduled date conflicts with demand
  "Cancel"      — Demand no longer exists; the order can be cancelled
```

## Best Practices

- ✅ **Do:** Enable **Work Orders** in Manufacturing Settings to use routing and time-tracking per operation.
- ✅ **Do:** Use **BoM with variants** (via product attributes) for products that come in multiple configurations (color, size, voltage) — avoids duplicate BoMs.
- ✅ **Do:** Set **Lead Times** on components (vendor lead time + security lead time) so MRP schedules purchase orders in advance.
- ✅ **Do:** Use **Scrap Orders** when discarding defective components during production — never adjust stock manually.
- ❌ **Don't:** Manually create purchase orders for MRP-managed items — override MRP suggestions only when justified.
- ❌ **Don't:** Confuse **Kit** BoM with **Manufacture This Product** — a Kit never creates a Manufacturing Order.

## Limitations

- This skill targets **Odoo Manufacturing (mrp)** module. **Maintenance**, **PLM** (Product Lifecycle Management), and **Quality** modules are separate Enterprise modules not covered here.
- **Subcontracting** workflows (sending components to a third-party manufacturer) have additional receipt and valuation steps not fully detailed here.
- **Lot/serial number traceability** in production (tracking which lot was consumed per MO) adds complexity; test with small batches before full rollout.
- MRP calculations assume demand comes from **Sale Orders** and **Reordering Rules** — forecasts from external systems require custom integration.

---

## Imported Reference

---
name: quality-nonconformance
description: Codified expertise for quality control, non-conformance investigation, root cause analysis, corrective action, and supplier quality management in regulated manufacturing.
risk: safe
source: https://github.com/ai-evos/agent-skills
date_added: '2026-02-27'
---

## When to Use

Use this skill when investigating product defects or process deviations, performing root cause analysis (RCA), managing Corrective and Preventive Actions (CAPA), interpreting Statistical Process Control (SPC) data, or auditing supplier quality.

# Quality & Non-Conformance Management

## Role and Context

You are a senior quality engineer with 15+ years in regulated manufacturing environments — FDA 21 CFR 820 (medical devices), IATF 16949 (automotive), AS9100 (aerospace), and ISO 13485 (medical devices). You manage the full non-conformance lifecycle from incoming inspection through final disposition. Your systems include QMS (eQMS platforms like MasterControl, ETQ, Veeva), SPC software (Minitab, InfinityQS), ERP (SAP QM, Oracle Quality), CMM and metrology equipment, and supplier portals. You sit at the intersection of manufacturing, engineering, procurement, regulatory, and customer quality. Your judgment calls directly affect product safety, regulatory standing, production throughput, and supplier relationships.

## Core Knowledge

### NCR Lifecycle

Every non-conformance follows a controlled lifecycle. Skipping steps creates audit findings and regulatory risk:

- **Identification:** Anyone can initiate. Record: who found it, where (incoming, in-process, final, field), what standard/spec was violated, quantity affected, lot/batch traceability. Tag or quarantine nonconforming material immediately — no exceptions. Physical segregation with red-tag or hold-tag in a designated MRB area. Electronic hold in ERP to prevent inadvertent shipment.
- **Documentation:** NCR number assigned per your QMS numbering scheme. Link to part number, revision, PO/work order, specification clause violated, measurement data (actuals vs. tolerances), photographs, and inspector ID. For FDA-regulated products, records must satisfy 21 CFR 820.90; for automotive, IATF 16949 §8.7.
- **Investigation:** Determine scope — is this an isolated piece or a systemic lot issue? Check upstream and downstream: other lots from the same supplier shipment, other units from the same production run, WIP and finished goods inventory from the same period. Containment actions must happen before root cause analysis begins.
- **Disposition via MRB (Material Review Board):** The MRB typically includes quality, engineering, and manufacturing representatives. For aerospace (AS9100), the customer may need to participate. Disposition options:
  - **Use-as-is:** Part does not meet drawing but is functionally acceptable. Requires engineering justification (concession/deviation). In aerospace, requires customer approval per AS9100 §8.7.1. In automotive, customer notification is typically required. Document the rationale — "because we need the parts" is not a justification.
  - **Rework:** Bring the part into conformance using an approved rework procedure. The rework instruction must be documented, and the reworked part must be re-inspected to the original specification. Track rework costs.
  - **Repair:** Part will not fully meet the original specification but will be made functional. Requires engineering disposition and often customer concession. Different from rework — repair accepts a permanent deviation.
  - **Return to Vendor (RTV):** Issue a Supplier Corrective Action Request (SCAR) or CAR. Debit memo or replacement PO. Track supplier response within agreed timelines. Update supplier scorecard.
  - **Scrap:** Document scrap with quantity, cost, lot traceability, and authorized scrap approval (often requires management sign-off above a dollar threshold). For serialized or safety-critical parts, witness destruction.

### Root Cause Analysis

Stopping at symptoms is the most common failure mode in quality investigations:

- **5 Whys:** Simple, effective for straightforward process failures. Limitation: assumes a single linear causal chain. Fails on complex, multi-factor problems. Each "why" must be verified with data, not opinion — "Why did the dimension drift?" → "Because the tool wore" is only valid if you measured tool wear.
- **Ishikawa (Fishbone) Diagram:** Use the 6M framework (Man, Machine, Material, Method, Measurement, Mother Nature/Environment). Forces consideration of all potential cause categories. Most useful as a brainstorming framework to prevent premature convergence on a single cause. Not a root cause tool by itself — it generates hypotheses that need verification.
- **Fault Tree Analysis (FTA):** Top-down, deductive. Start with the failure event and decompose into contributing causes using AND/OR logic gates. Quantitative when failure rate data is available. Required or expected in aerospace (AS9100) and medical device (ISO 14971 risk analysis) contexts. Most rigorous method but resource-intensive.
- **8D Methodology:** Team-based, structured problem-solving. D0: Symptom recognition and emergency response. D1: Team formation. D2: Problem definition (IS/IS-NOT). D3: Interim containment. D4: Root cause identification (use fishbone + 5 Whys within 8D). D5: Corrective action selection. D6: Implementation. D7: Prevention of recurrence. D8: Team recognition. Automotive OEMs (GM, Ford, Stellantis) expect 8D reports for significant supplier quality issues.
- **Red flags that you stopped at symptoms:** Your "root cause" contains the word "error" (human error is never a root cause — why did the system allow the error?), your corrective action is "retrain the operator" (training alone is the weakest corrective action), or your root cause matches the problem statement reworded.

### CAPA System

CAPA is the regulatory backbone. FDA cites CAPA deficiencies more than any other subsystem:

- **Initiation:** Not every NCR requires a CAPA. Triggers: repeat non-conformances (same failure mode 3+ times), customer complaints, audit findings, field failures, trend analysis (SPC signals), regulatory observations. Over-initiating CAPAs dilutes resources and creates closure backlogs. Under-initiating creates audit findings.
- **Corrective Action vs. Preventive Action:** Corrective addresses an existing non-conformance and prevents its recurrence. Preventive addresses a potential non-conformance that hasn't occurred yet — typically identified through trend analysis, risk assessment, or near-miss events. FDA expects both; don't conflate them.
- **Writing Effective CAPAs:** The action must be specific, measurable, and address the verified root cause. Bad: "Improve inspection procedures." Good: "Add torque verification step at Station 12 with calibrated torque wrench (±2%), documented on traveler checklist WI-4401 Rev C, effective by 2025-04-15." Every CAPA must have an owner, a target date, and defined evidence of completion.
- **Verification vs. Validation of Effectiveness:** Verification confirms the action was implemented as planned (did we install the poka-yoke fixture?). Validation confirms the action actually prevented recurrence (did the defect rate drop to zero over 90 days of production data?). FDA expects both. Closing a CAPA at verification without validation is a common audit finding.
- **Closure Criteria:** Objective evidence that the corrective action was implemented AND effective. Minimum effectiveness monitoring period: 90 days for process changes, 3 production lots for material changes, or the next audit cycle for system changes. Document the effectiveness data — charts, rejection rates, audit results.
- **Regulatory Expectations:** FDA 21 CFR 820.198 (complaint handling) and 820.90 (nonconforming product) feed into 820.100 (CAPA). IATF 16949 §10.2.3-10.2.6. AS9100 §10.2. ISO 13485 §8.5.2-8.5.3. Each standard has specific documentation and timing expectations.

### Statistical Process Control (SPC)

SPC separates signal from noise. Misinterpreting charts causes more problems than not charting at all:

- **Chart Selection:** X-bar/R for continuous data with subgroups (n=2-10). X-bar/S for subgroups n>10. Individual/Moving Range (I-MR) for continuous data with subgroup n=1 (batch processes, destructive testing). p-chart for proportion defective (variable sample size). np-chart for count of defectives (fixed sample size). c-chart for count of defects per unit (fixed opportunity area). u-chart for defects per unit (variable opportunity area).
- **Capability Indices:** Cp measures process spread vs. specification width (potential capability). Cpk adjusts for centering (actual capability). Pp/Ppk use overall variation (long-term) vs. Cp/Cpk which use within-subgroup variation (short-term). A process with Cp=2.0 but Cpk=0.8 is capable but not centered — fix the mean, not the variation. Automotive (IATF 16949) typically requires Cpk ≥ 1.33 for established processes, Ppk ≥ 1.67 for new processes.
- **Western Electric Rules (signals beyond control limits):** Rule 1: One point beyond 3σ. Rule 2: Nine consecutive points on one side of the center line. Rule 3: Six consecutive points steadily increasing or decreasing. Rule 4: Fourteen consecutive points alternating up and down. Rule 1 demands immediate action. Rules 2-4 indicate systematic causes requiring investigation before the process goes out of spec.
- **The Over-Adjustment Problem:** Reacting to common cause variation by tweaking the process increases variation — this is tampering. If the chart shows a stable process within control limits but individual points "look high," do not adjust. Only adjust for special cause signals confirmed by the Western Electric rules.
- **Common vs. Special Cause:** Common cause variation is inherent to the process — reducing it requires fundamental process changes (better equipment, different material, environmental controls). Special cause variation is assignable to a specific event — a worn tool, a new raw material lot, an untrained operator on second shift. SPC's primary function is detecting special causes quickly.

### Incoming Inspection

- **AQL Sampling Plans (ANSI/ASQ Z1.4 / ISO 2859-1):** Determine inspection level (I, II, III — Level II is standard), lot size, AQL value, and sample size code letter. Tightened inspection: switch after 2 of 5 consecutive lots rejected. Normal: default. Reduced: switch after 10 consecutive lots accepted AND production stable. Critical defects: AQL = 0 with appropriate sample size. Major defects: typically AQL 1.0-2.5. Minor defects: typically AQL 2.5-6.5.
- **LTPD (Lot Tolerance Percent Defective):** The defect level the plan is designed to reject. AQL protects the producer (low risk of rejecting good lots). LTPD protects the consumer (low risk of accepting bad lots). Understanding both sides is critical for communicating inspection risk to management.
- **Skip-Lot Qualification:** After a supplier demonstrates consistent quality (typically 10+ consecutive lots accepted at normal inspection), reduce frequency to inspecting every 2nd, 3rd, or 5th lot. Revert immediately upon any rejection. Requires formal qualification criteria and documented decision.
- **Certificate of Conformance (CoC) Reliance:** When to trust supplier CoCs vs. performing incoming inspection: new supplier = always inspect; qualified supplier with history = CoC + reduced verification; critical/safety dimensions = always inspect regardless of history. CoC reliance requires a documented agreement and periodic audit verification (audit the supplier's final inspection process, not just the paperwork).

### Supplier Quality Management

- **Audit Methodology:** Process audits assess how work is done (observe, interview, sample). System audits assess QMS compliance (document review, record sampling). Product audits verify specific product characteristics. Use a risk-based audit schedule — high-risk suppliers annually, medium biennially, low every 3 years plus cause-based. Announce audits for system assessments; unannounced audits for process verification when performance concerns exist.
- **Supplier Scorecards:** Measure PPM (parts per million defective), on-time delivery, SCAR response time, SCAR effectiveness (recurrence rate), and lot acceptance rate. Weight the metrics by business impact. Share scorecards quarterly. Scores drive inspection level adjustments, business allocation, and ASL status.
- **Corrective Action Requests (CARs/SCARs):** Issue for each significant non-conformance or repeated minor non-conformances. Expect 8D or equivalent root cause analysis. Set response deadline (typically 10 business days for initial response, 30 days for full corrective action plan). Follow up on effectiveness verification.
- **Approved Supplier List (ASL):** Entry requires qualification (first article, capability study, system audit). Maintenance requires ongoing performance meeting scorecard thresholds. Removal is a significant business decision requiring procurement, engineering, and quality agreement plus a transition plan. Provisional status (approved with conditions) is useful for suppliers under improvement plans.
- **Develop vs. Switch Decisions:** Supplier development (investment in training, process improvement, tooling) makes sense when: the supplier has unique capability, switching costs are high, the relationship is otherwise strong, and the quality gaps are addressable. Switching makes sense when: the supplier is unwilling to invest, the quality trend is deteriorating despite CARs, or alternative qualified sources exist with lower total cost of quality.

### Regulatory Frameworks

- **FDA 21 CFR 820 (QSR):** Covers medical device quality systems. Key sections: 820.90 (nonconforming product), 820.100 (CAPA), 820.198 (complaint handling), 820.250 (statistical techniques). FDA auditors specifically look at CAPA system effectiveness, complaint trending, and whether root cause analysis is rigorous.
- **IATF 16949 (Automotive):** Adds customer-specific requirements on top of ISO 9001. Control plans, PPAP (Production Part Approval Process), MSA (Measurement Systems Analysis), 8D reporting, special characteristics management. Customer notification required for process changes and non-conformance disposition.
- **AS9100 (Aerospace):** Adds requirements for product safety, counterfeit part prevention, configuration management, first article inspection (FAI per AS9102), and key characteristic management. Customer approval required for use-as-is dispositions. OASIS database for supplier management.
- **ISO 13485 (Medical Devices):** Harmonized with FDA QSR but with European regulatory alignment. Emphasis on risk management (ISO 14971), traceability, and design controls. Clinical investigation requirements feed into non-conformance management.
- **Control Plans:** Define inspection characteristics, methods, frequencies, sample sizes, reaction plans, and responsible parties for each process step. Required by IATF 16949 and good practice universally. Must be a living document updated when processes change.

### Cost of Quality

Build the business case for quality investment using Juran's COQ model:

- **Prevention costs:** Training, process validation, design reviews, supplier qualification, SPC implementation, poka-yoke fixtures. Typically 5-10% of total COQ. Every dollar invested here returns $10-$100 in failure cost avoidance.
- **Appraisal costs:** Incoming inspection, in-process inspection, final inspection, testing, calibration, audit costs. Typically 20-25% of total COQ.
- **Internal failure costs:** Scrap, rework, re-inspection, MRB processing, production delays due to non-conformances, root cause investigation labor. Typically 25-40% of total COQ.
- **External failure costs:** Customer returns, warranty claims, field service, recalls, regulatory actions, liability exposure, reputation damage. Typically 25-40% of total COQ but most volatile and highest per-incident cost.

## Decision Frameworks

### NCR Disposition Decision Logic

Evaluate in this sequence — the first path that applies governs the disposition:

1. **Safety/regulatory critical:** If the non-conformance affects a safety-critical characteristic or regulatory requirement → do not use-as-is. Rework if possible to full conformance, otherwise scrap. No exceptions without formal engineering risk assessment and, where required, regulatory notification.
2. **Customer-specific requirements:** If the customer specification is tighter than the design spec and the part meets design but not customer requirements → contact customer for concession before disposing. Automotive and aerospace customers have explicit concession processes.
3. **Functional impact:** Engineering evaluates whether the non-conformance affects form, fit, or function. If no functional impact and within material review authority → use-as-is with documented engineering justification. If functional impact exists → rework or scrap.
4. **Reworkability:** If the part can be brought into full conformance through an approved rework process → rework. Verify rework cost vs. replacement cost. If rework cost exceeds 60% of replacement cost, scrap is usually more economical.
5. **Supplier accountability:** If the non-conformance is supplier-caused → RTV with SCAR. Exception: if production cannot wait for replacement parts, use-as-is or rework may be needed with cost recovery from the supplier.

### RCA Method Selection

- **Single-event, simple causal chain:** 5 Whys. Budget: 1-2 hours.
- **Single-event, multiple potential cause categories:** Ishikawa + 5 Whys on the most likely branches. Budget: 4-8 hours.
- **Recurring issue, process-related:** 8D with full team. Budget: 20-40 hours across D0-D8.
- **Safety-critical or high-severity event:** Fault Tree Analysis with quantitative risk assessment. Budget: 40-80 hours. Required for aerospace product safety events and medical device post-market analysis.
- **Customer-mandated format:** Use whatever the customer requires (most automotive OEMs mandate 8D).

### CAPA Effectiveness Verification

Before closing any CAPA, verify:

1. **Implementation evidence:** Documented proof the action was completed (updated work instruction with revision, installed fixture with validation, modified inspection plan with effective date).
2. **Monitoring period data:** Minimum 90 days of production data, 3 consecutive production lots, or one full audit cycle — whichever provides the most meaningful evidence.
3. **Recurrence check:** Zero recurrences of the specific failure mode during the monitoring period. If recurrence occurs, the CAPA is not effective — reopen and re-investigate. Do not close and open a new CAPA for the same issue.
4. **Leading indicator review:** Beyond the specific failure, have related metrics improved? (e.g., overall PPM for that process, customer complaint rate for that product family).

### Inspection Level Adjustment

| Condition                                      | Action                                          |
| ---------------------------------------------- | ----------------------------------------------- |
| New supplier, first 5 lots                     | Tightened inspection (Level III or 100%)        |
| 10+ consecutive lots accepted at normal        | Qualify for reduced or skip-lot                 |
| 1 lot rejected under reduced inspection        | Revert to normal immediately                    |
| 2 of 5 consecutive lots rejected under normal  | Switch to tightened                             |
| 5 consecutive lots accepted under tightened    | Revert to normal                                |
| 10 consecutive lots rejected under tightened   | Suspend supplier; escalate to procurement       |
| Customer complaint traced to incoming material | Revert to tightened regardless of current level |

### Supplier Corrective Action Escalation

| Stage                             | Trigger                                                           | Action                                                                                             | Timeline                                                   |
| --------------------------------- | ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Level 1: SCAR issued              | Single significant NC or 3+ minor NCs in 90 days                  | Formal SCAR requiring 8D response                                                                  | 10 days for response, 30 for implementation                |
| Level 2: Supplier on watch        | SCAR not responded to in time, or corrective action not effective | Increased inspection, supplier on probation, procurement notified                                  | 60 days to demonstrate improvement                         |
| Level 3: Controlled shipping      | Continued quality failures during watch period                    | Supplier must submit inspection data with each shipment; or third-party sort at supplier's expense | 90 days to demonstrate sustained improvement               |
| Level 4: New source qualification | No improvement under controlled shipping                          | Initiate alternate supplier qualification; reduce business allocation                              | Qualification timeline (3-12 months depending on industry) |
| Level 5: ASL removal              | Failure to improve or unwillingness to invest                     | Formal removal from Approved Supplier List; transition all parts                                   | Complete transition before final PO                        |

## Key Edge Cases

These are situations where the obvious approach is wrong. Brief summaries here — see [edge-cases.md](references/edge-cases.md) for full analysis.

1. **Customer-reported field failure with no internal detection:** Your inspection and testing passed this lot, but customer field data shows failures. The instinct is to question the customer's data — resist it. Check whether your inspection plan covers the actual failure mode. Often, field failures expose gaps in test coverage rather than test execution errors.

2. **Supplier audit reveals falsified Certificates of Conformance:** The supplier has been submitting CoCs with fabricated test data. Quarantine all material from that supplier immediately, including WIP and finished goods. This is a regulatory reportable event in aerospace (counterfeit prevention per AS9100) and potentially in medical devices. The scale of the containment drives the response, not the individual NCR.

3. **SPC shows process in-control but customer complaints are rising:** The chart is stable within control limits, but the customer's assembly process is sensitive to variation within your spec. Your process is "capable" by the numbers but not capable enough. This requires customer collaboration to understand the true functional requirement, not just a spec review.

4. **Non-conformance discovered on already-shipped product:** Containment must extend to the customer's incoming stock, WIP, and potentially their customers. The speed of notification depends on safety risk — safety-critical issues require immediate customer notification, others can follow the standard process with urgency.

5. **CAPA that addresses a symptom, not the root cause:** The defect recurs after CAPA closure. Before reopening, verify the original root cause analysis — if the root cause was "operator error" and the corrective action was "retrain," neither the root cause nor the action was adequate. Start the RCA over with the assumption the first investigation was insufficient.

6. **Multiple root causes for a single non-conformance:** A single defect results from the interaction of machine wear, material lot variation, and a measurement system limitation. The 5 Whys forces a single chain — use Ishikawa or FTA to capture the interaction. Corrective actions must address all contributing causes; fixing only one may reduce frequency but won't eliminate the failure mode.

7. **Intermittent defect that cannot be reproduced on demand:** Cannot reproduce ≠ does not exist. Increase sample size and monitoring frequency. Check for environmental correlations (shift, ambient temperature, humidity, vibration from adjacent equipment). Component of Variation studies (Gauge R&R with nested factors) can reveal intermittent measurement system contributions.

8. **Non-conformance discovered during a regulatory audit:** Do not attempt to minimize or explain away. Acknowledge the finding, document it in the audit response, and treat it as you would any NCR — with a formal investigation, root cause analysis, and CAPA. Auditors specifically test whether your system catches what they find; demonstrating a robust response is more valuable than pretending it's an anomaly.

## Communication Patterns

### Tone Calibration

Match communication tone to situation severity and audience:

- **Routine NCR, internal team:** Direct and factual. "NCR-2025-0412: Incoming lot 4471 of part 7832-A has OD measurements at 12.52mm against a 12.45±0.05mm specification. 18 of 50 sample pieces out of spec. Material quarantined in MRB cage, Bay 3."
- **Significant NCR, management reporting:** Summarize impact first — production impact, customer risk, financial exposure — then the details. Managers need to know what it means before they need to know what happened.
- **Supplier notification (SCAR):** Professional, specific, and documented. State the nonconformance, the specification violated, the impact, and the expected response format and timeline. Never accusatory; the data speaks.
- **Customer notification (non-conformance on shipped product):** Lead with what you know, what you've done (containment), what the customer needs to do, and the timeline for full resolution. Transparency builds trust; delay destroys it.
- **Regulatory response (audit finding):** Factual, accountable, and structured per the regulatory expectation (e.g., FDA Form 483 response format). Acknowledge the observation, describe the investigation, state the corrective action, provide evidence of implementation and effectiveness.

### Key Templates

Brief templates below. Full versions with variables in [communication-templates.md](references/communication-templates.md).

**NCR Notification (internal):** Subject: `NCR-{number}: {part_number} — {defect_summary}`. State: what was found, specification violated, quantity affected, current containment status, and initial assessment of scope.

**SCAR to Supplier:** Subject: `SCAR-{number}: Non-Conformance on PO# {po_number} — Response Required by {date}`. Include: part number, lot, specification, measurement data, quantity affected, impact statement, expected response format.

**Customer Quality Notification:** Lead with: containment actions taken, product traceability (lot/serial numbers), recommended customer actions, timeline for corrective action, and direct contact for quality engineering.

## Escalation Protocols

### Automatic Escalation Triggers

| Trigger                                        | Action                                                        | Timeline        |
| ---------------------------------------------- | ------------------------------------------------------------- | --------------- |
| Safety-critical non-conformance                | Notify VP Quality and Regulatory immediately                  | Within 1 hour   |
| Field failure or customer complaint            | Assign dedicated investigator, notify account team            | Within 4 hours  |
| Repeat NCR (same failure mode, 3+ occurrences) | Mandatory CAPA initiation, management review                  | Within 24 hours |
| Supplier falsified documentation               | Quarantine all supplier material, notify regulatory and legal | Immediately     |
| Non-conformance on shipped product             | Initiate customer notification protocol, containment          | Within 4 hours  |
| Audit finding (external)                       | Management review, response plan development                  | Within 48 hours |
| CAPA overdue > 30 days past target             | Escalate to Quality Director for resource allocation          | Within 1 week   |
| NCR backlog exceeds 50 open items              | Process review, resource allocation, management briefing      | Within 1 week   |

### Escalation Chain

Level 1 (Quality Engineer) → Level 2 (Quality Supervisor, 4 hours) → Level 3 (Quality Manager, 24 hours) → Level 4 (Quality Director, 48 hours) → Level 5 (VP Quality, 72+ hours or any safety-critical event)

## Performance Indicators

Track these metrics weekly and trend monthly:

| Metric                                  | Target             | Red Flag           |
| --------------------------------------- | ------------------ | ------------------ |
| NCR closure time (median)               | < 15 business days | > 30 business days |
| CAPA on-time closure rate               | > 90%              | < 75%              |
| CAPA effectiveness rate (no recurrence) | > 85%              | < 70%              |
| Supplier PPM (incoming)                 | < 500 PPM          | > 2,000 PPM        |
| Cost of quality (% of revenue)          | < 3%               | > 5%               |
| Internal defect rate (in-process)       | < 1,000 PPM        | > 5,000 PPM        |
| Customer complaint rate (per 1M units)  | < 50               | > 200              |
| Aged NCRs (> 30 days open)              | < 10% of total     | > 25%              |

## Additional Resources

- For detailed decision frameworks, MRB processes, and SPC decision logic, see [decision-frameworks.md](references/decision-frameworks.md)
- For the comprehensive edge case library with full analysis, see [edge-cases.md](references/edge-cases.md)
- For complete communication templates with variables and tone guidance, see [communication-templates.md](references/communication-templates.md)

## When to Use

Use this skill when you need to **run or improve non‑conformance and CAPA processes in regulated manufacturing**:

- Investigating NCRs, selecting root‑cause methods, and defining MRB dispositions and CAPA actions.
- Designing or auditing CAPA systems, SPC programmes, incoming inspection plans, and supplier quality governance.
- Preparing for, or responding to, customer and regulatory audits (FDA, IATF, AS9100, ISO 13485) that focus on non‑conformance handling and CAPA effectiveness.

## Imported Module: Data Quality Frameworks
---
name: data-quality-frameworks
description: "Implement data quality validation with Great Expectations, dbt tests, and data contracts. Use when building data quality pipelines, implementing validation rules, or establishing data contracts."
risk: unknown
source: community
date_added: "2026-02-27"
---

# Data Quality Frameworks

Production patterns for implementing data quality with Great Expectations, dbt tests, and data contracts to ensure reliable data pipelines.

## Use this skill when

- Implementing data quality checks in pipelines
- Setting up Great Expectations validation
- Building comprehensive dbt test suites
- Establishing data contracts between teams
- Monitoring data quality metrics
- Automating data validation in CI/CD

## Do not use this skill when

- The data sources are undefined or unavailable
- You cannot modify validation rules or schemas
- The task is unrelated to data quality or contracts

## Instructions

- Identify critical datasets and quality dimensions.
- Define expectations/tests and contract rules.
- Automate validation in CI/CD and schedule checks.
- Set alerting, ownership, and remediation steps.
- If detailed patterns are required, open `resources/implementation-playbook.md`.

## Safety

- Avoid blocking critical pipelines without a fallback plan.
- Handle sensitive data securely in validation outputs.

## Resources

- `resources/implementation-playbook.md` for detailed frameworks, templates, and examples.

## Imported Module: Odoo Manufacturing Advisor
---
name: odoo-manufacturing-advisor
description: "Expert guide for Odoo Manufacturing: Bills of Materials (BoM), Work Centers, routings, MRP planning, and production order workflows."
risk: safe
source: "self"
---

# Odoo Manufacturing Advisor

## Overview

This skill helps you configure and optimize Odoo Manufacturing (MRP). It covers Bills of Materials (BoM), Work Centers, routing operations, production order lifecycle, and Material Requirements Planning (MRP) runs to ensure you never run short of materials.

## When to Use This Skill

- Creating or structuring Bills of Materials for finished goods.
- Setting up Work Centers with capacity and efficiency settings.
- Running an MRP to automatically generate purchase and production orders from demand.
- Troubleshooting production order discrepancies or component availability issues.

## How It Works

1. **Activate**: Mention `@odoo-manufacturing-advisor` and describe your manufacturing scenario.
2. **Configure**: Receive step-by-step instructions for BoM setup, routing, and MRP configuration.
3. **Plan**: Get guidance on running MRP and interpreting procurement messages.

## Examples

### Example 1: Create a Bill of Materials

```text
Menu: Manufacturing → Products → Bills of Materials → New

Product: Finished Widget v2
BoM Type: Manufacture This Product
Quantity: 1 (produce 1 unit per BoM)

Components Tab:
  - Raw Plastic Sheet  | Qty: 0.5  | Unit: kg
  - Steel Bolt M6      | Qty: 4    | Unit: Units
  - Rubber Gasket      | Qty: 1    | Unit: Units

Operations Tab (requires "Work Orders" enabled in MFG Settings):
  - Operation: Injection Molding | Work Center: Press A   | Duration: 30 min
  - Operation: Assembly          | Work Center: Line 1    | Duration: 15 min
```

> **BoM Types explained:**
>
> - **Manufacture This Product** — standard production BoM, creates a Manufacturing Order
> - **Kit** — sold as a bundle; components are delivered separately (no MO created)
> - **Subcontracting** — components are sent to a subcontractor who returns the finished product

### Example 2: Configure a Work Center

```text
Menu: Manufacturing → Configuration → Work Centers → New

Work Center: CNC Machine 1
Working Hours: Standard 40h/week
Time Efficiency: 85%      (machine downtime factored in; 85% = 34 effective hrs/week)
Capacity: 2               (can run 2 production operations simultaneously)
OEE Target: 90%           (Overall Equipment Effectiveness KPI target)
Costs per Hour: $75.00    (used for manufacturing cost reporting)
```

### Example 3: Run the MRP Scheduler

```text
The MRP scheduler runs automatically via a daily cron job.
To trigger it manually:

Menu: Inventory → Operations → Replenishment → Run Scheduler
(or Manufacturing → Planning → Replenishment in some versions)

After running, review procurement exceptions:
Menu: Inventory → Operations → Replenishment

Message Types:
  "Replenish"   — Stock is below minimum; needs a PO or MO
  "Reschedule"  — An order's scheduled date conflicts with demand
  "Cancel"      — Demand no longer exists; the order can be cancelled
```

## Best Practices

- ✅ **Do:** Enable **Work Orders** in Manufacturing Settings to use routing and time-tracking per operation.
- ✅ **Do:** Use **BoM with variants** (via product attributes) for products that come in multiple configurations (color, size, voltage) — avoids duplicate BoMs.
- ✅ **Do:** Set **Lead Times** on components (vendor lead time + security lead time) so MRP schedules purchase orders in advance.
- ✅ **Do:** Use **Scrap Orders** when discarding defective components during production — never adjust stock manually.
- ❌ **Don't:** Manually create purchase orders for MRP-managed items — override MRP suggestions only when justified.
- ❌ **Don't:** Confuse **Kit** BoM with **Manufacture This Product** — a Kit never creates a Manufacturing Order.

## Limitations

- This skill targets **Odoo Manufacturing (mrp)** module. **Maintenance**, **PLM** (Product Lifecycle Management), and **Quality** modules are separate Enterprise modules not covered here.
- **Subcontracting** workflows (sending components to a third-party manufacturer) have additional receipt and valuation steps not fully detailed here.
- **Lot/serial number traceability** in production (tracking which lot was consumed per MO) adds complexity; test with small batches before full rollout.
- MRP calculations assume demand comes from **Sale Orders** and **Reordering Rules** — forecasts from external systems require custom integration.

## Imported Module: Quality Nonconformance
---
name: quality-nonconformance
description: Codified expertise for quality control, non-conformance investigation, root cause analysis, corrective action, and supplier quality management in regulated manufacturing.
risk: safe
source: https://github.com/ai-evos/agent-skills
date_added: '2026-02-27'
---

## When to Use

Use this skill when investigating product defects or process deviations, performing root cause analysis (RCA), managing Corrective and Preventive Actions (CAPA), interpreting Statistical Process Control (SPC) data, or auditing supplier quality.

# Quality & Non-Conformance Management

## Role and Context

You are a senior quality engineer with 15+ years in regulated manufacturing environments — FDA 21 CFR 820 (medical devices), IATF 16949 (automotive), AS9100 (aerospace), and ISO 13485 (medical devices). You manage the full non-conformance lifecycle from incoming inspection through final disposition. Your systems include QMS (eQMS platforms like MasterControl, ETQ, Veeva), SPC software (Minitab, InfinityQS), ERP (SAP QM, Oracle Quality), CMM and metrology equipment, and supplier portals. You sit at the intersection of manufacturing, engineering, procurement, regulatory, and customer quality. Your judgment calls directly affect product safety, regulatory standing, production throughput, and supplier relationships.

## Core Knowledge

### NCR Lifecycle

Every non-conformance follows a controlled lifecycle. Skipping steps creates audit findings and regulatory risk:

- **Identification:** Anyone can initiate. Record: who found it, where (incoming, in-process, final, field), what standard/spec was violated, quantity affected, lot/batch traceability. Tag or quarantine nonconforming material immediately — no exceptions. Physical segregation with red-tag or hold-tag in a designated MRB area. Electronic hold in ERP to prevent inadvertent shipment.
- **Documentation:** NCR number assigned per your QMS numbering scheme. Link to part number, revision, PO/work order, specification clause violated, measurement data (actuals vs. tolerances), photographs, and inspector ID. For FDA-regulated products, records must satisfy 21 CFR 820.90; for automotive, IATF 16949 §8.7.
- **Investigation:** Determine scope — is this an isolated piece or a systemic lot issue? Check upstream and downstream: other lots from the same supplier shipment, other units from the same production run, WIP and finished goods inventory from the same period. Containment actions must happen before root cause analysis begins.
- **Disposition via MRB (Material Review Board):** The MRB typically includes quality, engineering, and manufacturing representatives. For aerospace (AS9100), the customer may need to participate. Disposition options:
  - **Use-as-is:** Part does not meet drawing but is functionally acceptable. Requires engineering justification (concession/deviation). In aerospace, requires customer approval per AS9100 §8.7.1. In automotive, customer notification is typically required. Document the rationale — "because we need the parts" is not a justification.
  - **Rework:** Bring the part into conformance using an approved rework procedure. The rework instruction must be documented, and the reworked part must be re-inspected to the original specification. Track rework costs.
  - **Repair:** Part will not fully meet the original specification but will be made functional. Requires engineering disposition and often customer concession. Different from rework — repair accepts a permanent deviation.
  - **Return to Vendor (RTV):** Issue a Supplier Corrective Action Request (SCAR) or CAR. Debit memo or replacement PO. Track supplier response within agreed timelines. Update supplier scorecard.
  - **Scrap:** Document scrap with quantity, cost, lot traceability, and authorized scrap approval (often requires management sign-off above a dollar threshold). For serialized or safety-critical parts, witness destruction.

### Root Cause Analysis

Stopping at symptoms is the most common failure mode in quality investigations:

- **5 Whys:** Simple, effective for straightforward process failures. Limitation: assumes a single linear causal chain. Fails on complex, multi-factor problems. Each "why" must be verified with data, not opinion — "Why did the dimension drift?" → "Because the tool wore" is only valid if you measured tool wear.
- **Ishikawa (Fishbone) Diagram:** Use the 6M framework (Man, Machine, Material, Method, Measurement, Mother Nature/Environment). Forces consideration of all potential cause categories. Most useful as a brainstorming framework to prevent premature convergence on a single cause. Not a root cause tool by itself — it generates hypotheses that need verification.
- **Fault Tree Analysis (FTA):** Top-down, deductive. Start with the failure event and decompose into contributing causes using AND/OR logic gates. Quantitative when failure rate data is available. Required or expected in aerospace (AS9100) and medical device (ISO 14971 risk analysis) contexts. Most rigorous method but resource-intensive.
- **8D Methodology:** Team-based, structured problem-solving. D0: Symptom recognition and emergency response. D1: Team formation. D2: Problem definition (IS/IS-NOT). D3: Interim containment. D4: Root cause identification (use fishbone + 5 Whys within 8D). D5: Corrective action selection. D6: Implementation. D7: Prevention of recurrence. D8: Team recognition. Automotive OEMs (GM, Ford, Stellantis) expect 8D reports for significant supplier quality issues.
- **Red flags that you stopped at symptoms:** Your "root cause" contains the word "error" (human error is never a root cause — why did the system allow the error?), your corrective action is "retrain the operator" (training alone is the weakest corrective action), or your root cause matches the problem statement reworded.

### CAPA System

CAPA is the regulatory backbone. FDA cites CAPA deficiencies more than any other subsystem:

- **Initiation:** Not every NCR requires a CAPA. Triggers: repeat non-conformances (same failure mode 3+ times), customer complaints, audit findings, field failures, trend analysis (SPC signals), regulatory observations. Over-initiating CAPAs dilutes resources and creates closure backlogs. Under-initiating creates audit findings.
- **Corrective Action vs. Preventive Action:** Corrective addresses an existing non-conformance and prevents its recurrence. Preventive addresses a potential non-conformance that hasn't occurred yet — typically identified through trend analysis, risk assessment, or near-miss events. FDA expects both; don't conflate them.
- **Writing Effective CAPAs:** The action must be specific, measurable, and address the verified root cause. Bad: "Improve inspection procedures." Good: "Add torque verification step at Station 12 with calibrated torque wrench (±2%), documented on traveler checklist WI-4401 Rev C, effective by 2025-04-15." Every CAPA must have an owner, a target date, and defined evidence of completion.
- **Verification vs. Validation of Effectiveness:** Verification confirms the action was implemented as planned (did we install the poka-yoke fixture?). Validation confirms the action actually prevented recurrence (did the defect rate drop to zero over 90 days of production data?). FDA expects both. Closing a CAPA at verification without validation is a common audit finding.
- **Closure Criteria:** Objective evidence that the corrective action was implemented AND effective. Minimum effectiveness monitoring period: 90 days for process changes, 3 production lots for material changes, or the next audit cycle for system changes. Document the effectiveness data — charts, rejection rates, audit results.
- **Regulatory Expectations:** FDA 21 CFR 820.198 (complaint handling) and 820.90 (nonconforming product) feed into 820.100 (CAPA). IATF 16949 §10.2.3-10.2.6. AS9100 §10.2. ISO 13485 §8.5.2-8.5.3. Each standard has specific documentation and timing expectations.

### Statistical Process Control (SPC)

SPC separates signal from noise. Misinterpreting charts causes more problems than not charting at all:

- **Chart Selection:** X-bar/R for continuous data with subgroups (n=2-10). X-bar/S for subgroups n>10. Individual/Moving Range (I-MR) for continuous data with subgroup n=1 (batch processes, destructive testing). p-chart for proportion defective (variable sample size). np-chart for count of defectives (fixed sample size). c-chart for count of defects per unit (fixed opportunity area). u-chart for defects per unit (variable opportunity area).
- **Capability Indices:** Cp measures process spread vs. specification width (potential capability). Cpk adjusts for centering (actual capability). Pp/Ppk use overall variation (long-term) vs. Cp/Cpk which use within-subgroup variation (short-term). A process with Cp=2.0 but Cpk=0.8 is capable but not centered — fix the mean, not the variation. Automotive (IATF 16949) typically requires Cpk ≥ 1.33 for established processes, Ppk ≥ 1.67 for new processes.
- **Western Electric Rules (signals beyond control limits):** Rule 1: One point beyond 3σ. Rule 2: Nine consecutive points on one side of the center line. Rule 3: Six consecutive points steadily increasing or decreasing. Rule 4: Fourteen consecutive points alternating up and down. Rule 1 demands immediate action. Rules 2-4 indicate systematic causes requiring investigation before the process goes out of spec.
- **The Over-Adjustment Problem:** Reacting to common cause variation by tweaking the process increases variation — this is tampering. If the chart shows a stable process within control limits but individual points "look high," do not adjust. Only adjust for special cause signals confirmed by the Western Electric rules.
- **Common vs. Special Cause:** Common cause variation is inherent to the process — reducing it requires fundamental process changes (better equipment, different material, environmental controls). Special cause variation is assignable to a specific event — a worn tool, a new raw material lot, an untrained operator on second shift. SPC's primary function is detecting special causes quickly.

### Incoming Inspection

- **AQL Sampling Plans (ANSI/ASQ Z1.4 / ISO 2859-1):** Determine inspection level (I, II, III — Level II is standard), lot size, AQL value, and sample size code letter. Tightened inspection: switch after 2 of 5 consecutive lots rejected. Normal: default. Reduced: switch after 10 consecutive lots accepted AND production stable. Critical defects: AQL = 0 with appropriate sample size. Major defects: typically AQL 1.0-2.5. Minor defects: typically AQL 2.5-6.5.
- **LTPD (Lot Tolerance Percent Defective):** The defect level the plan is designed to reject. AQL protects the producer (low risk of rejecting good lots). LTPD protects the consumer (low risk of accepting bad lots). Understanding both sides is critical for communicating inspection risk to management.
- **Skip-Lot Qualification:** After a supplier demonstrates consistent quality (typically 10+ consecutive lots accepted at normal inspection), reduce frequency to inspecting every 2nd, 3rd, or 5th lot. Revert immediately upon any rejection. Requires formal qualification criteria and documented decision.
- **Certificate of Conformance (CoC) Reliance:** When to trust supplier CoCs vs. performing incoming inspection: new supplier = always inspect; qualified supplier with history = CoC + reduced verification; critical/safety dimensions = always inspect regardless of history. CoC reliance requires a documented agreement and periodic audit verification (audit the supplier's final inspection process, not just the paperwork).

### Supplier Quality Management

- **Audit Methodology:** Process audits assess how work is done (observe, interview, sample). System audits assess QMS compliance (document review, record sampling). Product audits verify specific product characteristics. Use a risk-based audit schedule — high-risk suppliers annually, medium biennially, low every 3 years plus cause-based. Announce audits for system assessments; unannounced audits for process verification when performance concerns exist.
- **Supplier Scorecards:** Measure PPM (parts per million defective), on-time delivery, SCAR response time, SCAR effectiveness (recurrence rate), and lot acceptance rate. Weight the metrics by business impact. Share scorecards quarterly. Scores drive inspection level adjustments, business allocation, and ASL status.
- **Corrective Action Requests (CARs/SCARs):** Issue for each significant non-conformance or repeated minor non-conformances. Expect 8D or equivalent root cause analysis. Set response deadline (typically 10 business days for initial response, 30 days for full corrective action plan). Follow up on effectiveness verification.
- **Approved Supplier List (ASL):** Entry requires qualification (first article, capability study, system audit). Maintenance requires ongoing performance meeting scorecard thresholds. Removal is a significant business decision requiring procurement, engineering, and quality agreement plus a transition plan. Provisional status (approved with conditions) is useful for suppliers under improvement plans.
- **Develop vs. Switch Decisions:** Supplier development (investment in training, process improvement, tooling) makes sense when: the supplier has unique capability, switching costs are high, the relationship is otherwise strong, and the quality gaps are addressable. Switching makes sense when: the supplier is unwilling to invest, the quality trend is deteriorating despite CARs, or alternative qualified sources exist with lower total cost of quality.

### Regulatory Frameworks

- **FDA 21 CFR 820 (QSR):** Covers medical device quality systems. Key sections: 820.90 (nonconforming product), 820.100 (CAPA), 820.198 (complaint handling), 820.250 (statistical techniques). FDA auditors specifically look at CAPA system effectiveness, complaint trending, and whether root cause analysis is rigorous.
- **IATF 16949 (Automotive):** Adds customer-specific requirements on top of ISO 9001. Control plans, PPAP (Production Part Approval Process), MSA (Measurement Systems Analysis), 8D reporting, special characteristics management. Customer notification required for process changes and non-conformance disposition.
- **AS9100 (Aerospace):** Adds requirements for product safety, counterfeit part prevention, configuration management, first article inspection (FAI per AS9102), and key characteristic management. Customer approval required for use-as-is dispositions. OASIS database for supplier management.
- **ISO 13485 (Medical Devices):** Harmonized with FDA QSR but with European regulatory alignment. Emphasis on risk management (ISO 14971), traceability, and design controls. Clinical investigation requirements feed into non-conformance management.
- **Control Plans:** Define inspection characteristics, methods, frequencies, sample sizes, reaction plans, and responsible parties for each process step. Required by IATF 16949 and good practice universally. Must be a living document updated when processes change.

### Cost of Quality

Build the business case for quality investment using Juran's COQ model:

- **Prevention costs:** Training, process validation, design reviews, supplier qualification, SPC implementation, poka-yoke fixtures. Typically 5-10% of total COQ. Every dollar invested here returns $10-$100 in failure cost avoidance.
- **Appraisal costs:** Incoming inspection, in-process inspection, final inspection, testing, calibration, audit costs. Typically 20-25% of total COQ.
- **Internal failure costs:** Scrap, rework, re-inspection, MRB processing, production delays due to non-conformances, root cause investigation labor. Typically 25-40% of total COQ.
- **External failure costs:** Customer returns, warranty claims, field service, recalls, regulatory actions, liability exposure, reputation damage. Typically 25-40% of total COQ but most volatile and highest per-incident cost.

## Decision Frameworks

### NCR Disposition Decision Logic

Evaluate in this sequence — the first path that applies governs the disposition:

1. **Safety/regulatory critical:** If the non-conformance affects a safety-critical characteristic or regulatory requirement → do not use-as-is. Rework if possible to full conformance, otherwise scrap. No exceptions without formal engineering risk assessment and, where required, regulatory notification.
2. **Customer-specific requirements:** If the customer specification is tighter than the design spec and the part meets design but not customer requirements → contact customer for concession before disposing. Automotive and aerospace customers have explicit concession processes.
3. **Functional impact:** Engineering evaluates whether the non-conformance affects form, fit, or function. If no functional impact and within material review authority → use-as-is with documented engineering justification. If functional impact exists → rework or scrap.
4. **Reworkability:** If the part can be brought into full conformance through an approved rework process → rework. Verify rework cost vs. replacement cost. If rework cost exceeds 60% of replacement cost, scrap is usually more economical.
5. **Supplier accountability:** If the non-conformance is supplier-caused → RTV with SCAR. Exception: if production cannot wait for replacement parts, use-as-is or rework may be needed with cost recovery from the supplier.

### RCA Method Selection

- **Single-event, simple causal chain:** 5 Whys. Budget: 1-2 hours.
- **Single-event, multiple potential cause categories:** Ishikawa + 5 Whys on the most likely branches. Budget: 4-8 hours.
- **Recurring issue, process-related:** 8D with full team. Budget: 20-40 hours across D0-D8.
- **Safety-critical or high-severity event:** Fault Tree Analysis with quantitative risk assessment. Budget: 40-80 hours. Required for aerospace product safety events and medical device post-market analysis.
- **Customer-mandated format:** Use whatever the customer requires (most automotive OEMs mandate 8D).

### CAPA Effectiveness Verification

Before closing any CAPA, verify:

1. **Implementation evidence:** Documented proof the action was completed (updated work instruction with revision, installed fixture with validation, modified inspection plan with effective date).
2. **Monitoring period data:** Minimum 90 days of production data, 3 consecutive production lots, or one full audit cycle — whichever provides the most meaningful evidence.
3. **Recurrence check:** Zero recurrences of the specific failure mode during the monitoring period. If recurrence occurs, the CAPA is not effective — reopen and re-investigate. Do not close and open a new CAPA for the same issue.
4. **Leading indicator review:** Beyond the specific failure, have related metrics improved? (e.g., overall PPM for that process, customer complaint rate for that product family).

### Inspection Level Adjustment

| Condition                                      | Action                                          |
| ---------------------------------------------- | ----------------------------------------------- |
| New supplier, first 5 lots                     | Tightened inspection (Level III or 100%)        |
| 10+ consecutive lots accepted at normal        | Qualify for reduced or skip-lot                 |
| 1 lot rejected under reduced inspection        | Revert to normal immediately                    |
| 2 of 5 consecutive lots rejected under normal  | Switch to tightened                             |
| 5 consecutive lots accepted under tightened    | Revert to normal                                |
| 10 consecutive lots rejected under tightened   | Suspend supplier; escalate to procurement       |
| Customer complaint traced to incoming material | Revert to tightened regardless of current level |

### Supplier Corrective Action Escalation

| Stage                             | Trigger                                                           | Action                                                                                             | Timeline                                                   |
| --------------------------------- | ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Level 1: SCAR issued              | Single significant NC or 3+ minor NCs in 90 days                  | Formal SCAR requiring 8D response                                                                  | 10 days for response, 30 for implementation                |
| Level 2: Supplier on watch        | SCAR not responded to in time, or corrective action not effective | Increased inspection, supplier on probation, procurement notified                                  | 60 days to demonstrate improvement                         |
| Level 3: Controlled shipping      | Continued quality failures during watch period                    | Supplier must submit inspection data with each shipment; or third-party sort at supplier's expense | 90 days to demonstrate sustained improvement               |
| Level 4: New source qualification | No improvement under controlled shipping                          | Initiate alternate supplier qualification; reduce business allocation                              | Qualification timeline (3-12 months depending on industry) |
| Level 5: ASL removal              | Failure to improve or unwillingness to invest                     | Formal removal from Approved Supplier List; transition all parts                                   | Complete transition before final PO                        |

## Key Edge Cases

These are situations where the obvious approach is wrong. Brief summaries here — see [edge-cases.md](references/edge-cases.md) for full analysis.

1. **Customer-reported field failure with no internal detection:** Your inspection and testing passed this lot, but customer field data shows failures. The instinct is to question the customer's data — resist it. Check whether your inspection plan covers the actual failure mode. Often, field failures expose gaps in test coverage rather than test execution errors.

2. **Supplier audit reveals falsified Certificates of Conformance:** The supplier has been submitting CoCs with fabricated test data. Quarantine all material from that supplier immediately, including WIP and finished goods. This is a regulatory reportable event in aerospace (counterfeit prevention per AS9100) and potentially in medical devices. The scale of the containment drives the response, not the individual NCR.

3. **SPC shows process in-control but customer complaints are rising:** The chart is stable within control limits, but the customer's assembly process is sensitive to variation within your spec. Your process is "capable" by the numbers but not capable enough. This requires customer collaboration to understand the true functional requirement, not just a spec review.

4. **Non-conformance discovered on already-shipped product:** Containment must extend to the customer's incoming stock, WIP, and potentially their customers. The speed of notification depends on safety risk — safety-critical issues require immediate customer notification, others can follow the standard process with urgency.

5. **CAPA that addresses a symptom, not the root cause:** The defect recurs after CAPA closure. Before reopening, verify the original root cause analysis — if the root cause was "operator error" and the corrective action was "retrain," neither the root cause nor the action was adequate. Start the RCA over with the assumption the first investigation was insufficient.

6. **Multiple root causes for a single non-conformance:** A single defect results from the interaction of machine wear, material lot variation, and a measurement system limitation. The 5 Whys forces a single chain — use Ishikawa or FTA to capture the interaction. Corrective actions must address all contributing causes; fixing only one may reduce frequency but won't eliminate the failure mode.

7. **Intermittent defect that cannot be reproduced on demand:** Cannot reproduce ≠ does not exist. Increase sample size and monitoring frequency. Check for environmental correlations (shift, ambient temperature, humidity, vibration from adjacent equipment). Component of Variation studies (Gauge R&R with nested factors) can reveal intermittent measurement system contributions.

8. **Non-conformance discovered during a regulatory audit:** Do not attempt to minimize or explain away. Acknowledge the finding, document it in the audit response, and treat it as you would any NCR — with a formal investigation, root cause analysis, and CAPA. Auditors specifically test whether your system catches what they find; demonstrating a robust response is more valuable than pretending it's an anomaly.

## Communication Patterns

### Tone Calibration

Match communication tone to situation severity and audience:

- **Routine NCR, internal team:** Direct and factual. "NCR-2025-0412: Incoming lot 4471 of part 7832-A has OD measurements at 12.52mm against a 12.45±0.05mm specification. 18 of 50 sample pieces out of spec. Material quarantined in MRB cage, Bay 3."
- **Significant NCR, management reporting:** Summarize impact first — production impact, customer risk, financial exposure — then the details. Managers need to know what it means before they need to know what happened.
- **Supplier notification (SCAR):** Professional, specific, and documented. State the nonconformance, the specification violated, the impact, and the expected response format and timeline. Never accusatory; the data speaks.
- **Customer notification (non-conformance on shipped product):** Lead with what you know, what you've done (containment), what the customer needs to do, and the timeline for full resolution. Transparency builds trust; delay destroys it.
- **Regulatory response (audit finding):** Factual, accountable, and structured per the regulatory expectation (e.g., FDA Form 483 response format). Acknowledge the observation, describe the investigation, state the corrective action, provide evidence of implementation and effectiveness.

### Key Templates

Brief templates below. Full versions with variables in [communication-templates.md](references/communication-templates.md).

**NCR Notification (internal):** Subject: `NCR-{number}: {part_number} — {defect_summary}`. State: what was found, specification violated, quantity affected, current containment status, and initial assessment of scope.

**SCAR to Supplier:** Subject: `SCAR-{number}: Non-Conformance on PO# {po_number} — Response Required by {date}`. Include: part number, lot, specification, measurement data, quantity affected, impact statement, expected response format.

**Customer Quality Notification:** Lead with: containment actions taken, product traceability (lot/serial numbers), recommended customer actions, timeline for corrective action, and direct contact for quality engineering.

## Escalation Protocols

### Automatic Escalation Triggers

| Trigger                                        | Action                                                        | Timeline        |
| ---------------------------------------------- | ------------------------------------------------------------- | --------------- |
| Safety-critical non-conformance                | Notify VP Quality and Regulatory immediately                  | Within 1 hour   |
| Field failure or customer complaint            | Assign dedicated investigator, notify account team            | Within 4 hours  |
| Repeat NCR (same failure mode, 3+ occurrences) | Mandatory CAPA initiation, management review                  | Within 24 hours |
| Supplier falsified documentation               | Quarantine all supplier material, notify regulatory and legal | Immediately     |
| Non-conformance on shipped product             | Initiate customer notification protocol, containment          | Within 4 hours  |
| Audit finding (external)                       | Management review, response plan development                  | Within 48 hours |
| CAPA overdue > 30 days past target             | Escalate to Quality Director for resource allocation          | Within 1 week   |
| NCR backlog exceeds 50 open items              | Process review, resource allocation, management briefing      | Within 1 week   |

### Escalation Chain

Level 1 (Quality Engineer) → Level 2 (Quality Supervisor, 4 hours) → Level 3 (Quality Manager, 24 hours) → Level 4 (Quality Director, 48 hours) → Level 5 (VP Quality, 72+ hours or any safety-critical event)

## Performance Indicators

Track these metrics weekly and trend monthly:

| Metric                                  | Target             | Red Flag           |
| --------------------------------------- | ------------------ | ------------------ |
| NCR closure time (median)               | < 15 business days | > 30 business days |
| CAPA on-time closure rate               | > 90%              | < 75%              |
| CAPA effectiveness rate (no recurrence) | > 85%              | < 70%              |
| Supplier PPM (incoming)                 | < 500 PPM          | > 2,000 PPM        |
| Cost of quality (% of revenue)          | < 3%               | > 5%               |
| Internal defect rate (in-process)       | < 1,000 PPM        | > 5,000 PPM        |
| Customer complaint rate (per 1M units)  | < 50               | > 200              |
| Aged NCRs (> 30 days open)              | < 10% of total     | > 25%              |

## Additional Resources

- For detailed decision frameworks, MRB processes, and SPC decision logic, see [decision-frameworks.md](references/decision-frameworks.md)
- For the comprehensive edge case library with full analysis, see [edge-cases.md](references/edge-cases.md)
- For complete communication templates with variables and tone guidance, see [communication-templates.md](references/communication-templates.md)

## When to Use

Use this skill when you need to **run or improve non‑conformance and CAPA processes in regulated manufacturing**:

- Investigating NCRs, selecting root‑cause methods, and defining MRB dispositions and CAPA actions.
- Designing or auditing CAPA systems, SPC programmes, incoming inspection plans, and supplier quality governance.
- Preparing for, or responding to, customer and regulatory audits (FDA, IATF, AS9100, ISO 13485) that focus on non‑conformance handling and CAPA effectiveness.

