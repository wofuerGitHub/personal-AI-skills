# Business Capital Preservation Score

This skill estimates a business capital preservation score from 0 to 10 for investment research.

It helps assess whether a business is likely to preserve economic value and shareholder capital through difficult conditions by reviewing balance sheet strength, cash-flow resilience, business durability, profitability, cyclicality, capital allocation, dilution, governance, and idiosyncratic risks.

## What This Skill Helps With

- Scoring business resilience on a 0-to-10 scale.
- Comparing downside protection across companies.
- Identifying risks that could impair shareholder capital.
- Separating business quality from valuation attractiveness.
- Summarizing strengths, weaknesses, missing data, and confidence.
- Reviewing a company through a capital-preservation lens.

## Best Inputs

The best inputs include:

- Company name and ticker.
- Recent income statement, balance sheet, and cash-flow metrics.
- Revenue growth, margins, ROIC, free cash flow, and capex intensity.
- Debt, cash, interest coverage, liquidity, and debt maturities.
- Business model and industry description.
- Customer concentration, supplier concentration, and revenue concentration.
- Historical performance during downturns.
- Capital allocation history, acquisitions, dividends, buybacks, and dilution.
- Governance, accounting, litigation, regulatory, or management concerns.
- Peer group or comparable companies.

## Example Request

```text
Estimate the business capital preservation score for ExampleCo.

Use these inputs:
- Net debt / EBITDA: 0.8x
- Interest coverage: 14x
- Free cash flow positive in 9 of the last 10 years
- ROIC: 18%
- Revenue is 70% recurring
- Top customer is 8% of revenue
- Moderate recession sensitivity
- Diluted share count down 1% annually over five years
- No major governance or accounting concerns identified
```

## Expected Outputs

The skill should produce:

- Overall score from 0 to 10.
- Confidence level.
- Component scorecard.
- Evidence-based rationale.
- Strengths and red flags.
- Missing information.
- What could raise or lower the score.
- Statement that the analysis is informational and not personalized investment advice.

## Scoring Summary

- 9.0-10.0: Exceptional capital preservation profile.
- 7.0-8.9: Strong profile.
- 5.0-6.9: Moderate profile.
- 3.0-4.9: Weak profile.
- 0.0-2.9: Very weak profile.

## Important Limitations

The score is not a valuation, price target, credit rating, or investment recommendation. A high-quality business may still be overpriced, and a low-scoring business may still perform well under certain conditions.

The skill should not invent current financial data. If current data is unavailable, it should use user-provided data, label assumptions, and lower confidence where appropriate.
