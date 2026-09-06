# Case Study: Workforce Budget Scenario Modeling

**Business Question:** How much would Nexora Analytics' total payroll and headcount change under different staffing strategies, and at what point does a scenario become significant enough to require executive sign-off?

**Method:** Built a dynamic scenario engine in Google Sheets covering four named strategies — Baseline, Growth, Cost-Cutting, and Hiring Freeze — plus a fully customizable mode. Each scenario models attrition, backfill hiring, new growth hires, and raises independently per department, then rolls up to a company-wide total with an automatic escalation flag at a ±5% variance threshold.

**Findings:**
- Baseline reproduces the current $9,267,829 payroll exactly, with zero variance — confirming the model's math is internally consistent before testing any real change.
- Growth (10% headcount growth, 3% raise, 8% attrition with backfill) increases payroll to $10,763,564 — a 16.1% increase, driven roughly equally by raises, backfill hiring, and new growth hires.
- Cost-Cutting (-5% headcount, 12% attrition, no backfill) reduces payroll to $7,685,786 — a 17.1% decrease.
- **The most interesting finding: Hiring Freeze — the most conservative-sounding scenario — still triggers escalation.** With zero growth and zero raises, natural attrition alone (10%, no backfill) drives a -10.0% swing. This means at Nexora's current size and attrition rate, doing *nothing* still produces a budget shift large enough to require sign-off under the current threshold — which raises a real question about whether ±5% is calibrated correctly for a company this size, or whether it would flag nearly every year as "exceptional."

**Recommendation:** Before using this model for real planning, Nexora's Finance team should revisit the escalation threshold specifically — the data suggests 5% may be too tight to distinguish routine attrition-driven fluctuation from genuinely exceptional strategic shifts.
