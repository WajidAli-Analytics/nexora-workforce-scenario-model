# Nexora Analytics — Workforce & Payroll Scenario Model

**Live model:** [View on Google Sheets](https://docs.google.com/spreadsheets/d/18LRWCKGLbaQPHjZbs7QNXLeh6NCCNRyrqeF8aVVdA7M/edit?usp=sharing)

## Business Problem
A company's Finance/HR team needs to model staffing budget under different scenarios (growth, freeze, cuts) before locking in next year's plan — replacing ad-hoc, disconnected spreadsheet recalculation with a single tool that shows budget impact instantly when an assumption changes.

## Objective
Give decision-makers a live model where switching one assumption (e.g., "grow headcount by 10%") instantly recalculates the full budget impact, with automatic flags for when a scenario is significant enough to need executive sign-off.

## Approach
Built entirely in Google Sheets: a dropdown-driven scenario engine (Baseline / Growth / Cost-Cutting / Hiring Freeze / Custom), a department-level calculation layer, a pivot table role breakdown, and a live dashboard — all fully dynamic, nothing hardcoded.

## Key Features
- **Scenario control panel** — pick a preset or manually override any assumption for a fully custom scenario
- **Backfill-vs-no-backfill attrition logic** — Growth/Baseline scenarios replace leavers (at 1.15x onboarding cost), Cost-Cutting/Hiring Freeze treat attrition as natural headcount reduction with no backfill — mirroring how real cost-cutting plans actually use attrition
- **Dual-level escalation flags** — both company-wide and per-department, triggered at a ±5% variance threshold
- **Plausibility warnings** — flags internally inconsistent inputs (e.g., high attrition + zero raise)
- **Zero-floor guardrail** — extreme manual inputs can't produce a negative headcount or negative payroll

## Results (independently verified)

| Scenario | New Payroll | Headcount | Variance | Flag |
|---|---|---|---|---|
| Baseline | $9,267,829 | 120 | 0.0% | OK |
| Growth | $10,763,564 | 133 | +16.1% | ESCALATE |
| Cost-Cutting | $7,685,786 | 100 | -17.1% | ESCALATE |
| Hiring Freeze | $8,341,046 | 107 | -10.0% | ESCALATE |

Every number above was hand-calculated department-by-department and reconciled against the Sheet's live output before being reported here.

## Recommendations
1. **Revisit the ±5% escalation threshold.** Three of four realistic scenarios trigger it — even "Hiring Freeze," the most conservative option, swings -10% purely from natural attrition. A wider band (e.g., 8-10%) may better separate routine fluctuation from genuinely exceptional shifts at this company's size.
2. **Treat the backfill toggle as the single highest-leverage assumption.** It's the biggest factor determining whether attrition saves money or simply shrinks the company — review it explicitly before trusting any Cost-Cutting or Hiring Freeze output.
3. **Revisit the 1.15x new-hire cost multiplier before using this for real budget decisions** — Growth's cost is materially sensitive to this one assumption.

## Limitations
- 100% synthetic data — 120 fabricated employees, no real company or personal data
- Single-year horizon only; no multi-year projection
- No real payroll tax, benefits, or compliance modeling
- Assumes every department always retains at least one employee (not guarded against a fully emptied department)
- Manually overriding an input cell permanently replaces its formula — a deliberate spreadsheet-modeling tradeoff, not a bug (documented in the in-sheet "How to Use" tab)
- The ±5% escalation threshold is an illustrative assumption for this company's size, not derived from a validated industry benchmark
