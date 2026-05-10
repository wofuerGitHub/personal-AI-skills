# Skill: Investment Research – Company Fundamentals from Company Reports

## Metadata

- ID: `skill.investment-research.company-analysis`
- Version: `0.2.0`
- Status: `draft`
- Owner: `Wolfgang Fuerst`
- Last updated: `2026-05-09`

## Purpose

Extract, normalize, and summarize company fundamentals from official company reports. The default use case is **one company with multiple files**. For testing only, the user may provide multiple companies; analyze each company separately, ask for a 0–10 score after each, and incorporate feedback before continuing.

## Use Cases

- Extract fundamentals from annual reports, 10-K, 20-F, quarterly/interim reports, 10-Q, and official result releases.
- Consolidate multiple reports into one trend-first fundamentals matrix.
- Convert source units into complete numeric values while preserving currency and source precision.
- Bridge from the latest annual report to the latest available interim period.
- Quantify trends using CAGR, YoY %, bridge %, or basis-point change.
- Adapt metrics to business model: operating company, holding company, insurer, conglomerate, industrial, pharmaceutical, retail.

## Not For

- Personalized financial advice, buy/sell/hold calls, or portfolio allocation.
- Inventing missing values.
- Using substitute sources when the user supplied sources, unless explicitly authorized.
- Mixing GAAP/IFRS with non-GAAP/APM metrics without labels.
- Treating interim values as 12-month values.
- Treating management guidance as guaranteed performance.

## Inputs

The user may provide company names, tickers, report links, uploaded reports, pasted text, fiscal periods, filing dates, preferred metrics, and output-format instructions.

## Source-Usage Rules

### Provided-source mode

If the user provides report links, uploads, or pasted source text:

- Use only those provided sources.
- Do not search for replacement, fallback, or supplemental sources.
- If a provided source is inaccessible, write `Not available — provided source inaccessible`.
- Do not fill missing values from other websites, memory, search results, or market-data services.
- State which provided reports were used and which were not used.

### Discovery mode

If the user does not provide sources:

- Use official primary sources first: SEC filings, company annual reports, investor-relations reports, or official exchange filings.
- State the selected source and selection assumption.

## Default Output Order

1. `Filing Context`
2. `Consolidated Fundamentals Matrix`
3. `Executive Trend Readout`
4. `Risks & Caveats`
5. `Assumptions & Limitations`, only if needed
6. `Optional JSON Appendix`, only if requested or useful

Keep prose compact and executive-style.

## Process

1. **Clarify only when necessary.** If the report/source set is sufficient, proceed.
2. **Group inputs by company.** If multiple companies are provided for testing, analyze one company at a time and ask for a 0–10 rating after each.
3. **Select source set.** In provided-source mode, do not search or substitute sources.
4. **Determine filing context.** Include company, ticker if available, reports used/not used, period dates, filing/publication dates, report-valid-as-of date, currency, source units, accounting basis, and interim marker.
5. **Apply annual-anchor rule.**
   - Use the latest annual report as the main anchor.
   - If a newer annual report exists, do not show earlier quarterly reports just because they were provided.
   - Use interim reports only when they are later than the latest annual report and bridge the gap to the latest available period.
   - Do not annualize interim values unless explicitly requested.
6. **Build one consolidated fundamentals matrix.**
   - Time periods are columns.
   - Metrics are rows.
   - The final column is `Quantified trend`.
   - Use chronological annual columns, then the latest bridge column if applicable.
   - Avoid separate annual and quarterly tables unless requested.
7. **Use the `*` interim marker correctly.**
   - `*` = interim / not a 12-month period.
   - Mark interim income-statement values, cash-flow values, EPS, dividends paid, buybacks, and other period-flow values.
   - Do **not** mark margins, ratios, percentages, or balance-sheet as-of values solely because they are interim.
   - Add the footnote: `* = interim / not a 12-month period. Ratios and balance-sheet as-of values are not marked.`
8. **Normalize values.**
   - Convert thousands/millions/billions to complete numeric values.
   - Preserve currency, signs, and source precision.
   - Keep EPS, percentages, ratios, units, and employee counts in natural units.
   - Label derived values and formulas.
   - Use `Not found` when not clearly disclosed.
9. **Quantify every trend.**
   - Use CAGR for 3+ annual periods.
   - Use YoY % for comparable two-period values.
   - Use bps change for margins, ratios, rates, and combined ratios.
   - Use bridge change versus latest annual balance-sheet value for point-in-time metrics.
   - If not calculable, write `Not calculable — <reason>`.
   - Do not use vague trend-only language without numbers.
10. **Write executive trend readout.**
    - Merge summary and trend commentary.
    - Focus on the few most important quantified signals.
11. **End with risks and caveats.**
    - Include material risks, inaccessible sources, restatements, discontinued operations, accounting changes, source precision, non-GAAP/APM caveats, and interim limitations.

## Metric Packs

### Standard Operating Company

Revenue, gross profit/margin, operating income/margin, net income, diluted EPS, operating cash flow, capex, free cash flow, cash/equivalents, marketable securities if material, total assets, debt, liabilities, equity, dividends, repurchases.

### Investment Holding Company / NAV

Adjusted NAV, reported NAV, NAV/share, total adjusted assets, portfolio values by bucket, listed/private/fund holdings, gross cash, gross debt, net debt, leverage, dividends received, management cost/ratio, total shareholder return, dividend/share.

### Conglomerate / Insurance-Heavy

Total revenue excluding investment gains when appropriate, investment gains/losses separately, operating earnings if disclosed, underwriting result, float if disclosed, segment earnings, cash, Treasury bills, equity securities, operating cash flow, capex, assets, liabilities, equity, repurchases.

### Insurer / Reinsurer

Insurance revenue, technical result, claims, acquisition/admin costs, combined ratio, investment result, operating result, net result, EPS, ROE, ROI, investments, insurance contract balances, equity, solvency ratio if disclosed, dividend/share, segment results.

### Industrial Equipment / Engineering

Order intake, order backlog, book-to-bill, revenue, EBITDA/margin, EBITA/margin, comparable EBITA/margin, EBIT/margin, net income, EPS, operating cash flow, capex, free cash flow, liquid funds, net liquidity/debt, equity ratio, employees.

### Pharmaceutical

Net sales from continuing operations, gross profit/margin, R&D expense, R&D as % of sales, operating income/margin, net income continuing operations, diluted EPS, core operating income/margin labeled Non-IFRS/non-GAAP, operating cash flow, free cash flow, liquidity, financial debt, net debt, assets, liabilities, equity, dividends, treasury share purchases.

### Retail

Sales, comparable sales, gross margin, SG&A ratio, operating income/margin, net earnings, diluted EPS, operating cash flow, capex, free cash flow, inventory, cash, debt/lease liabilities, assets, liabilities, equity, dividends, repurchases, store count or square footage if disclosed.

## Default Output Format

```md
## Filing Context

| Field | Value |
|---|---|
| Company |  |
| Ticker |  |
| Reports used |  |
| Reports not used |  |
| Latest annual period |  |
| Latest bridge period |  |
| Report-valid-as-of date |  |
| Currency |  |
| Source reporting units |  |
| Output unit | Complete numeric values; EPS, percentages, ratios, units, and counts kept in natural units |
| Accounting basis |  |
| Interim marker | `*` = interim / not a 12-month period. Ratios and balance-sheet as-of values are not marked. |

## Consolidated Fundamentals Matrix

| Metric | FY20XX / <date> | FY20XX / <date> | FY20XX / <date> | Latest bridge: <period> / <date> | Quantified trend |
|---|---:|---:|---:|---:|---|
| Revenue / net sales |  |  |  |  | CAGR / YoY / bridge change |
| Gross margin |  |  |  |  | bps change |
| Operating income |  |  |  |  | CAGR / YoY / bridge change |
| Net income |  |  |  |  | CAGR / YoY / bridge change |
| Operating cash flow |  |  |  |  | CAGR / YoY / bridge change |
| Capex |  |  |  |  | CAGR / YoY / bridge change |
| Free cash flow |  |  |  |  | CAGR / YoY / bridge change |
| Cash and equivalents |  |  |  |  | CAGR / latest bridge change |
| Total debt |  |  |  |  | CAGR / latest bridge change |
| Equity |  |  |  |  | CAGR / latest bridge change |

## Executive Trend Readout

- <Quantified finding>
- <Quantified finding>
- <Quantified bridge finding, if applicable>

## Risks & Caveats

- <Risk or caveat>
- <Comparability caveat>
- <Source-access or missing-data caveat>
```

## Quality Checklist

- [ ] Provided-source mode respected.
- [ ] Filing Context first.
- [ ] One consolidated matrix by default.
- [ ] Time periods are columns.
- [ ] Metrics are rows.
- [ ] Final column is quantified trend.
- [ ] Latest annual report is anchor.
- [ ] Earlier interims ignored when covered by newer annual report.
- [ ] Later interims used only as bridge.
- [ ] `*` used only for non-12-month period-flow values.
- [ ] Ratios and balance-sheet as-of values not marked solely due to interim source.
- [ ] Complete numeric values used.
- [ ] Currency and source units disclosed.
- [ ] GAAP/IFRS and non-GAAP/APM separated.
- [ ] Derived values labeled.
- [ ] Risks & Caveats at end.
