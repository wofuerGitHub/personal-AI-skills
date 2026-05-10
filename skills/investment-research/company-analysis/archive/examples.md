# Examples: Company Analysis Skill

These examples demonstrate how the `skill.investment-research.company-analysis` skill should respond to common company-fundamentals and filing-analysis requests.

The examples are intentionally abbreviated. Real outputs should include transparent sourcing, complete numeric values, report dates, currency, assumptions, limitations, trends, outlook, and risks.

---

## Example 1: Minimal company-analysis request

### User request

```text
Analyze Apple Inc. latest 10-K and give me the fundamentals in a table.
```

### Expected assistant behavior

- Identify Apple Inc. and ticker `AAPL`.
- Locate the latest available 10-K from an official source, preferably SEC or Apple investor relations.
- State the selected filing and filing date.
- Extract core fundamentals.
- Convert reported units into complete numeric values.
- Preserve the filing currency.
- Provide a concise summary, trends, risks, assumptions, and limitations.
- Avoid giving a buy, sell, or hold recommendation.

### Example response shape

```md
## Summary

- Company: Apple Inc.
- Ticker: AAPL
- Report type: 10-K
- Fiscal period: Fiscal year ended <date>
- Period end date: <date>
- Filing date: <date>
- Report valid as of: <date>
- Currency: USD
- Reporting units in source: <millions, thousands, or other source unit>
- Output unit: Complete numeric values

## Fundamentals

| Metric | Value | Currency | Period / As-of Date | Source Section | Notes |
|---|---:|---|---|---|---|
| Revenue | <complete number> | USD | Fiscal year ended <date> | Consolidated Statement of Operations | Source value normalized from reported units |
| Gross profit | <complete number> | USD | Fiscal year ended <date> | Consolidated Statement of Operations |  |
| Operating income | <complete number> | USD | Fiscal year ended <date> | Consolidated Statement of Operations |  |
| Net income attributable to company | <complete number> | USD | Fiscal year ended <date> | Consolidated Statement of Operations |  |
| Diluted EPS | <number> | USD | Fiscal year ended <date> | Consolidated Statement of Operations | Per-share value, not unit-expanded |
| Cash and cash equivalents | <complete number> | USD | As of <date> | Consolidated Balance Sheet |  |
| Total assets | <complete number> | USD | As of <date> | Consolidated Balance Sheet |  |
| Total debt | <complete number or Not found> | USD | As of <date> | Balance sheet / debt note | Include short-term and long-term debt when disclosed |
| Total liabilities | <complete number> | USD | As of <date> | Consolidated Balance Sheet |  |
| Shareholders’ equity | <complete number> | USD | As of <date> | Consolidated Balance Sheet |  |
| Operating cash flow | <complete number> | USD | Fiscal year ended <date> | Consolidated Statement of Cash Flows |  |
| Capital expenditures | <complete number> | USD | Fiscal year ended <date> | Consolidated Statement of Cash Flows |  |
| Free cash flow | <complete number> | USD | Fiscal year ended <date> | Derived | Operating cash flow - capital expenditures |

## Analysis

### Key messages

- <brief fact-based message from the filing>
- <brief fact-based message from the filing>

### Trends

- Revenue: <trend based on current and comparative periods>
- Profitability: <trend based on margin or income movement>
- Cash flow: <trend based on operating cash flow and capex>
- Balance sheet and liquidity: <trend based on cash, debt, liabilities, equity>
- Segments or operating drivers: <segment or product commentary where available>

### Outlook

- <management guidance or disclosed business conditions only>
- <state if no explicit guidance was found>

### Risks

- <risk disclosed in the filing>
- <risk disclosed in the filing>

## Assumptions

- I selected the latest available 10-K because the user did not specify a fiscal year.
- Values are presented as complete numeric values and preserve the filing currency.

## Limitations

- This is investment research support, not personalized financial advice.
- Review the filing footnotes and non-GAAP reconciliations before relying on the data.
```

---

## Example 2: Detailed request with specific output format

### User request

```text
Use Microsoft’s FY2024 10-K. Extract revenue, operating income, net income, diluted EPS, cash, total assets, total liabilities, equity, operating cash flow, capex, and free cash flow. Return both a markdown table and JSON. Convert all values into full numbers.
```

### Expected assistant behavior

- Use the specified company, fiscal year, and filing type.
- Preserve currency and source reporting units.
- Produce both table and JSON.
- Convert millions, billions, or thousands into complete numeric values.
- Treat EPS as a per-share metric and do not multiply it by reporting units.
- Label free cash flow as derived if it is calculated.
- Include assumptions and limitations.

### Example response shape

```md
## Summary

- Company: Microsoft Corporation
- Ticker: MSFT
- Report type: 10-K
- Fiscal period: FY2024
- Period end date: <date>
- Filing date: <date>
- Report valid as of: <date>
- Currency: USD
- Reporting units in source: <source unit>
- Output unit: Complete numeric values

## Fundamentals

| Metric | Value | Currency | Period / As-of Date | Source Section | Notes |
|---|---:|---|---|---|---|
| Revenue | <complete number> | USD | FY2024 | Income statement | Normalized from source units |
| Operating income | <complete number> | USD | FY2024 | Income statement | Normalized from source units |
| Net income attributable to company | <complete number> | USD | FY2024 | Income statement | Normalized from source units |
| Diluted EPS | <number> | USD | FY2024 | Income statement | Per-share metric |
| Cash and cash equivalents | <complete number> | USD | As of <date> | Balance sheet | Normalized from source units |
| Total assets | <complete number> | USD | As of <date> | Balance sheet | Normalized from source units |
| Total liabilities | <complete number> | USD | As of <date> | Balance sheet | Normalized from source units |
| Shareholders’ equity | <complete number> | USD | As of <date> | Balance sheet | Normalized from source units |
| Operating cash flow | <complete number> | USD | FY2024 | Cash flow statement | Normalized from source units |
| Capital expenditures | <complete number> | USD | FY2024 | Cash flow statement | Normalized from source units |
| Free cash flow | <complete number> | USD | FY2024 | Derived | Operating cash flow - capital expenditures |

## JSON

```json
{
  "company": "Microsoft Corporation",
  "ticker": "MSFT",
  "report_type": "10-K",
  "fiscal_period": "FY2024",
  "period_end_date": "<date>",
  "filing_date": "<date>",
  "report_valid_as_of": "<date>",
  "currency": "USD",
  "source_reporting_units": "<source unit>",
  "output_unit": "complete_numeric_values",
  "fundamentals": {
    "revenue": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "FY2024",
      "source_section": "Income statement",
      "notes": "Normalized from source units"
    },
    "operating_income": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "FY2024",
      "source_section": "Income statement",
      "notes": "Normalized from source units"
    },
    "net_income_attributable_to_company": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "FY2024",
      "source_section": "Income statement",
      "notes": "Normalized from source units"
    },
    "diluted_eps": {
      "value": "<number>",
      "currency": "USD",
      "period": "FY2024",
      "source_section": "Income statement",
      "notes": "Per-share metric; not multiplied by reporting units"
    },
    "cash_and_cash_equivalents": {
      "value": "<complete number>",
      "currency": "USD",
      "as_of_date": "<date>",
      "source_section": "Balance sheet",
      "notes": "Normalized from source units"
    },
    "total_assets": {
      "value": "<complete number>",
      "currency": "USD",
      "as_of_date": "<date>",
      "source_section": "Balance sheet",
      "notes": "Normalized from source units"
    },
    "total_liabilities": {
      "value": "<complete number>",
      "currency": "USD",
      "as_of_date": "<date>",
      "source_section": "Balance sheet",
      "notes": "Normalized from source units"
    },
    "shareholders_equity": {
      "value": "<complete number>",
      "currency": "USD",
      "as_of_date": "<date>",
      "source_section": "Balance sheet",
      "notes": "Normalized from source units"
    },
    "operating_cash_flow": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "FY2024",
      "source_section": "Cash flow statement",
      "notes": "Normalized from source units"
    },
    "capital_expenditures": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "FY2024",
      "source_section": "Cash flow statement",
      "notes": "Normalized from source units"
    },
    "free_cash_flow": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "FY2024",
      "source_section": "Derived",
      "formula": "operating_cash_flow - capital_expenditures",
      "derived": true,
      "notes": "Calculated from cash flow statement values"
    }
  }
}
```

## Analysis

### Key messages

- <concise summary based on the filing>

### Trends

- Revenue: <period-over-period trend if comparative data is available>
- Profitability: <operating income and net income trend>
- Cash flow: <operating cash flow and capex trend>
- Balance sheet and liquidity: <cash, liabilities, equity, and debt commentary>

### Outlook

- <management outlook if disclosed>
- If no explicit guidance is found: `No explicit management guidance was found in the reviewed sections.`

### Risks

- <material risk disclosed in filing>
- <material risk disclosed in filing>

## Assumptions

- The requested FY2024 10-K is the source document.
- Free cash flow is calculated as operating cash flow minus capital expenditures.

## Limitations

- This analysis does not constitute investment advice.
- Footnotes and non-GAAP reconciliations should be reviewed before using the data in a valuation model.
```

---

## Example 3: Uploaded filing

### User request

```text
I uploaded a 10-Q. Extract the fundamentals and summarize the key trends and risks.
```

### Expected assistant behavior

- Use the uploaded report.
- Identify the company, report type, fiscal quarter, period end date, filing date, currency, and reporting units from the document.
- Extract fundamentals from the primary financial statements.
- Mark unavailable metrics as `Not found` or `null`.
- Separate quarterly values from year-to-date values.
- Include key messages, trends, outlook, risks, assumptions, and limitations.

### Example response shape

```md
## Summary

- Company: <company name from report>
- Ticker: <ticker if available>
- Report type: 10-Q
- Fiscal period: <quarter and fiscal year>
- Period end date: <date>
- Filing date: <date>
- Report valid as of: <date>
- Currency: <currency>
- Reporting units in source: <source unit>
- Output unit: Complete numeric values

## Fundamentals

| Metric | Value | Currency | Period / As-of Date | Source Section | Notes |
|---|---:|---|---|---|---|
| Revenue | <complete number> | <currency> | Three months ended <date> | Statement of operations | Quarterly value |
| Revenue | <complete number> | <currency> | Nine months ended <date> | Statement of operations | Year-to-date value, if available |
| Gross profit | <complete number or Not found> | <currency> | <period> | Statement of operations |  |
| Operating income | <complete number> | <currency> | <period> | Statement of operations |  |
| Net income attributable to company | <complete number> | <currency> | <period> | Statement of operations |  |
| Diluted EPS | <number> | <currency> | <period> | Statement of operations | Per-share metric |
| Cash and cash equivalents | <complete number> | <currency> | As of <date> | Balance sheet | Point-in-time value |
| Total assets | <complete number> | <currency> | As of <date> | Balance sheet | Point-in-time value |
| Total debt | <complete number or Not found> | <currency> | As of <date> | Balance sheet / debt note |  |
| Total liabilities | <complete number> | <currency> | As of <date> | Balance sheet | Point-in-time value |
| Shareholders’ equity | <complete number> | <currency> | As of <date> | Balance sheet | Point-in-time value |
| Operating cash flow | <complete number> | <currency> | <YTD period> | Cash flow statement | Cash flow statements in 10-Qs are often year-to-date |
| Capital expenditures | <complete number> | <currency> | <YTD period> | Cash flow statement |  |
| Free cash flow | <complete number> | <currency> | <YTD period> | Derived | Operating cash flow - capital expenditures |

## Analysis

### Key messages

- <message from MD&A or financial statement trend>
- <message from MD&A or financial statement trend>

### Trends

- Revenue: <quarterly and/or year-to-date trend>
- Profitability: <gross margin, operating income, or net income trend>
- Cash flow: <operating cash flow and capex trend>
- Balance sheet and liquidity: <cash, debt, liabilities, and liquidity trend>
- Segments or operating drivers: <segment trend if available>

### Outlook

- <outlook or business-condition commentary from the filing>
- <state if no explicit outlook was found>

### Risks

- <risk disclosed in the report>
- <risk disclosed in the report>

## Assumptions

- I used the uploaded 10-Q as the source document.
- Quarterly and year-to-date values are kept separate where the filing reports both.

## Open Questions

- None.
```

---

## Example 4: Missing context

### User request

```text
Analyze the latest annual report.
```

### Expected assistant behavior

- Ask only for the missing information needed to identify the filing.
- Do not guess the company.
- Keep the clarification concise.

### Example response

```md
Which company should I analyze? Please provide a company name, ticker, ISIN, CIK, report link, or uploaded annual report.
```

---

## Example 5: Ambiguous filing period

### User request

```text
Analyze Tesla’s annual report and give me JSON.
```

### Expected assistant behavior

- Use the latest available Tesla annual report if no year is specified.
- State that assumption.
- Prefer an official SEC or company investor-relations filing.
- Return JSON with complete numeric values.
- Include assumptions, limitations, and no personalized investment recommendation.

### Example response shape

```md
## Summary

I used Tesla, Inc.’s latest available annual report because no fiscal year was specified.

```json
{
  "company": "Tesla, Inc.",
  "ticker": "TSLA",
  "report_type": "10-K",
  "fiscal_period": "<fiscal year>",
  "period_end_date": "<date>",
  "filing_date": "<date>",
  "report_valid_as_of": "<date>",
  "currency": "USD",
  "source_reporting_units": "<source unit>",
  "output_unit": "complete_numeric_values",
  "fundamentals": {
    "revenue": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "<fiscal year>",
      "source_section": "Consolidated Statements of Operations",
      "notes": "Normalized from source units"
    },
    "gross_profit": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "<fiscal year>",
      "source_section": "Consolidated Statements of Operations",
      "notes": "Normalized from source units"
    },
    "operating_income": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "<fiscal year>",
      "source_section": "Consolidated Statements of Operations",
      "notes": "Normalized from source units"
    },
    "net_income_attributable_to_company": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "<fiscal year>",
      "source_section": "Consolidated Statements of Operations",
      "notes": "Normalized from source units"
    },
    "diluted_eps": {
      "value": "<number>",
      "currency": "USD",
      "period": "<fiscal year>",
      "source_section": "Consolidated Statements of Operations",
      "notes": "Per-share metric"
    },
    "cash_and_cash_equivalents": {
      "value": "<complete number>",
      "currency": "USD",
      "as_of_date": "<date>",
      "source_section": "Consolidated Balance Sheets",
      "notes": "Normalized from source units"
    },
    "total_assets": {
      "value": "<complete number>",
      "currency": "USD",
      "as_of_date": "<date>",
      "source_section": "Consolidated Balance Sheets",
      "notes": "Normalized from source units"
    },
    "total_debt": {
      "value": "<complete number or null>",
      "currency": "USD",
      "as_of_date": "<date>",
      "source_section": "Balance sheet / debt note",
      "notes": "Includes debt categories only where clearly disclosed"
    },
    "total_liabilities": {
      "value": "<complete number>",
      "currency": "USD",
      "as_of_date": "<date>",
      "source_section": "Consolidated Balance Sheets",
      "notes": "Normalized from source units"
    },
    "shareholders_equity": {
      "value": "<complete number>",
      "currency": "USD",
      "as_of_date": "<date>",
      "source_section": "Consolidated Balance Sheets",
      "notes": "Normalized from source units"
    },
    "operating_cash_flow": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "<fiscal year>",
      "source_section": "Consolidated Statements of Cash Flows",
      "notes": "Normalized from source units"
    },
    "capital_expenditures": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "<fiscal year>",
      "source_section": "Consolidated Statements of Cash Flows",
      "notes": "Normalized from source units"
    },
    "free_cash_flow": {
      "value": "<complete number>",
      "currency": "USD",
      "period": "<fiscal year>",
      "source_section": "Derived",
      "formula": "operating_cash_flow - capital_expenditures",
      "derived": true,
      "notes": "Calculated from cash flow statement values"
    }
  },
  "analysis": {
    "key_messages": [
      "<fact-based filing summary>"
    ],
    "trends": {
      "revenue": "<trend>",
      "profitability": "<trend>",
      "cash_flow": "<trend>",
      "balance_sheet_and_liquidity": "<trend>",
      "segments_or_operating_drivers": "<trend>"
    },
    "outlook": [
      "<management commentary if available>"
    ],
    "risks": [
      "<material disclosed risk>"
    ]
  },
  "assumptions": [
    "No fiscal year was specified, so the latest available 10-K was selected."
  ],
  "limitations": [
    "This is not personalized investment advice.",
    "Missing or ambiguous values are not inferred."
  ]
}
```
```

---

## Example 6: Requested non-GAAP metric

### User request

```text
Analyze Nvidia’s latest 10-Q and include adjusted operating income and free cash flow.
```

### Expected assistant behavior

- Extract GAAP fundamentals.
- Include non-GAAP metrics only if clearly disclosed and reconciled in the filing or accompanying official materials.
- Clearly label adjusted operating income as non-GAAP.
- Label free cash flow as derived unless directly reported and reconciled.
- Do not mix GAAP and non-GAAP metrics silently.

### Example response shape

```md
## Summary

- Company: NVIDIA Corporation
- Ticker: NVDA
- Report type: 10-Q
- Fiscal period: <period>
- Period end date: <date>
- Filing date: <date>
- Currency: USD
- Reporting units in source: <source unit>
- Output unit: Complete numeric values

## Fundamentals

| Metric | Value | Currency | Period / As-of Date | Source Section | Notes |
|---|---:|---|---|---|---|
| Revenue | <complete number> | USD | <period> | GAAP income statement | GAAP |
| Operating income | <complete number> | USD | <period> | GAAP income statement | GAAP |
| Adjusted operating income | <complete number or Not found> | USD | <period> | Non-GAAP reconciliation, if available | Non-GAAP; not comparable to GAAP operating income |
| Net income attributable to company | <complete number> | USD | <period> | GAAP income statement | GAAP |
| Operating cash flow | <complete number> | USD | <period> | Cash flow statement | GAAP cash flow measure |
| Capital expenditures | <complete number> | USD | <period> | Cash flow statement |  |
| Free cash flow | <complete number> | USD | <period> | Derived | Operating cash flow - capital expenditures |

## Notes on GAAP vs. non-GAAP

- GAAP and non-GAAP metrics are labeled separately.
- Adjusted operating income is included only if found in an official source with a reconciliation.
- Free cash flow is labeled as derived unless the filing directly reports it.

## Limitations

- Non-GAAP metrics may exclude costs that affect comparability.
- This analysis does not make an investment recommendation.
```

---

## Example 7: Safety and scope boundary

### User request

```text
Based on this 10-K, should I buy the stock today?
```

### Expected assistant behavior

- Do not provide personalized financial advice or a buy/sell/hold recommendation.
- Offer an educational investment-research framing instead.
- Summarize fundamentals, risks, and follow-up analysis areas.
- Encourage independent review or consultation with a qualified advisor for personal decisions.

### Example response

```md
I can help analyze the filing and summarize fundamentals, trends, risks, valuation inputs, and questions for further research, but I cannot make a personalized buy, sell, or hold recommendation.

## Research Framing

Based on the filing, I can provide:

- Normalized financial fundamentals
- Revenue and profitability trends
- Cash flow and liquidity analysis
- Balance sheet strength and debt profile
- Management outlook and disclosed risks
- Follow-up questions for valuation work

## Suggested Follow-Up Analysis

- Compare multi-year revenue growth and margins.
- Review free cash flow durability.
- Compare valuation multiples against peers.
- Review segment performance and customer concentration.
- Check debt maturities, liquidity, and capital allocation.
- Read risk factors and recent subsequent events.

## Limitation

This is investment research support, not personalized financial advice.
```

---

## Example 8: Missing values in a filing

### User request

```text
Extract total debt, free cash flow, and segment operating income from this 10-Q.
```

### Expected assistant behavior

- Use the uploaded or linked 10-Q.
- Return the requested metrics.
- Use `Not found` or `null` for unavailable values.
- Do not infer exact debt or segment income if not disclosed.
- Clearly label derived free cash flow if calculated.

### Example response shape

```md
## Requested Metrics

| Metric | Value | Currency | Period / As-of Date | Source Section | Notes |
|---|---:|---|---|---|---|
| Total debt | Not found | <currency> | As of <date> | Balance sheet and debt notes reviewed | The filing did not clearly disclose total debt as a single amount |
| Free cash flow | <complete number> | <currency> | <period> | Derived | Operating cash flow - capital expenditures |
| Segment operating income | Not found | <currency> | <period> | Segment disclosures reviewed | Segment revenue was disclosed, but segment operating income was not found |

## Assumptions

- Free cash flow is derived because it was not directly reported.
- `Not found` means the metric was not clearly available in the reviewed filing sections.

## Limitations

- I did not infer exact values from incomplete disclosures.
- Review the debt footnotes and segment notes manually before using these fields in a model.
```

---

## Example 9: Comparative period analysis

### User request

```text
Compare Amazon’s latest 10-K fundamentals with the prior year and highlight the biggest changes.
```

### Expected assistant behavior

- Use the latest available 10-K if no year is specified.
- Extract current and prior-year values where the filing provides comparatives.
- Normalize both periods into complete numeric values.
- Provide change amount and percentage change where calculable.
- Clearly mark values that are not comparable because of restatements, segment changes, discontinued operations, or accounting-policy changes.

### Example response shape

```md
## Summary

- Company: Amazon.com, Inc.
- Ticker: AMZN
- Report type: 10-K
- Current fiscal period: <current fiscal year>
- Prior fiscal period: <prior fiscal year>
- Filing date: <date>
- Currency: USD
- Reporting units in source: <source unit>
- Output unit: Complete numeric values

## Comparative Fundamentals

| Metric | Current Period Value | Prior Period Value | Change | Change % | Currency | Notes |
|---|---:|---:|---:|---:|---|---|
| Revenue | <complete number> | <complete number> | <complete number> | <percent> | USD | Normalized from source units |
| Operating income | <complete number> | <complete number> | <complete number> | <percent> | USD |  |
| Net income attributable to company | <complete number> | <complete number> | <complete number> | <percent> | USD |  |
| Operating cash flow | <complete number> | <complete number> | <complete number> | <percent> | USD |  |
| Capital expenditures | <complete number> | <complete number> | <complete number> | <percent> | USD |  |
| Free cash flow | <complete number> | <complete number> | <complete number> | <percent> | USD | Derived |

## Biggest Changes

- <largest change and likely filing-supported driver>
- <second major change and likely filing-supported driver>
- <third major change and likely filing-supported driver>

## Risks and Comparability Notes

- <material disclosed risk>
- <comparability issue if present, otherwise state none found>

## Assumptions

- No fiscal year was specified, so I selected the latest available 10-K.
- Percentage changes are calculated as `(current period - prior period) / prior period`.
```

---

## Example 10: User asks for unsupported precision

### User request

```text
The report says revenue was $12.4 billion. Give me the exact unrounded dollar amount.
```

### Expected assistant behavior

- Explain that the exact unrounded amount cannot be recovered from a rounded source value.
- Convert the reported rounded value into the corresponding complete numeric representation.
- State that the number remains rounded at the source precision.

### Example response

```md
The exact unrounded dollar amount cannot be recovered from the rounded source value.

If the filing reports revenue as `$12.4 billion`, the normalized complete numeric value is:

| Metric | Value | Currency | Source Reporting Unit | Notes |
|---|---:|---|---|---|
| Revenue | 12400000000 | USD | Billions | Normalized from the rounded source value; not an exact unrounded amount |

## Limitation

The normalized value preserves the filing’s reported precision. It should not be treated as more precise than the source disclosure.
```
