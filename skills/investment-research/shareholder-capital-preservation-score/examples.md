# Examples: shareholder-capital-preservation-score

## Example 1: Strong Capital Preserver

### User Prompt

Score ExampleCo's shareholder capital preservation from 0 to 10. It has net cash, 20% return on invested capital, steady free cash flow, share count down 2% annually, no major acquisitions, and insider ownership of 8%.

### Expected Response

## Shareholder Capital Preservation Score

**Company:** ExampleCo  
**Period reviewed:** User-provided summary  
**Score:** 8.6/10  
**Confidence:** Low

## Rationale

ExampleCo appears to have a strong capital preservation profile based on the provided facts. Net cash, consistent free cash flow, high returns on invested capital, modest share-count reduction, and insider ownership all support a high score. Confidence is low because the assessment relies only on the user summary, not primary financial statements.

## Score Breakdown

| Category | Weight | Raw Score | Weighted Contribution | Key Evidence |
|---|---:|---:|---:|---|
| Balance-sheet resilience | 20% | 9.5 | 1.90 | Net cash position |
| Cash generation and earnings quality | 20% | 8.5 | 1.70 | Steady free cash flow |
| Capital allocation discipline | 20% | 8.5 | 1.70 | High ROIC; no major acquisition concerns |
| Dilution and shareholder treatment | 15% | 9.0 | 1.35 | Share count down 2% annually |
| Business durability and downside protection | 15% | 8.0 | 1.20 | High returns suggest quality, but durability details are limited |
| Governance and alignment | 10% | 7.5 | 0.75 | Insider ownership of 8% |

## Main Strengths

- Net cash balance sheet.
- Consistent free cash flow.
- Evidence of per-share discipline through buybacks or controlled issuance.

## Main Risks

- Durability, customer concentration, and accounting quality are not provided.
- No valuation assessment is included.

## Watch Items

- Whether buybacks were made at reasonable prices.
- Whether free cash flow remains stable in a downturn.

## Assumptions and Limitations

- This is based only on the user-provided summary.
- No buy, sell, or hold recommendation is implied.

## Example 2: Weak Capital Preserver

### User Prompt

Score RiskyCo. It has negative free cash flow for five years, share count doubled, net debt is 5x EBITDA, and management keeps making acquisitions.

### Expected Response

## Shareholder Capital Preservation Score

**Company:** RiskyCo  
**Period reviewed:** User-provided summary  
**Score:** 2.5/10  
**Confidence:** Low

## Rationale

RiskyCo shows several capital preservation red flags: persistent free-cash-flow burn, severe dilution, high leverage, and acquisition-driven strategy. These factors materially increase the risk of permanent impairment for shareholders.

## Score Breakdown

| Category | Weight | Raw Score | Weighted Contribution | Key Evidence |
|---|---:|---:|---:|---|
| Balance-sheet resilience | 20% | 2.0 | 0.40 | Net debt around 5x EBITDA |
| Cash generation and earnings quality | 20% | 1.5 | 0.30 | Negative free cash flow for five years |
| Capital allocation discipline | 20% | 2.0 | 0.40 | Continued acquisitions despite weak cash flow |
| Dilution and shareholder treatment | 15% | 1.0 | 0.15 | Share count doubled |
| Business durability and downside protection | 15% | 4.0 | 0.60 | Insufficient business-quality data; weak cash flow is concerning |
| Governance and alignment | 10% | 6.0 | 0.60 | No direct governance data provided |

## Main Strengths

- None evident from the provided information.

## Main Risks

- High leverage.
- Repeated dilution.
- Persistent cash burn.
- Potential value destruction through acquisitions.

## Watch Items

- Liquidity runway and maturity schedule.
- Covenant compliance.
- Acquisition returns and goodwill impairment risk.
- Whether equity issuance is required to fund operations or debt service.

## Assumptions and Limitations

- Score is capped by persistent cash burn, high leverage, and recurring dilution.
- Confidence is low because only a short summary was provided.

## Example 3: Incomplete Data

### User Prompt

Give Tesla a shareholder capital preservation score.

### Expected Response Pattern

Ask for or gather the relevant period and data if available. If no current data source is available, explain the limitation and provide a framework-based assessment only if sufficient information is already in context. Do not invent current financial figures.

Required elements:

- State the period reviewed.
- Identify missing data.
- Assign low confidence if relying on incomplete information.
- Avoid buy/sell/hold advice.
