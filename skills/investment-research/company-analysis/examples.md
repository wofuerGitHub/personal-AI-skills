# Examples: Company Analysis Skill v0.2.0

Examples are abbreviated; real outputs should include source context, complete numeric values, dates, currency, quantified trend math, and risks/caveats.

## Example 1 — Multiple provided filings for one operating company

### User request

```text
Use these Apple annual and quarterly reports. Extract fundamentals and analyze the trend.
```

### Expected behavior

- Use only supplied reports.
- Use latest annual as anchor.
- Use only later interim reports as bridge.
- Ignore quarterlies already covered by a newer annual report.
- Return one consolidated matrix.
- Periods on columns, metrics on rows, quantified trend in final column.
- Mark interim period-flow values with `*`.

### Response shape

```md
## Filing Context

| Field | Value |
|---|---|
| Company | Apple Inc. |
| Reports used | FY2023 10-K, FY2024 10-K, FY2025 10-K, Q2 FY2026 10-Q |
| Reports not used | Q3 FY2025 10-Q because FY2025 10-K is newer |
| Latest annual period | FY2025 / 2025-09-27 |
| Latest bridge period | H1 FY2026 / 2026-03-28 |
| Currency | USD |
| Source reporting units | USD millions |
| Interim marker | `*` = interim / not a 12-month period. Ratios and balance-sheet as-of values are not marked. |

## Consolidated Fundamentals Matrix

| Metric | FY2023 | FY2024 | FY2025 | Latest bridge: H1 FY2026 | Quantified trend |
|---|---:|---:|---:|---:|---|
| Total net sales | <full number> | <full number> | <full number> | <full number>* | FY23–FY25 CAGR <x.x%>; H1 YoY <x.x%> |
| Gross margin | <x.x%> | <x.x%> | <x.x%> | <x.x%> | FY23–FY25 <xxx bps>; H1 YoY <xxx bps> |
| Operating income | <full number> | <full number> | <full number> | <full number>* | FY23–FY25 CAGR <x.x%>; H1 YoY <x.x%> |
| Cash and marketable securities | <full number> | <full number> | <full number> | <full number> | FY23–FY25 CAGR <x.x%>; bridge vs FY25 <x.x%> |

## Executive Trend Readout

- Revenue CAGR was <x.x%>, while Services grew at <x.x%>.
- Gross margin expanded <xxx bps>.
- Latest bridge is positive/negative by <x.x%>, but marked values are not 12-month values.

## Risks & Caveats

- `*` marks values that are not 12-month values.
- Free cash flow is derived.
- No substitute sources were used.
```

## Example 2 — Investment holding company

### Expected behavior

Use NAV-focused metrics rather than forcing revenue/gross profit.

```md
| Metric | FY2023 | FY2024 | FY2025 | Latest bridge: Q1 2026 | Quantified trend |
|---|---:|---:|---:|---:|---|
| Adjusted NAV | <full number> | <full number> | <full number> | <full number> | FY23–FY25 CAGR <x.x%>; bridge vs FY25 <x.x%> |
| NAV/share | <value> | <value> | <value> | <value> | FY23–FY25 CAGR <x.x%> |
| Net debt | <full number> | <full number> | <full number> | <full number> | FY23–FY25 CAGR <x.x%>; bridge vs FY25 <x.x%> |
| Leverage | <x.x%> | <x.x%> | <x.x%> | <x.x%> | FY23–FY25 <xxx bps> |
| Dividends received | <full number> | <full number> | <full number> | <full number>* | FY23–FY25 CAGR <x.x%> |
```

Caveat: adjusted NAV and leverage may be APMs; label them.

## Example 3 — Latest annual supersedes earlier quarterlies

### User request

```text
Provided reports: FY2023 annual, FY2024 annual, FY2025 annual, Q1 2025, Q2 2025, Q3 2025. Analyze fundamentals.
```

### Expected behavior

- Use FY2025 annual as latest annual anchor.
- Do not show Q1/Q2/Q3 2025 columns.
- State: `Q1–Q3 2025 reports were not used because FY2025 annual report is newer.`

## Example 4 — Later interim bridges from latest annual

### User request

```text
Provided reports: FY2023 annual, FY2024 annual, FY2025 annual, Q1 2026 interim.
```

### Expected behavior

```md
| Metric | FY2023 | FY2024 | FY2025 | Latest bridge: Q1 2026 | Quantified trend |
|---|---:|---:|---:|---:|---|
| Revenue | <full number> | <full number> | <full number> | <full number>* | FY23–FY25 CAGR <x.x%>; Q1 YoY <x.x%> |
| Operating margin | <x.x%> | <x.x%> | <x.x%> | <x.x%> | FY23–FY25 <xxx bps>; Q1 YoY <xxx bps> |
| Cash | <full number> | <full number> | <full number> | <full number> | FY23–FY25 CAGR <x.x%>; bridge vs FY25 <x.x%> |
```

Revenue is marked with `*`; operating margin and cash are not.

## Example 5 — Inaccessible provided source

### Expected behavior

```md
| Field | Value |
|---|---|
| Reports used | FY2025 Annual Report |
| Reports not used | Q1 2026 report: Not available — provided source inaccessible |
```

No substitute source is used.

## Example 6 — Multiple-company testing workflow

Analyze one company at a time and end each output with:

```md
Please rate this output from 0–10 for expected Company Analysis Skill behavior, and tell me what should be improved before I continue.
```

## Example 7 — Non-GAAP / APM separation

```md
| Metric | FY2023 | FY2024 | FY2025 | Latest bridge | Quantified trend |
|---|---:|---:|---:|---:|---|
| Operating income, IFRS | <full number> | <full number> | <full number> | <full number>* | IFRS; CAGR <x.x%> |
| Core operating income, Non-IFRS | <full number> | <full number> | <full number> | <full number>* | Non-IFRS; CAGR <x.x%> |
| Free cash flow, derived | <full number> | <full number> | <full number> | <full number>* | Derived; CAGR <x.x%> |
```
