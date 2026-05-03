# Shareholder Capital Preservation Score

This skill evaluates equity data and produces a 0-to-10 score expressing how well a company appears positioned to preserve shareholder capital.

It focuses on protecting principal from permanent loss. It prioritizes balance-sheet strength, liquidity, cash-flow durability, disciplined capital allocation, valuation downside risk, governance, accounting quality, and business stability over high growth or high returns.

## What This Skill Helps With

- Scoring a public equity for capital-preservation quality.
- Comparing equities using a consistent downside-risk rubric.
- Identifying red flags that may threaten shareholder principal.
- Turning financial-statement and valuation inputs into a structured research output.
- Making uncertainty and missing data explicit.

## Best Inputs

Provide as much of the following as possible:

- Company name, ticker, exchange, and reporting currency.
- Recent balance sheet, income statement, and cash-flow data.
- Cash, debt, maturity profile, interest coverage, and liquidity information.
- Free cash flow, earnings quality, margins, and cyclicality.
- Dividend, buyback, dilution, acquisition, and leverage history.
- Valuation metrics and relevant peers.
- Governance, accounting, litigation, regulatory, and other tail-risk context.

## Example Request

```text
Score Company ABC on shareholder capital preservation using a 0-to-10 scale.

Data:
- Net cash: $2.1B
- Free cash flow: $850M
- Revenue growth: 3%
- Operating margin: 18%
- Debt maturities: none material for 4 years
- Buybacks: modest and below intrinsic value estimate
- Valuation: 13x normalized FCF
- Risks: customer concentration and cyclical end market
```

## Expected Outputs

The skill should return:

- A final 0-to-10 Shareholder Capital Preservation Score.
- A score band and interpretation.
- A weighted scoring table.
- Red-flag review.
- Main positives and negatives.
- Missing information and assumptions.
- A reminder that the analysis is investment research support, not personalized financial advice.
