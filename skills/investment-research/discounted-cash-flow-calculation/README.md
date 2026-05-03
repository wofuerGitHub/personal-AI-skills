# Discounted Cash Flow Calculation

This skill helps perform a fundamental discounted cash flow valuation for an equity.

It acts like a Senior Financial Analyst: it gathers or uses available financial data, builds a free cash flow forecast, discounts projected cash flows, calculates terminal value, derives equity value per share, and compares that value with a market price when available.

## What This Skill Helps With

- Estimating intrinsic value per share.
- Building a DCF from financial statements and assumptions.
- Comparing intrinsic value to market price.
- Assessing whether an equity appears overvalued, undervalued, or fairly valued.
- Running sensitivity analysis.
- Explaining which assumptions drive valuation.

## Best Inputs

Useful inputs include:

- Company name and ticker.
- Current share price or valuation date.
- Revenue, EBIT, EBITDA, net income, depreciation, capex, working capital changes, cash, debt, and diluted shares.
- Forecast growth assumptions.
- Margin assumptions.
- Tax rate.
- Discount rate or WACC assumptions.
- Terminal growth rate or exit multiple.
- Projection period.
- Scenario assumptions.

## Example Request

```text
Perform a DCF for ExampleCo.

Use:
- Revenue: $10 billion
- EBIT margin: 18%
- Tax rate: 22%
- Revenue growth: 8% for 5 years, then 3% terminal growth
- Reinvestment: 25% of NOPAT
- WACC: 9%
- Cash: $1.2 billion
- Debt: $2.0 billion
- Diluted shares: 500 million
- Current share price: $42
```

## Expected Outputs

The skill should produce:

- Valuation summary.
- Key assumptions.
- Free cash flow forecast.
- Discount-rate explanation.
- Terminal value calculation.
- Enterprise value and equity value bridge.
- Implied value per share.
- Upside or downside versus market price.
- Sensitivity analysis when useful.
- Risks and limitations.
- Clear statement that the analysis is informational and not personalized financial advice.

## Important Limitations

DCF models are highly sensitive to assumptions. Small changes in discount rate, terminal growth, margins, or reinvestment needs can materially change the valuation.

The skill should not invent current financial data or market prices. If fresh data is unavailable, it should use user-provided data or clearly label the model as illustrative.
