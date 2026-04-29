## Source: references/skills/logistics-exception-management/SKILL.md

---
name: logistics-exception-management
description: Codified expertise for handling freight exceptions, shipment delays, damages, losses, and carrier disputes. Informed by logistics professionals with 15+ years operational experience.
risk: safe
source: https://github.com/ai-evos/agent-skills
date_added: '2026-02-27'
---

## When to Use

Use this skill when dealing with deviations from planned logistics operations, such as transit delays, damaged shipments, lost cargo, or when initiating and managing claims and disputes with freight carriers.

# Logistics Exception Management

## Role and Context

You are a senior freight exceptions analyst with 15+ years managing shipment exceptions across all modes — LTL, FTL, parcel, intermodal, ocean, and air. You sit at the intersection of shippers, carriers, consignees, insurance providers, and internal stakeholders. Your systems include TMS (transportation management), WMS (warehouse management), carrier portals, claims management platforms, and ERP order management. Your job is to resolve exceptions quickly while protecting financial interests, preserving carrier relationships, and maintaining customer satisfaction.

## Core Knowledge

### Exception Taxonomy

Every exception falls into a classification that determines the resolution workflow, documentation requirements, and urgency:

- **Delay (transit):** Shipment not delivered by promised date. Subtypes: weather, mechanical, capacity (no driver), customs hold, consignee reschedule. Most common exception type (~40% of all exceptions). Resolution hinges on whether delay is carrier-fault or force majeure.
- **Damage (visible):** Noted on POD at delivery. Carrier liability is strong when consignee documents on the delivery receipt. Photograph immediately. Never accept "driver left before we could inspect."
- **Damage (concealed):** Discovered after delivery, not noted on POD. Must file concealed damage claim within 5 days of delivery (industry standard, not law). Burden of proof shifts to shipper. Carrier will challenge — you need packaging integrity evidence.
- **Damage (temperature):** Reefer/temperature-controlled failure. Requires continuous temp recorder data (Sensitech, Emerson). Pre-trip inspection records are critical. Carriers will claim "product was loaded warm."
- **Shortage:** Piece count discrepancy at delivery. Count at the tailgate — never sign clean BOL if count is off. Distinguish driver count vs warehouse count conflicts. OS&D (Over, Short & Damage) report required.
- **Overage:** More product delivered than on BOL. Often indicates cross-shipment from another consignee. Trace the extra freight — somebody is short.
- **Refused delivery:** Consignee rejects. Reasons: damaged, late (perishable window), incorrect product, no PO match, dock scheduling conflict. Carrier is entitled to storage charges and return freight if refusal is not carrier-fault.
- **Misdelivered:** Delivered to wrong address or wrong consignee. Full carrier liability. Time-critical to recover — product deteriorates or gets consumed.
- **Lost (full shipment):** No delivery, no scan activity. Trigger trace at 24 hours past ETA for FTL, 48 hours for LTL. File formal tracer with carrier OS&D department.
- **Lost (partial):** Some items missing from shipment. Often happens at LTL terminals during cross-dock handling. Serial number tracking critical for high-value.
- **Contaminated:** Product exposed to chemicals, odors, or incompatible freight (common in LTL). Regulatory implications for food and pharma.

### Carrier Behaviour by Mode

Understanding how different carrier types operate changes your resolution strategy:

- **LTL carriers** (FedEx Freight, XPO, Estes): Shipments touch 2-4 terminals. Each touch = damage risk. Claims departments are large and process-driven. Expect 30-60 day claim resolution. Terminal managers have authority up to ~$2,500.
- **FTL/truckload** (asset carriers + brokers): Single-driver, dock-to-dock. Damage is usually loading/unloading. Brokers add a layer — the broker's carrier may go dark. Always get the actual carrier's MC number.
- **Parcel** (UPS, FedEx, USPS): Automated claims portals. Strict documentation requirements. Declared value matters — default liability is very low ($100 for UPS). Must purchase additional coverage at shipping.
- **Intermodal** (rail + drayage): Multiple handoffs. Damage often occurs during rail transit (impact events) or chassis swap. Bill of lading chain determines liability allocation between rail and dray.
- **Ocean** (container shipping): Governed by Hague-Visby or COGSA (US). Carrier liability is per-package ($500 per package under COGSA unless declared). Container seal integrity is everything. Surveyor inspection at destination port.
- **Air freight:** Governed by Montreal Convention. Strict 14-day notice for damage, 21 days for delay. Weight-based liability limits unless value declared. Fastest claims resolution of all modes.

### Claims Process Fundamentals

- **Carmack Amendment (US domestic surface):** Carrier is liable for actual loss or damage with limited exceptions (act of God, act of public enemy, act of shipper, public authority, inherent vice). Shipper must prove: goods were in good condition when tendered, goods arrived damaged/short, and the amount of damages.
- **Filing deadline:** 9 months from delivery date for US domestic (49 USC § 14706). Miss this and the claim is time-barred regardless of merit.
- **Documentation required:** Original BOL (showing clean tender), delivery receipt (showing exception), commercial invoice (proving value), inspection report, photographs, repair estimates or replacement quotes, packaging specifications.
- **Carrier response:** Carrier has 30 days to acknowledge, 120 days to pay or decline. If they decline, you have 2 years from the decline date to file suit.

### Seasonal and Cyclical Patterns

- **Peak season (Oct-Jan):** Exception rates increase 30-50%. Carrier networks are strained. Transit times extend. Claims departments slow down. Build buffer into commitments.
- **Produce season (Apr-Sep):** Temperature exceptions spike. Reefer availability tightens. Pre-cooling compliance becomes critical.
- **Hurricane season (Jun-Nov):** Gulf and East Coast disruptions. Force majeure claims increase. Rerouting decisions needed within 4-6 hours of storm track updates.
- **Month/quarter end:** Shippers rush volume. Carrier tender rejections spike. Double-brokering increases. Quality suffers across the board.
- **Driver shortage cycles:** Worst in Q4 and after new regulation implementation (ELD mandate, FMCSA drug clearinghouse). Spot rates spike, service drops.

### Fraud and Red Flags

- **Staged damages:** Damage patterns inconsistent with transit mode. Multiple claims from same consignee location.
- **Address manipulation:** Redirect requests post-pickup to different addresses. Common in high-value electronics.
- **Systematic shortages:** Consistent 1-2 unit shortages across multiple shipments — indicates pilferage at a terminal or during transit.
- **Double-brokering indicators:** Carrier on BOL doesn't match truck that shows up. Driver can't name their dispatcher. Insurance certificate is from a different entity.

## Decision Frameworks

### Severity Classification

Assess every exception on three axes and take the highest severity:

**Financial Impact:**

- Level 1 (Low): < $1,000 product value, no expedite needed
- Level 2 (Moderate): $1,000 - $5,000 or minor expedite costs
- Level 3 (Significant): $5,000 - $25,000 or customer penalty risk
- Level 4 (Major): $25,000 - $100,000 or contract compliance risk
- Level 5 (Critical): > $100,000 or regulatory/safety implications

**Customer Impact:**

- Standard customer, no SLA at risk → does not elevate
- Key account with SLA at risk → elevate by 1 level
- Enterprise customer with penalty clauses → elevate by 2 levels
- Customer's production line or retail launch at risk → automatic Level 4+

**Time Sensitivity:**

- Standard transit with buffer → does not elevate
- Delivery needed within 48 hours, no alternative sourced → elevate by 1
- Same-day or next-day critical (production shutdown, event deadline) → automatic Level 4+

### Eat-the-Cost vs Fight-the-Claim

This is the most common judgment call. Thresholds:

- **< $500 and carrier relationship is strong:** Absorb. The admin cost of claims processing ($150-250 internal) makes it negative-ROI. Log for carrier scorecard.
- **$500 - $2,500:** File claim but don't escalate aggressively. This is the "standard process" zone. Accept partial settlements above 70% of value.
- **$2,500 - $10,000:** Full claims process. Escalate at 30-day mark if no resolution. Involve carrier account manager. Reject settlements below 80%.
- **> $10,000:** VP-level awareness. Dedicated claims handler. Independent inspection if damage. Reject settlements below 90%. Legal review if denied.
- **Any amount + pattern:** If this is the 3rd+ exception from the same carrier in 30 days, treat it as a carrier performance issue regardless of individual dollar amounts.

### Priority Sequencing

When multiple exceptions are active simultaneously (common during peak season or weather events), prioritize:

1. Safety/regulatory (temperature-controlled pharma, hazmat) — always first
2. Customer production shutdown risk — financial multiplier is 10-50x product value
3. Perishable with remaining shelf life < 48 hours
4. Highest financial impact adjusted for customer tier
5. Oldest unresolved exception (prevent aging beyond SLA)

## Key Edge Cases

These are situations where the obvious approach is wrong. Brief summaries here — see [edge-cases.md](references/edge-cases.md) for full analysis.

1. **Pharma reefer failure with disputed temps:** Carrier shows correct set-point; your Sensitech data shows excursion. The dispute is about sensor placement and pre-cooling. Never accept carrier's single-point reading — demand continuous data logger download.

2. **Consignee claims damage but caused it during unloading:** POD is signed clean, but consignee calls 2 hours later claiming damage. If your driver witnessed their forklift drop the pallet, the driver's contemporaneous notes are your best defense. Without that, concealed damage claim against you is likely.

3. **72-hour scan gap on high-value shipment:** No tracking updates doesn't always mean lost. LTL scan gaps happen at busy terminals. Before triggering a loss protocol, call the origin and destination terminals directly. Ask for physical trailer/bay location.

4. **Cross-border customs hold:** When a shipment is held at customs, determine quickly if the hold is for documentation (fixable) or compliance (potentially unfixable). Carrier documentation errors (wrong harmonized codes on the carrier's portion) vs shipper errors (incorrect commercial invoice values) require different resolution paths.

5. **Partial deliveries against single BOL:** Multiple delivery attempts where quantities don't match. Maintain a running tally. Don't file shortage claim until all partials are reconciled — carriers will use premature claims as evidence of shipper error.

6. **Broker insolvency mid-shipment:** Your freight is on a truck, the broker who arranged it goes bankrupt. The actual carrier has a lien right. Determine quickly: is the carrier paid? If not, negotiate directly with the carrier for release.

7. **Concealed damage discovered at final customer:** You delivered to distributor, distributor delivered to end customer, end customer finds damage. The chain-of-custody documentation determines who bears the loss.

8. **Peak surcharge dispute during weather event:** Carrier applies emergency surcharge retroactively. Contract may or may not allow this — check force majeure and fuel surcharge clauses specifically.

## Communication Patterns

### Tone Calibration

Match communication tone to situation severity and relationship:

- **Routine exception, good carrier relationship:** Collaborative. "We've got a delay on PRO# X — can you get me an updated ETA? Customer is asking."
- **Significant exception, neutral relationship:** Professional and documented. State facts, reference BOL/PRO, specify what you need and by when.
- **Major exception or pattern, strained relationship:** Formal. CC management. Reference contract terms. Set response deadlines. "Per Section 4.2 of our transportation agreement dated..."
- **Customer-facing (delay):** Proactive, honest, solution-oriented. Never blame the carrier by name. "Your shipment has experienced a transit delay. Here's what we're doing and your updated timeline."
- **Customer-facing (damage/loss):** Empathetic, action-oriented. Lead with the resolution, not the problem. "We've identified an issue with your shipment and have already initiated [replacement/credit]."

### Key Templates

Brief templates below. Full versions with variables in [communication-templates.md](references/communication-templates.md).

**Initial carrier inquiry:** Subject: `Exception Notice — PRO# {pro} / BOL# {bol}`. State: what happened, what you need (ETA update, inspection, OS&D report), and by when.

**Customer proactive update:** Lead with: what you know, what you're doing about it, what the customer's revised timeline is, and your direct contact for questions.

**Escalation to carrier management:** Subject: `ESCALATION: Unresolved Exception — {shipment_ref} — {days} Days`. Include timeline of previous communications, financial impact, and what resolution you expect.

## Escalation Protocols

### Automatic Escalation Triggers

| Trigger                                    | Action                                         | Timeline          |
| ------------------------------------------ | ---------------------------------------------- | ----------------- |
| Exception value > $25,000                  | Notify VP Supply Chain immediately             | Within 1 hour     |
| Enterprise customer affected               | Assign dedicated handler, notify account team  | Within 2 hours    |
| Carrier non-response                       | Escalate to carrier account manager            | After 4 hours     |
| Repeated carrier (3+ in 30 days)           | Carrier performance review with procurement    | Within 1 week     |
| Potential fraud indicators                 | Notify compliance and halt standard processing | Immediately       |
| Temperature excursion on regulated product | Notify quality/regulatory team                 | Within 30 minutes |
| No scan update on high-value (> $50K)      | Initiate trace protocol and notify security    | After 24 hours    |
| Claims denied > $10,000                    | Legal review of denial basis                   | Within 48 hours   |

### Escalation Chain

Level 1 (Analyst) → Level 2 (Team Lead, 4 hours) → Level 3 (Manager, 24 hours) → Level 4 (Director, 48 hours) → Level 5 (VP, 72+ hours or any Level 5 severity)

## Performance Indicators

Track these metrics weekly and trend monthly:

| Metric                                 | Target              | Red Flag      |
| -------------------------------------- | ------------------- | ------------- |
| Mean resolution time                   | < 72 hours          | > 120 hours   |
| First-contact resolution rate          | > 40%               | < 25%         |
| Financial recovery rate (claims)       | > 75%               | < 50%         |
| Customer satisfaction (post-exception) | > 4.0/5.0           | < 3.5/5.0     |
| Exception rate (per 1,000 shipments)   | < 25                | > 40          |
| Claims filing timeliness               | 100% within 30 days | Any > 60 days |
| Repeat exceptions (same carrier/lane)  | < 10%               | > 20%         |
| Aged exceptions (> 30 days open)       | < 5% of total       | > 15%         |

## Additional Resources

- For detailed decision frameworks, escalation matrices, and mode-specific workflows, see [decision-frameworks.md](references/decision-frameworks.md)
- For the comprehensive edge case library with full analysis, see [edge-cases.md](references/edge-cases.md)
- For complete communication templates with variables and tone guidance, see [communication-templates.md](references/communication-templates.md)

## When to Use

Use this skill when you need to **triage and resolve logistics exceptions or design exception-handling playbooks**:

- Handling delays, damages, shortages, misdeliveries, and claims across LTL, FTL, parcel, intermodal, ocean, or air.
- Defining escalation rules, severity classification, and “eat‑the‑cost vs fight‑the‑claim” thresholds for your network.
- Building SOPs, dashboards, or automation for OS&D, claims workflows, and customer communications during freight disruptions.

---

## Merged Reference (legacy variant)

---
name: inventory-demand-planning
description: Codified expertise for demand forecasting, safety stock optimisation, replenishment planning, and promotional lift estimation at multi-location retailers.
risk: safe
source: https://github.com/ai-evos/agent-skills
date_added: '2026-02-27'
---

## When to Use

Use this skill when forecasting product demand, calculating optimal safety stock levels, planning inventory replenishment cycles, estimating the impact of retail promotions, or conducting ABC/XYZ inventory segmentation.

# Inventory Demand Planning

## Role and Context

You are a senior demand planner at a multi-location retailer operating 40–200 stores with regional distribution centers. You manage 300–800 active SKUs across categories including grocery, general merchandise, seasonal, and promotional assortments. Your systems include a demand planning suite (Blue Yonder, Oracle Demantra, or Kinaxis), an ERP (SAP, Oracle), a WMS for DC-level inventory, POS data feeds at the store level, and vendor portals for purchase order management. You sit between merchandising (which decides what to sell and at what price), supply chain (which manages warehouse capacity and transportation), and finance (which sets inventory investment budgets and GMROI targets). Your job is to translate commercial intent into executable purchase orders while minimizing both stockouts and excess inventory.

## Core Knowledge

### Forecasting Methods and When to Use Each

**Moving Averages (simple, weighted, trailing):** Use for stable-demand, low-variability items where recent history is a reliable predictor. A 4-week simple moving average works for commodity staples. Weighted moving averages (heavier on recent weeks) work better when demand is stable but shows slight drift. Never use moving averages on seasonal items — they lag trend changes by half the window length.

**Exponential Smoothing (single, double, triple):** Single exponential smoothing (SES, alpha 0.1–0.3) suits stationary demand with noise. Double exponential smoothing (Holt's) adds trend tracking — use for items with consistent growth or decline. Triple exponential smoothing (Holt-Winters) adds seasonal indices — this is the workhorse for seasonal items with 52-week or 12-month cycles. The alpha/beta/gamma parameters are critical: high alpha (>0.3) chases noise in volatile items; low alpha (<0.1) responds too slowly to regime changes. Optimize on holdout data, never on the same data used for fitting.

**Seasonal Decomposition (STL, classical, X-13ARIMA-SEATS):** When you need to isolate trend, seasonal, and residual components separately. STL (Seasonal and Trend decomposition using Loess) is robust to outliers. Use seasonal decomposition when seasonal patterns are shifting year over year, when you need to remove seasonality before applying a different model to the de-seasonalized data, or when building promotional lift estimates on top of a clean baseline.

**Causal/Regression Models:** When external factors drive demand beyond the item's own history — price elasticity, promotional flags, weather, competitor actions, local events. The practical challenge is feature engineering: promotional flags should encode depth (% off), display type, circular feature, and cross-category promo presence. Overfitting on sparse promo history is the single biggest pitfall. Regularize aggressively (Lasso/Ridge) and validate on out-of-time, not out-of-sample.

**Machine Learning (gradient boosting, neural nets):** Justified when you have large data (1,000+ SKUs × 2+ years of weekly history), multiple external regressors, and an ML engineering team. LightGBM/XGBoost with proper feature engineering outperforms simpler methods by 10–20% WAPE on promotional and intermittent items. But they require continuous monitoring — model drift in retail is real and quarterly retraining is the minimum.

### Forecast Accuracy Metrics

- **MAPE (Mean Absolute Percentage Error):** Standard metric but breaks on low-volume items (division by near-zero actuals produces inflated percentages). Use only for items averaging 50+ units/week.
- **Weighted MAPE (WMAPE):** Sum of absolute errors divided by sum of actuals. Prevents low-volume items from dominating the metric. This is the metric finance cares about because it reflects dollars.
- **Bias:** Average signed error. Positive bias = forecast systematically too high (overstock risk). Negative bias = systematically too low (stockout risk). Bias < ±5% is healthy. Bias > 10% in either direction means a structural problem in the model, not noise.
- **Tracking Signal:** Cumulative error divided by MAD (mean absolute deviation). When tracking signal exceeds ±4, the model has drifted and needs intervention — either re-parameterize or switch methods.

### Safety Stock Calculation

The textbook formula is `SS = Z × σ_d × √(LT + RP)` where Z is the service level z-score, σ_d is the standard deviation of demand per period, LT is lead time in periods, and RP is review period in periods. In practice, this formula works only for normally distributed, stationary demand.

**Service Level Targets:** 95% service level (Z=1.65) is standard for A-items. 99% (Z=2.33) for critical/A+ items where stockout cost dwarfs holding cost. 90% (Z=1.28) is acceptable for C-items. Moving from 95% to 99% nearly doubles safety stock — always quantify the inventory investment cost of the incremental service level before committing.

**Lead Time Variability:** When vendor lead times are uncertain, use `SS = Z × √(LT_avg × σ_d² + d_avg² × σ_LT²)` — this captures both demand variability and lead time variability. Vendors with coefficient of variation (CV) on lead time > 0.3 need safety stock adjustments that can be 40–60% higher than demand-only formulas suggest.

**Lumpy/Intermittent Demand:** Normal-distribution safety stock fails for items with many zero-demand periods. Use Croston's method for forecasting intermittent demand (separate forecasts for demand interval and demand size), and compute safety stock using a bootstrapped demand distribution rather than analytical formulas.

**New Products:** No demand history means no σ_d. Use analogous item profiling — find the 3–5 most similar items at the same lifecycle stage and use their demand variability as a proxy. Add a 20–30% buffer for the first 8 weeks, then taper as own history accumulates.

### Reorder Logic

**Inventory Position:** `IP = On-Hand + On-Order − Backorders − Committed (allocated to open customer orders)`. Never reorder based on on-hand alone — you will double-order when POs are in transit.

**Min/Max:** Simple, suitable for stable-demand items with consistent lead times. Min = average demand during lead time + safety stock. Max = Min + EOQ. When IP drops to Min, order up to Max. The weakness: it doesn't adapt to changing demand patterns without manual adjustment.

**Reorder Point / EOQ:** ROP = average demand during lead time + safety stock. EOQ = √(2DS/H) where D = annual demand, S = ordering cost, H = holding cost per unit per year. EOQ is theoretically optimal for constant demand, but in practice you round to vendor case packs, layer quantities, or pallet tiers. A "perfect" EOQ of 847 units means nothing if the vendor ships in cases of 24.

**Periodic Review (R,S):** Review inventory every R periods, order up to target level S. Better when you consolidate orders to a vendor on fixed days (e.g., Tuesday orders for Thursday pickup). R is set by vendor delivery schedule; S = average demand during (R + LT) + safety stock for that combined period.

**Vendor Tier-Based Frequencies:** A-vendors (top 10 by spend) get weekly review cycles. B-vendors (next 20) get bi-weekly. C-vendors (remaining) get monthly. This aligns review effort with financial impact and allows consolidation discounts.

### Promotional Planning

**Demand Signal Distortion:** Promotions create artificial demand peaks that contaminate baseline forecasting. Strip promotional volume from history before fitting baseline models. Keep a separate "promotional lift" layer that applies multiplicatively on top of the baseline during promo weeks.

**Lift Estimation Methods:** (1) Year-over-year comparison of promoted vs. non-promoted periods for the same item. (2) Cross-elasticity model using historical promo depth, display type, and media support as inputs. (3) Analogous item lift — new items borrow lift profiles from similar items in the same category that have been promoted before. Typical lifts: 15–40% for TPR (temporary price reduction) only, 80–200% for TPR + display + circular feature, 300–500%+ for doorbuster/loss-leader events.

**Cannibalization:** When SKU A is promoted, SKU B (same category, similar price point) loses volume. Estimate cannibalization at 10–30% of lifted volume for close substitutes. Ignore cannibalization across categories unless the promo is a traffic driver that shifts basket composition.

**Forward-Buy Calculation:** Customers stock up during deep promotions, creating a post-promo dip. The dip duration correlates with product shelf life and promotional depth. A 30% off promotion on a pantry item with 12-month shelf life creates a 2–4 week dip as households consume stockpiled units. A 15% off promotion on a perishable produces almost no dip.

**Post-Promo Dip:** Expect 1–3 weeks of below-baseline demand after a major promotion. The dip magnitude is typically 30–50% of the incremental lift, concentrated in the first week post-promo. Failing to forecast the dip leads to excess inventory and markdowns.

### ABC/XYZ Classification

**ABC (Value):** A = top 20% of SKUs driving 80% of revenue/margin. B = next 30% driving 15%. C = bottom 50% driving 5%. Classify on margin contribution, not revenue, to avoid overinvesting in high-revenue low-margin items.

**XYZ (Predictability):** X = CV of demand < 0.5 (highly predictable). Y = CV 0.5–1.0 (moderately predictable). Z = CV > 1.0 (erratic/lumpy). Compute on de-seasonalized, de-promoted demand to avoid penalizing seasonal items that are actually predictable within their pattern.

**Policy Matrix:** AX items get automated replenishment with tight safety stock. AZ items need human review every cycle — they're high-value but erratic. CX items get automated replenishment with generous review periods. CZ items are candidates for discontinuation or make-to-order conversion.

### Seasonal Transition Management

**Buy Timing:** Seasonal buys (e.g., holiday, summer, back-to-school) are committed 12–20 weeks before selling season. Allocate 60–70% of expected season demand in the initial buy, reserving 30–40% for reorder based on early-season sell-through. This "open-to-buy" reserve is your hedge against forecast error.

**Markdown Timing:** Begin markdowns when sell-through pace drops below 60% of plan at the season midpoint. Early shallow markdowns (20–30% off) recover more margin than late deep markdowns (50–70% off). The rule of thumb: every week of delay in markdown initiation costs 3–5 percentage points of margin on the remaining inventory.

**Season-End Liquidation:** Set a hard cutoff date (typically 2–3 weeks before the next season's product arrives). Everything remaining at cutoff goes to outlet, liquidator, or donation. Holding seasonal product into the next year rarely works — style items date, and warehousing cost erodes any margin recovery from selling next season.

## Decision Frameworks

### Forecast Method Selection by Demand Pattern

| Demand Pattern                                  | Primary Method                                                          | Fallback Method                           | Review Trigger                                        |
| ----------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------- | ----------------------------------------------------- |
| Stable, high-volume, no seasonality             | Weighted moving average (4–8 weeks)                                     | Single exponential smoothing              | WMAPE > 25% for 4 consecutive weeks                   |
| Trending (growth or decline)                    | Holt's double exponential smoothing                                     | Linear regression on recent 26 weeks      | Tracking signal exceeds ±4                            |
| Seasonal, repeating pattern                     | Holt-Winters (multiplicative for growing seasonal, additive for stable) | STL decomposition + SES on residual       | Season-over-season pattern correlation < 0.7          |
| Intermittent / lumpy (>30% zero-demand periods) | Croston's method or SBA (Syntetos-Boylan Approximation)                 | Bootstrap simulation on demand intervals  | Mean inter-demand interval shifts by >30%             |
| Promotion-driven                                | Causal regression (baseline + promo lift layer)                         | Analogous item lift + baseline            | Post-promo actuals deviate >40% from forecast         |
| New product (0–12 weeks history)                | Analogous item profile with lifecycle curve                             | Category average with decay toward actual | Own-data WMAPE stabilizes below analogous-based WMAPE |
| Event-driven (weather, local events)            | Regression with external regressors                                     | Manual override with documented rationale |                                                       |

### Safety Stock Service Level Selection

| Segment                               | Target Service Level | Z-Score   | Rationale                                                                                    |
| ------------------------------------- | -------------------- | --------- | -------------------------------------------------------------------------------------------- |
| AX (high-value, predictable)          | 97.5%                | 1.96      | High value justifies investment; low variability keeps SS moderate                           |
| AY (high-value, moderate variability) | 95%                  | 1.65      | Standard target; variability makes higher SL prohibitively expensive                         |
| AZ (high-value, erratic)              | 92–95%               | 1.41–1.65 | Erratic demand makes high SL astronomically expensive; supplement with expediting capability |
| BX/BY                                 | 95%                  | 1.65      | Standard target                                                                              |
| BZ                                    | 90%                  | 1.28      | Accept some stockout risk on mid-tier erratic items                                          |
| CX/CY                                 | 90–92%               | 1.28–1.41 | Low value doesn't justify high SS investment                                                 |
| CZ                                    | 85%                  | 1.04      | Candidate for discontinuation; minimal investment                                            |

### Promotional Lift Decision Framework

1. **Is there historical lift data for this SKU-promo type combination?** → Use own-item lift with recency weighting (most recent 3 promos weighted 50/30/20).
2. **No own-item data but same category has been promoted?** → Use analogous item lift adjusted for price point and brand tier.
3. **Brand-new category or promo type?** → Use conservative category-average lift discounted 20%. Build in a wider safety stock buffer for the promo period.
4. **Cross-promoted with another category?** → Model the traffic driver separately from the cross-promo beneficiary. Apply cross-elasticity coefficient if available; default 0.15 lift for cross-category halo.
5. **Always model the post-promo dip.** Default to 40% of incremental lift, concentrated 60/30/10 across the three post-promo weeks.

### Markdown Timing Decision

| Sell-Through at Season Midpoint | Action                                                                               | Expected Margin Recovery  |
| ------------------------------- | ------------------------------------------------------------------------------------ | ------------------------- |
| ≥ 80% of plan                   | Hold price. Reorder cautiously if weeks of supply < 3.                               | Full margin               |
| 60–79% of plan                  | Take 20–25% markdown. No reorder.                                                    | 70–80% of original margin |
| 40–59% of plan                  | Take 30–40% markdown immediately. Cancel any open POs.                               | 50–65% of original margin |
| < 40% of plan                   | Take 50%+ markdown. Explore liquidation channels. Flag buying error for post-mortem. | 30–45% of original margin |

### Slow-Mover Kill Decision

Evaluate quarterly. Flag for discontinuation when ALL of the following are true:

- Weeks of supply > 26 at current sell-through rate
- Last 13-week sales velocity < 50% of the item's first 13 weeks (lifecycle declining)
- No promotional activity planned in the next 8 weeks
- Item is not contractually obligated (planogram commitment, vendor agreement)
- Replacement or substitution SKU exists or category can absorb the gap

If flagged, initiate markdown at 30% off for 4 weeks. If still not moving, escalate to 50% off or liquidation. Set a hard exit date 8 weeks from first markdown. Do not allow slow movers to linger indefinitely in the assortment — they consume shelf space, warehouse slots, and working capital.

## Key Edge Cases

Brief summaries here. Full analysis in [edge-cases.md](references/edge-cases.md).

1. **New product launch with zero history:** Analogous item profiling is your only tool. Select analogs carefully — match on price point, category, brand tier, and target demographic, not just product type. Commit a conservative initial buy (60% of analog-based forecast) and build in weekly auto-replenishment triggers.

2. **Viral social media spike:** Demand jumps 500–2,000% with no warning. Do not chase — by the time your supply chain responds (4–8 week lead times), the spike is over. Capture what you can from existing inventory, issue allocation rules to prevent a single location from hoarding, and let the wave pass. Revise the baseline only if sustained demand persists 4+ weeks post-spike.

3. **Supplier lead time doubling overnight:** Recalculate safety stock immediately using the new lead time. If SS doubles, you likely cannot fill the gap from current inventory. Place an emergency order for the delta, negotiate partial shipments, and identify secondary suppliers. Communicate to merchandising that service levels will temporarily drop.

4. **Cannibalization from an unplanned promotion:** A competitor or another department runs an unplanned promo that steals volume from your category. Your forecast will over-project. Detect early by monitoring daily POS for a pattern break, then manually override the forecast downward. Defer incoming orders if possible.

5. **Demand pattern regime change:** An item that was stable-seasonal suddenly shifts to trending or erratic. Common after a reformulation, packaging change, or competitor entry/exit. The old model will fail silently. Monitor tracking signal weekly — when it exceeds ±4 for two consecutive periods, trigger a model re-selection.

6. **Phantom inventory:** WMS says you have 200 units; physical count reveals 40. Every forecast and replenishment decision based on that phantom inventory is wrong. Suspect phantom inventory when service level drops despite "adequate" on-hand. Conduct cycle counts on any item with stockouts that the system says shouldn't have occurred.

7. **Vendor MOQ conflicts:** Your EOQ says order 150 units; the vendor's minimum order quantity is 500. You either over-order (accepting weeks of excess inventory) or negotiate. Options: consolidate with other items from the same vendor to meet dollar minimums, negotiate a lower MOQ for this SKU, or accept the overage if holding cost is lower than ordering from an alternative supplier.

8. **Holiday calendar shift effects:** When key selling holidays shift position in the calendar (e.g., Easter moves between March and April), week-over-week comparisons break. Align forecasts to "weeks relative to holiday" rather than calendar weeks. A failure to account for Easter shifting from Week 13 to Week 16 will create significant forecast error in both years.

## Communication Patterns

### Tone Calibration

- **Vendor routine reorder:** Transactional, brief, PO-reference-driven. "PO #XXXX for delivery week of MM/DD per our agreed schedule."
- **Vendor lead time escalation:** Firm, fact-based, quantifies business impact. "Our analysis shows your lead time has increased from 14 to 22 days over the past 8 weeks. This has resulted in X stockout events. We need a corrective plan by [date]."
- **Internal stockout alert:** Urgent, actionable, includes estimated revenue at risk. Lead with the customer impact, not the inventory metric. "SKU X will stock out at 12 locations by Thursday. Estimated lost sales: $XX,000. Recommended action: [expedite/reallocate/substitute]."
- **Markdown recommendation to merchandising:** Data-driven, includes margin impact analysis. Never frame it as "we bought too much" — frame as "sell-through pace requires price action to meet margin targets."
- **Promotional forecast submission:** Structured, with baseline, lift, and post-promo dip called out separately. Include assumptions and confidence range. "Baseline: 500 units/week. Promotional lift estimate: 180% (900 incremental). Post-promo dip: −35% for 2 weeks. Confidence: ±25%."
- **New product forecast assumptions:** Document every assumption explicitly so it can be audited at post-mortem. "Based on analogs [list], we project 200 units/week in weeks 1–4, declining to 120 units/week by week 8. Assumptions: price point $X, distribution to 80 doors, no competitive launch in window."

Brief templates above. Full versions with variables in [communication-templates.md](references/communication-templates.md).

## Escalation Protocols

### Automatic Escalation Triggers

| Trigger                                               | Action                                                 | Timeline                   |
| ----------------------------------------------------- | ------------------------------------------------------ | -------------------------- |
| Projected stockout on A-item within 7 days            | Alert demand planning manager + category merchant      | Within 4 hours             |
| Vendor confirms lead time increase > 25%              | Notify supply chain director; recalculate all open POs | Within 1 business day      |
| Promotional forecast miss > 40% (over or under)       | Post-promo debrief with merchandising and vendor       | Within 1 week of promo end |
| Excess inventory > 26 weeks of supply on any A/B item | Markdown recommendation to merchandising VP            | Within 1 week of detection |
| Forecast bias exceeds ±10% for 4 consecutive weeks    | Model review and re-parameterization                   | Within 2 weeks             |
| New product sell-through < 40% of plan after 4 weeks  | Assortment review with merchandising                   | Within 1 week              |
| Service level drops below 90% for any category        | Root cause analysis and corrective plan                | Within 48 hours            |

### Escalation Chain

Level 1 (Demand Planner) → Level 2 (Planning Manager, 24 hours) → Level 3 (Director of Supply Chain Planning, 48 hours) → Level 4 (VP Supply Chain, 72+ hours or any A-item stockout at enterprise customer)

## Performance Indicators

Track weekly and trend monthly:

| Metric                                          | Target       | Red Flag            |
| ----------------------------------------------- | ------------ | ------------------- |
| WMAPE (weighted mean absolute percentage error) | < 25%        | > 35%               |
| Forecast bias                                   | ±5%          | > ±10% for 4+ weeks |
| In-stock rate (A-items)                         | > 97%        | < 94%               |
| In-stock rate (all items)                       | > 95%        | < 92%               |
| Weeks of supply (aggregate)                     | 4–8 weeks    | > 12 or < 3         |
| Excess inventory (>26 weeks supply)             | < 5% of SKUs | > 10% of SKUs       |
| Dead stock (zero sales, 13+ weeks)              | < 2% of SKUs | > 5% of SKUs        |
| Purchase order fill rate from vendors           | > 95%        | < 90%               |
| Promotional forecast accuracy (WMAPE)           | < 35%        | > 50%               |

## Additional Resources

- For detailed decision frameworks, optimization models, and method selection trees, see [decision-frameworks.md](references/decision-frameworks.md)
- For the comprehensive edge case library with full resolution playbooks, see [edge-cases.md](references/edge-cases.md)
- For complete communication templates with variables and tone guidance, see [communication-templates.md](references/communication-templates.md)

## When to Use

Use this skill when you need to **forecast demand and shape inventory policy across SKUs, stores, and vendors**:

- Selecting and tuning forecasting methods, safety stock policies, and reorder logic for different demand patterns.
- Planning promotions, seasonal transitions, markdowns, and end‑of‑life strategies while balancing service, cash, and margin.
- Investigating chronic stockouts, excess inventory, or forecast bias and redesigning the planning process with clearer decision frameworks.

---

## Merged Reference (legacy variant)

---
name: odoo-inventory-optimizer
description: "Expert guide for Odoo Inventory: stock valuation (FIFO/AVCO), reordering rules, putaway strategies, routes, and multi-warehouse configuration."
risk: safe
source: "self"
---

# Odoo Inventory Optimizer

## Overview

This skill helps you configure and optimize Odoo Inventory for accuracy, efficiency, and traceability. It covers stock valuation methods, reordering rules, putaway strategies, warehouse routes, and multi-step flows (receive → quality → store).

## When to Use This Skill

- Choosing and configuring FIFO vs AVCO stock valuation.
- Setting up minimum stock reordering rules to avoid stockouts.
- Designing a multi-step warehouse flow (2-step receipt, 3-step delivery).
- Configuring putaway rules to direct products to specific storage locations.
- Troubleshooting negative stock, incorrect valuation, or missing moves.

## How It Works

1. **Activate**: Mention `@odoo-inventory-optimizer` and describe your warehouse scenario.
2. **Configure**: Receive step-by-step configuration instructions with exact Odoo menu paths.
3. **Optimize**: Get recommendations for reordering rules and stock accuracy improvements.

## Examples

### Example 1: Enable FIFO Stock Valuation

```text
Menu: Inventory → Configuration → Settings

Enable: Storage Locations
Enable: Multi-Step Routes
Costing Method: (set per Product Category, not globally)

Menu: Inventory → Configuration → Product Categories → Edit

  Category: All / Physical Goods
  Costing Method: First In First Out (FIFO)
  Inventory Valuation: Automated
  Account Stock Valuation: [Balance Sheet inventory account]
  Account Stock Input:   [Stock Received Not Billed]
  Account Stock Output:  [Stock Delivered Not Invoiced]
```

### Example 2: Set Up a Min/Max Reordering Rule

```text
Menu: Inventory → Operations → Replenishment → New

Product: Office Paper A4
Location: WH/Stock
Min Qty: 100   (trigger reorder when stock falls below this)
Max Qty: 500   (purchase up to this quantity)
Multiple Qty: 50  (always order in multiples of 50)
Route: Buy    (triggers a Purchase Order automatically)
       or Manufacture (triggers a Manufacturing Order)
```

### Example 3: Configure Putaway Rules

```text
Menu: Inventory → Configuration → Putaway Rules → New

Purpose: Direct products from WH/Input to specific bin locations

Rules:
  Product Category: Refrigerated Goods
    → Location: WH/Stock/Cold Storage

  Product: Laptop Model X
    → Location: WH/Stock/Electronics/Shelf A

  (leave Product blank to apply the rule to an entire category)

Result: When a receipt is validated, Odoo automatically suggests
the correct destination location per product or category.
```

### Example 4: Configure 3-Step Warehouse Delivery

```text
Menu: Inventory → Configuration → Warehouses → [Your Warehouse]

Outgoing Shipments: Pick + Pack + Ship (3 steps)

Operations created automatically:
  PICK  — Move goods from storage shelf to packing area
  PACK  — Package items and print shipping label
  OUT   — Hand off to carrier / mark as shipped
```

## Best Practices

- ✅ **Do:** Use **Lots/Serial Numbers** for high-value or regulated items (medical devices, electronics).
- ✅ **Do:** Run a **physical inventory adjustment** at least quarterly (Inventory → Operations → Physical Inventory) to correct drift.
- ✅ **Do:** Set reordering rules on fast-moving items so purchase orders are generated automatically.
- ✅ **Do:** Enable **Putaway Rules** on warehouses with multiple storage zones — it eliminates manual location selection errors.
- ❌ **Don't:** Switch stock valuation method (FIFO ↔ AVCO) after recording transactions — it produces incorrect historical cost data.
- ❌ **Don't:** Use "Update Quantity" to fix stock errors — always use Inventory Adjustments to maintain a proper audit trail.
- ❌ **Don't:** Mix product categories with different costing methods in the same storage location without understanding the valuation impact.

## Limitations

- **Serial number tracking** at the individual unit level (SN per line) adds significant UI overhead; test performance with large volumes before enabling.
- Does not cover **landed costs** (import duties, freight allocation to product cost) — that requires the `stock_landed_costs` module.
- **Cross-warehouse stock transfers** have routing complexities (transit locations, intercompany invoicing) not fully covered here.
- Automated inventory valuation requires the **Accounting** module; Community Edition installations without it cannot post stock journal entries.

## Source: references/skills/logistics-exception-management/references/legacy/inventory-demand-planning/SKILL.md

---
name: inventory-demand-planning
description: Codified expertise for demand forecasting, safety stock optimisation, replenishment planning, and promotional lift estimation at multi-location retailers.
risk: safe
source: https://github.com/ai-evos/agent-skills
date_added: '2026-02-27'
---

## When to Use

Use this skill when forecasting product demand, calculating optimal safety stock levels, planning inventory replenishment cycles, estimating the impact of retail promotions, or conducting ABC/XYZ inventory segmentation.

# Inventory Demand Planning

## Role and Context

You are a senior demand planner at a multi-location retailer operating 40–200 stores with regional distribution centers. You manage 300–800 active SKUs across categories including grocery, general merchandise, seasonal, and promotional assortments. Your systems include a demand planning suite (Blue Yonder, Oracle Demantra, or Kinaxis), an ERP (SAP, Oracle), a WMS for DC-level inventory, POS data feeds at the store level, and vendor portals for purchase order management. You sit between merchandising (which decides what to sell and at what price), supply chain (which manages warehouse capacity and transportation), and finance (which sets inventory investment budgets and GMROI targets). Your job is to translate commercial intent into executable purchase orders while minimizing both stockouts and excess inventory.

## Core Knowledge

### Forecasting Methods and When to Use Each

**Moving Averages (simple, weighted, trailing):** Use for stable-demand, low-variability items where recent history is a reliable predictor. A 4-week simple moving average works for commodity staples. Weighted moving averages (heavier on recent weeks) work better when demand is stable but shows slight drift. Never use moving averages on seasonal items — they lag trend changes by half the window length.

**Exponential Smoothing (single, double, triple):** Single exponential smoothing (SES, alpha 0.1–0.3) suits stationary demand with noise. Double exponential smoothing (Holt's) adds trend tracking — use for items with consistent growth or decline. Triple exponential smoothing (Holt-Winters) adds seasonal indices — this is the workhorse for seasonal items with 52-week or 12-month cycles. The alpha/beta/gamma parameters are critical: high alpha (>0.3) chases noise in volatile items; low alpha (<0.1) responds too slowly to regime changes. Optimize on holdout data, never on the same data used for fitting.

**Seasonal Decomposition (STL, classical, X-13ARIMA-SEATS):** When you need to isolate trend, seasonal, and residual components separately. STL (Seasonal and Trend decomposition using Loess) is robust to outliers. Use seasonal decomposition when seasonal patterns are shifting year over year, when you need to remove seasonality before applying a different model to the de-seasonalized data, or when building promotional lift estimates on top of a clean baseline.

**Causal/Regression Models:** When external factors drive demand beyond the item's own history — price elasticity, promotional flags, weather, competitor actions, local events. The practical challenge is feature engineering: promotional flags should encode depth (% off), display type, circular feature, and cross-category promo presence. Overfitting on sparse promo history is the single biggest pitfall. Regularize aggressively (Lasso/Ridge) and validate on out-of-time, not out-of-sample.

**Machine Learning (gradient boosting, neural nets):** Justified when you have large data (1,000+ SKUs × 2+ years of weekly history), multiple external regressors, and an ML engineering team. LightGBM/XGBoost with proper feature engineering outperforms simpler methods by 10–20% WAPE on promotional and intermittent items. But they require continuous monitoring — model drift in retail is real and quarterly retraining is the minimum.

### Forecast Accuracy Metrics

- **MAPE (Mean Absolute Percentage Error):** Standard metric but breaks on low-volume items (division by near-zero actuals produces inflated percentages). Use only for items averaging 50+ units/week.
- **Weighted MAPE (WMAPE):** Sum of absolute errors divided by sum of actuals. Prevents low-volume items from dominating the metric. This is the metric finance cares about because it reflects dollars.
- **Bias:** Average signed error. Positive bias = forecast systematically too high (overstock risk). Negative bias = systematically too low (stockout risk). Bias < ±5% is healthy. Bias > 10% in either direction means a structural problem in the model, not noise.
- **Tracking Signal:** Cumulative error divided by MAD (mean absolute deviation). When tracking signal exceeds ±4, the model has drifted and needs intervention — either re-parameterize or switch methods.

### Safety Stock Calculation

The textbook formula is `SS = Z × σ_d × √(LT + RP)` where Z is the service level z-score, σ_d is the standard deviation of demand per period, LT is lead time in periods, and RP is review period in periods. In practice, this formula works only for normally distributed, stationary demand.

**Service Level Targets:** 95% service level (Z=1.65) is standard for A-items. 99% (Z=2.33) for critical/A+ items where stockout cost dwarfs holding cost. 90% (Z=1.28) is acceptable for C-items. Moving from 95% to 99% nearly doubles safety stock — always quantify the inventory investment cost of the incremental service level before committing.

**Lead Time Variability:** When vendor lead times are uncertain, use `SS = Z × √(LT_avg × σ_d² + d_avg² × σ_LT²)` — this captures both demand variability and lead time variability. Vendors with coefficient of variation (CV) on lead time > 0.3 need safety stock adjustments that can be 40–60% higher than demand-only formulas suggest.

**Lumpy/Intermittent Demand:** Normal-distribution safety stock fails for items with many zero-demand periods. Use Croston's method for forecasting intermittent demand (separate forecasts for demand interval and demand size), and compute safety stock using a bootstrapped demand distribution rather than analytical formulas.

**New Products:** No demand history means no σ_d. Use analogous item profiling — find the 3–5 most similar items at the same lifecycle stage and use their demand variability as a proxy. Add a 20–30% buffer for the first 8 weeks, then taper as own history accumulates.

### Reorder Logic

**Inventory Position:** `IP = On-Hand + On-Order − Backorders − Committed (allocated to open customer orders)`. Never reorder based on on-hand alone — you will double-order when POs are in transit.

**Min/Max:** Simple, suitable for stable-demand items with consistent lead times. Min = average demand during lead time + safety stock. Max = Min + EOQ. When IP drops to Min, order up to Max. The weakness: it doesn't adapt to changing demand patterns without manual adjustment.

**Reorder Point / EOQ:** ROP = average demand during lead time + safety stock. EOQ = √(2DS/H) where D = annual demand, S = ordering cost, H = holding cost per unit per year. EOQ is theoretically optimal for constant demand, but in practice you round to vendor case packs, layer quantities, or pallet tiers. A "perfect" EOQ of 847 units means nothing if the vendor ships in cases of 24.

**Periodic Review (R,S):** Review inventory every R periods, order up to target level S. Better when you consolidate orders to a vendor on fixed days (e.g., Tuesday orders for Thursday pickup). R is set by vendor delivery schedule; S = average demand during (R + LT) + safety stock for that combined period.

**Vendor Tier-Based Frequencies:** A-vendors (top 10 by spend) get weekly review cycles. B-vendors (next 20) get bi-weekly. C-vendors (remaining) get monthly. This aligns review effort with financial impact and allows consolidation discounts.

### Promotional Planning

**Demand Signal Distortion:** Promotions create artificial demand peaks that contaminate baseline forecasting. Strip promotional volume from history before fitting baseline models. Keep a separate "promotional lift" layer that applies multiplicatively on top of the baseline during promo weeks.

**Lift Estimation Methods:** (1) Year-over-year comparison of promoted vs. non-promoted periods for the same item. (2) Cross-elasticity model using historical promo depth, display type, and media support as inputs. (3) Analogous item lift — new items borrow lift profiles from similar items in the same category that have been promoted before. Typical lifts: 15–40% for TPR (temporary price reduction) only, 80–200% for TPR + display + circular feature, 300–500%+ for doorbuster/loss-leader events.

**Cannibalization:** When SKU A is promoted, SKU B (same category, similar price point) loses volume. Estimate cannibalization at 10–30% of lifted volume for close substitutes. Ignore cannibalization across categories unless the promo is a traffic driver that shifts basket composition.

**Forward-Buy Calculation:** Customers stock up during deep promotions, creating a post-promo dip. The dip duration correlates with product shelf life and promotional depth. A 30% off promotion on a pantry item with 12-month shelf life creates a 2–4 week dip as households consume stockpiled units. A 15% off promotion on a perishable produces almost no dip.

**Post-Promo Dip:** Expect 1–3 weeks of below-baseline demand after a major promotion. The dip magnitude is typically 30–50% of the incremental lift, concentrated in the first week post-promo. Failing to forecast the dip leads to excess inventory and markdowns.

### ABC/XYZ Classification

**ABC (Value):** A = top 20% of SKUs driving 80% of revenue/margin. B = next 30% driving 15%. C = bottom 50% driving 5%. Classify on margin contribution, not revenue, to avoid overinvesting in high-revenue low-margin items.

**XYZ (Predictability):** X = CV of demand < 0.5 (highly predictable). Y = CV 0.5–1.0 (moderately predictable). Z = CV > 1.0 (erratic/lumpy). Compute on de-seasonalized, de-promoted demand to avoid penalizing seasonal items that are actually predictable within their pattern.

**Policy Matrix:** AX items get automated replenishment with tight safety stock. AZ items need human review every cycle — they're high-value but erratic. CX items get automated replenishment with generous review periods. CZ items are candidates for discontinuation or make-to-order conversion.

### Seasonal Transition Management

**Buy Timing:** Seasonal buys (e.g., holiday, summer, back-to-school) are committed 12–20 weeks before selling season. Allocate 60–70% of expected season demand in the initial buy, reserving 30–40% for reorder based on early-season sell-through. This "open-to-buy" reserve is your hedge against forecast error.

**Markdown Timing:** Begin markdowns when sell-through pace drops below 60% of plan at the season midpoint. Early shallow markdowns (20–30% off) recover more margin than late deep markdowns (50–70% off). The rule of thumb: every week of delay in markdown initiation costs 3–5 percentage points of margin on the remaining inventory.

**Season-End Liquidation:** Set a hard cutoff date (typically 2–3 weeks before the next season's product arrives). Everything remaining at cutoff goes to outlet, liquidator, or donation. Holding seasonal product into the next year rarely works — style items date, and warehousing cost erodes any margin recovery from selling next season.

## Decision Frameworks

### Forecast Method Selection by Demand Pattern

| Demand Pattern                                  | Primary Method                                                          | Fallback Method                           | Review Trigger                                        |
| ----------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------- | ----------------------------------------------------- |
| Stable, high-volume, no seasonality             | Weighted moving average (4–8 weeks)                                     | Single exponential smoothing              | WMAPE > 25% for 4 consecutive weeks                   |
| Trending (growth or decline)                    | Holt's double exponential smoothing                                     | Linear regression on recent 26 weeks      | Tracking signal exceeds ±4                            |
| Seasonal, repeating pattern                     | Holt-Winters (multiplicative for growing seasonal, additive for stable) | STL decomposition + SES on residual       | Season-over-season pattern correlation < 0.7          |
| Intermittent / lumpy (>30% zero-demand periods) | Croston's method or SBA (Syntetos-Boylan Approximation)                 | Bootstrap simulation on demand intervals  | Mean inter-demand interval shifts by >30%             |
| Promotion-driven                                | Causal regression (baseline + promo lift layer)                         | Analogous item lift + baseline            | Post-promo actuals deviate >40% from forecast         |
| New product (0–12 weeks history)                | Analogous item profile with lifecycle curve                             | Category average with decay toward actual | Own-data WMAPE stabilizes below analogous-based WMAPE |
| Event-driven (weather, local events)            | Regression with external regressors                                     | Manual override with documented rationale |                                                       |

### Safety Stock Service Level Selection

| Segment                               | Target Service Level | Z-Score   | Rationale                                                                                    |
| ------------------------------------- | -------------------- | --------- | -------------------------------------------------------------------------------------------- |
| AX (high-value, predictable)          | 97.5%                | 1.96      | High value justifies investment; low variability keeps SS moderate                           |
| AY (high-value, moderate variability) | 95%                  | 1.65      | Standard target; variability makes higher SL prohibitively expensive                         |
| AZ (high-value, erratic)              | 92–95%               | 1.41–1.65 | Erratic demand makes high SL astronomically expensive; supplement with expediting capability |
| BX/BY                                 | 95%                  | 1.65      | Standard target                                                                              |
| BZ                                    | 90%                  | 1.28      | Accept some stockout risk on mid-tier erratic items                                          |
| CX/CY                                 | 90–92%               | 1.28–1.41 | Low value doesn't justify high SS investment                                                 |
| CZ                                    | 85%                  | 1.04      | Candidate for discontinuation; minimal investment                                            |

### Promotional Lift Decision Framework

1. **Is there historical lift data for this SKU-promo type combination?** → Use own-item lift with recency weighting (most recent 3 promos weighted 50/30/20).
2. **No own-item data but same category has been promoted?** → Use analogous item lift adjusted for price point and brand tier.
3. **Brand-new category or promo type?** → Use conservative category-average lift discounted 20%. Build in a wider safety stock buffer for the promo period.
4. **Cross-promoted with another category?** → Model the traffic driver separately from the cross-promo beneficiary. Apply cross-elasticity coefficient if available; default 0.15 lift for cross-category halo.
5. **Always model the post-promo dip.** Default to 40% of incremental lift, concentrated 60/30/10 across the three post-promo weeks.

### Markdown Timing Decision

| Sell-Through at Season Midpoint | Action                                                                               | Expected Margin Recovery  |
| ------------------------------- | ------------------------------------------------------------------------------------ | ------------------------- |
| ≥ 80% of plan                   | Hold price. Reorder cautiously if weeks of supply < 3.                               | Full margin               |
| 60–79% of plan                  | Take 20–25% markdown. No reorder.                                                    | 70–80% of original margin |
| 40–59% of plan                  | Take 30–40% markdown immediately. Cancel any open POs.                               | 50–65% of original margin |
| < 40% of plan                   | Take 50%+ markdown. Explore liquidation channels. Flag buying error for post-mortem. | 30–45% of original margin |

### Slow-Mover Kill Decision

Evaluate quarterly. Flag for discontinuation when ALL of the following are true:

- Weeks of supply > 26 at current sell-through rate
- Last 13-week sales velocity < 50% of the item's first 13 weeks (lifecycle declining)
- No promotional activity planned in the next 8 weeks
- Item is not contractually obligated (planogram commitment, vendor agreement)
- Replacement or substitution SKU exists or category can absorb the gap

If flagged, initiate markdown at 30% off for 4 weeks. If still not moving, escalate to 50% off or liquidation. Set a hard exit date 8 weeks from first markdown. Do not allow slow movers to linger indefinitely in the assortment — they consume shelf space, warehouse slots, and working capital.

## Key Edge Cases

Brief summaries here. Full analysis in [edge-cases.md](references/edge-cases.md).

1. **New product launch with zero history:** Analogous item profiling is your only tool. Select analogs carefully — match on price point, category, brand tier, and target demographic, not just product type. Commit a conservative initial buy (60% of analog-based forecast) and build in weekly auto-replenishment triggers.

2. **Viral social media spike:** Demand jumps 500–2,000% with no warning. Do not chase — by the time your supply chain responds (4–8 week lead times), the spike is over. Capture what you can from existing inventory, issue allocation rules to prevent a single location from hoarding, and let the wave pass. Revise the baseline only if sustained demand persists 4+ weeks post-spike.

3. **Supplier lead time doubling overnight:** Recalculate safety stock immediately using the new lead time. If SS doubles, you likely cannot fill the gap from current inventory. Place an emergency order for the delta, negotiate partial shipments, and identify secondary suppliers. Communicate to merchandising that service levels will temporarily drop.

4. **Cannibalization from an unplanned promotion:** A competitor or another department runs an unplanned promo that steals volume from your category. Your forecast will over-project. Detect early by monitoring daily POS for a pattern break, then manually override the forecast downward. Defer incoming orders if possible.

5. **Demand pattern regime change:** An item that was stable-seasonal suddenly shifts to trending or erratic. Common after a reformulation, packaging change, or competitor entry/exit. The old model will fail silently. Monitor tracking signal weekly — when it exceeds ±4 for two consecutive periods, trigger a model re-selection.

6. **Phantom inventory:** WMS says you have 200 units; physical count reveals 40. Every forecast and replenishment decision based on that phantom inventory is wrong. Suspect phantom inventory when service level drops despite "adequate" on-hand. Conduct cycle counts on any item with stockouts that the system says shouldn't have occurred.

7. **Vendor MOQ conflicts:** Your EOQ says order 150 units; the vendor's minimum order quantity is 500. You either over-order (accepting weeks of excess inventory) or negotiate. Options: consolidate with other items from the same vendor to meet dollar minimums, negotiate a lower MOQ for this SKU, or accept the overage if holding cost is lower than ordering from an alternative supplier.

8. **Holiday calendar shift effects:** When key selling holidays shift position in the calendar (e.g., Easter moves between March and April), week-over-week comparisons break. Align forecasts to "weeks relative to holiday" rather than calendar weeks. A failure to account for Easter shifting from Week 13 to Week 16 will create significant forecast error in both years.

## Communication Patterns

### Tone Calibration

- **Vendor routine reorder:** Transactional, brief, PO-reference-driven. "PO #XXXX for delivery week of MM/DD per our agreed schedule."
- **Vendor lead time escalation:** Firm, fact-based, quantifies business impact. "Our analysis shows your lead time has increased from 14 to 22 days over the past 8 weeks. This has resulted in X stockout events. We need a corrective plan by [date]."
- **Internal stockout alert:** Urgent, actionable, includes estimated revenue at risk. Lead with the customer impact, not the inventory metric. "SKU X will stock out at 12 locations by Thursday. Estimated lost sales: $XX,000. Recommended action: [expedite/reallocate/substitute]."
- **Markdown recommendation to merchandising:** Data-driven, includes margin impact analysis. Never frame it as "we bought too much" — frame as "sell-through pace requires price action to meet margin targets."
- **Promotional forecast submission:** Structured, with baseline, lift, and post-promo dip called out separately. Include assumptions and confidence range. "Baseline: 500 units/week. Promotional lift estimate: 180% (900 incremental). Post-promo dip: −35% for 2 weeks. Confidence: ±25%."
- **New product forecast assumptions:** Document every assumption explicitly so it can be audited at post-mortem. "Based on analogs [list], we project 200 units/week in weeks 1–4, declining to 120 units/week by week 8. Assumptions: price point $X, distribution to 80 doors, no competitive launch in window."

Brief templates above. Full versions with variables in [communication-templates.md](references/communication-templates.md).

## Escalation Protocols

### Automatic Escalation Triggers

| Trigger                                               | Action                                                 | Timeline                   |
| ----------------------------------------------------- | ------------------------------------------------------ | -------------------------- |
| Projected stockout on A-item within 7 days            | Alert demand planning manager + category merchant      | Within 4 hours             |
| Vendor confirms lead time increase > 25%              | Notify supply chain director; recalculate all open POs | Within 1 business day      |
| Promotional forecast miss > 40% (over or under)       | Post-promo debrief with merchandising and vendor       | Within 1 week of promo end |
| Excess inventory > 26 weeks of supply on any A/B item | Markdown recommendation to merchandising VP            | Within 1 week of detection |
| Forecast bias exceeds ±10% for 4 consecutive weeks    | Model review and re-parameterization                   | Within 2 weeks             |
| New product sell-through < 40% of plan after 4 weeks  | Assortment review with merchandising                   | Within 1 week              |
| Service level drops below 90% for any category        | Root cause analysis and corrective plan                | Within 48 hours            |

### Escalation Chain

Level 1 (Demand Planner) → Level 2 (Planning Manager, 24 hours) → Level 3 (Director of Supply Chain Planning, 48 hours) → Level 4 (VP Supply Chain, 72+ hours or any A-item stockout at enterprise customer)

## Performance Indicators

Track weekly and trend monthly:

| Metric                                          | Target       | Red Flag            |
| ----------------------------------------------- | ------------ | ------------------- |
| WMAPE (weighted mean absolute percentage error) | < 25%        | > 35%               |
| Forecast bias                                   | ±5%          | > ±10% for 4+ weeks |
| In-stock rate (A-items)                         | > 97%        | < 94%               |
| In-stock rate (all items)                       | > 95%        | < 92%               |
| Weeks of supply (aggregate)                     | 4–8 weeks    | > 12 or < 3         |
| Excess inventory (>26 weeks supply)             | < 5% of SKUs | > 10% of SKUs       |
| Dead stock (zero sales, 13+ weeks)              | < 2% of SKUs | > 5% of SKUs        |
| Purchase order fill rate from vendors           | > 95%        | < 90%               |
| Promotional forecast accuracy (WMAPE)           | < 35%        | > 50%               |

## Additional Resources

- For detailed decision frameworks, optimization models, and method selection trees, see [decision-frameworks.md](references/decision-frameworks.md)
- For the comprehensive edge case library with full resolution playbooks, see [edge-cases.md](references/edge-cases.md)
- For complete communication templates with variables and tone guidance, see [communication-templates.md](references/communication-templates.md)

## When to Use

Use this skill when you need to **forecast demand and shape inventory policy across SKUs, stores, and vendors**:

- Selecting and tuning forecasting methods, safety stock policies, and reorder logic for different demand patterns.
- Planning promotions, seasonal transitions, markdowns, and end‑of‑life strategies while balancing service, cash, and margin.
- Investigating chronic stockouts, excess inventory, or forecast bias and redesigning the planning process with clearer decision frameworks.

## Source: references/skills/logistics-exception-management/references/legacy/odoo-inventory-optimizer/SKILL.md

---
name: odoo-inventory-optimizer
description: "Expert guide for Odoo Inventory: stock valuation (FIFO/AVCO), reordering rules, putaway strategies, routes, and multi-warehouse configuration."
risk: safe
source: "self"
---

# Odoo Inventory Optimizer

## Overview

This skill helps you configure and optimize Odoo Inventory for accuracy, efficiency, and traceability. It covers stock valuation methods, reordering rules, putaway strategies, warehouse routes, and multi-step flows (receive → quality → store).

## When to Use This Skill

- Choosing and configuring FIFO vs AVCO stock valuation.
- Setting up minimum stock reordering rules to avoid stockouts.
- Designing a multi-step warehouse flow (2-step receipt, 3-step delivery).
- Configuring putaway rules to direct products to specific storage locations.
- Troubleshooting negative stock, incorrect valuation, or missing moves.

## How It Works

1. **Activate**: Mention `@odoo-inventory-optimizer` and describe your warehouse scenario.
2. **Configure**: Receive step-by-step configuration instructions with exact Odoo menu paths.
3. **Optimize**: Get recommendations for reordering rules and stock accuracy improvements.

## Examples

### Example 1: Enable FIFO Stock Valuation

```text
Menu: Inventory → Configuration → Settings

Enable: Storage Locations
Enable: Multi-Step Routes
Costing Method: (set per Product Category, not globally)

Menu: Inventory → Configuration → Product Categories → Edit

  Category: All / Physical Goods
  Costing Method: First In First Out (FIFO)
  Inventory Valuation: Automated
  Account Stock Valuation: [Balance Sheet inventory account]
  Account Stock Input:   [Stock Received Not Billed]
  Account Stock Output:  [Stock Delivered Not Invoiced]
```

### Example 2: Set Up a Min/Max Reordering Rule

```text
Menu: Inventory → Operations → Replenishment → New

Product: Office Paper A4
Location: WH/Stock
Min Qty: 100   (trigger reorder when stock falls below this)
Max Qty: 500   (purchase up to this quantity)
Multiple Qty: 50  (always order in multiples of 50)
Route: Buy    (triggers a Purchase Order automatically)
       or Manufacture (triggers a Manufacturing Order)
```

### Example 3: Configure Putaway Rules

```text
Menu: Inventory → Configuration → Putaway Rules → New

Purpose: Direct products from WH/Input to specific bin locations

Rules:
  Product Category: Refrigerated Goods
    → Location: WH/Stock/Cold Storage

  Product: Laptop Model X
    → Location: WH/Stock/Electronics/Shelf A

  (leave Product blank to apply the rule to an entire category)

Result: When a receipt is validated, Odoo automatically suggests
the correct destination location per product or category.
```

### Example 4: Configure 3-Step Warehouse Delivery

```text
Menu: Inventory → Configuration → Warehouses → [Your Warehouse]

Outgoing Shipments: Pick + Pack + Ship (3 steps)

Operations created automatically:
  PICK  — Move goods from storage shelf to packing area
  PACK  — Package items and print shipping label
  OUT   — Hand off to carrier / mark as shipped
```

## Best Practices

- ✅ **Do:** Use **Lots/Serial Numbers** for high-value or regulated items (medical devices, electronics).
- ✅ **Do:** Run a **physical inventory adjustment** at least quarterly (Inventory → Operations → Physical Inventory) to correct drift.
- ✅ **Do:** Set reordering rules on fast-moving items so purchase orders are generated automatically.
- ✅ **Do:** Enable **Putaway Rules** on warehouses with multiple storage zones — it eliminates manual location selection errors.
- ❌ **Don't:** Switch stock valuation method (FIFO ↔ AVCO) after recording transactions — it produces incorrect historical cost data.
- ❌ **Don't:** Use "Update Quantity" to fix stock errors — always use Inventory Adjustments to maintain a proper audit trail.
- ❌ **Don't:** Mix product categories with different costing methods in the same storage location without understanding the valuation impact.

## Limitations

- **Serial number tracking** at the individual unit level (SN per line) adds significant UI overhead; test performance with large volumes before enabling.
- Does not cover **landed costs** (import duties, freight allocation to product cost) — that requires the `stock_landed_costs` module.
- **Cross-warehouse stock transfers** have routing complexities (transit locations, intercompany invoicing) not fully covered here.
- Automated inventory valuation requires the **Accounting** module; Community Edition installations without it cannot post stock journal entries.

