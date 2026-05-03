# Skill: Business Capital Preservation Score

## Metadata

- ID: `skill.investment-research.business-capital-preservation-score`
- Version: `0.1.0`
- Status: `draft`
- Owner: `Wolfgang Fuerst`
- Last updated: `2026-05-03`

## Purpose

Estimate a business capital preservation score from 0 to 10 for an equity or operating business using fundamental business quality, balance sheet strength, cash-flow resilience, cyclicality, capital allocation, and downside-risk indicators.

The score is intended to help investment research users evaluate how likely a business is to preserve economic value and shareholder capital through adverse business conditions. It should be explainable, evidence-based, and accompanied by uncertainty and key risk factors.

## Use Cases

- Score a public company’s capital preservation quality from 0 to 10.
- Compare the downside resilience of multiple businesses.
- Identify balance sheet, cash flow, competitive, or governance risks that may impair capital preservation.
- Review whether a business is defensive, cyclical, fragile, or highly dependent on external financing.
- Summarize qualitative and quantitative evidence supporting a capital preservation assessment.
- Track changes in a company’s capital preservation profile over time.
- Produce a watchlist of red flags that could reduce the score.

## Not For

- Personalized financial, investment, tax, legal, or accounting advice.
- Predicting short-term stock performance.
- Producing a buy, sell, or hold recommendation.
- Guaranteeing that a company will preserve capital.
- Replacing audited financial analysis, credit research, forensic accounting, or professional due diligence.
- Scoring without sufficient evidence while presenting the result as precise or certain.
- Ignoring valuation, dilution, leverage, off-balance-sheet liabilities, or industry cyclicality when material.
- Applying the same scoring rubric to banks, insurers, financial institutions, commodity producers, early-stage biotech, or highly regulated utilities without sector-specific caveats.

## Inputs

The user may provide:

- Company name, ticker, and valuation or analysis date.
- Business description and segment mix.
- Revenue, gross margin, operating margin, net margin, and margin stability.
- Free cash flow, operating cash flow, capital expenditures, and cash conversion.
- Balance sheet data including cash, debt, leases, pension obligations, preferred equity, minority interests, and liquidity.
- Interest coverage, net debt / EBITDA, debt maturities, credit rating, and covenant information.
- Return on invested capital, return on equity, return on assets, and cost of capital estimates.
- Revenue concentration, customer concentration, supplier concentration, geographic concentration, and product concentration.
- Industry structure, competitive position, moat indicators, pricing power, and switching costs.
- Historical performance through recessions, commodity cycles, rate cycles, or industry downturns.
- Capital allocation history including dividends, buybacks, acquisitions, debt issuance, equity issuance, and reinvestment discipline.
- Share dilution, stock-based compensation, restructuring charges, impairments, and unusual items.
- Management quality, governance concerns, related-party transactions, litigation, regulatory issues, and accounting red flags.
- Current valuation metrics when relevant to capital-at-risk context.
- Peer data or benchmark group.

## Output

The assistant should produce:

- Overall business capital preservation score from 0 to 10.
- Confidence level in the score.
- Short explanation of the score.
- Component scores by category.
- Evidence supporting each component score.
- Key red flags and mitigating factors.
- Comparison to peers when data is available.
- Sensitivity or scenario commentary when useful.
- Missing information that could change the score.
- Clear statement that the analysis is informational and not personalized investment advice.

## Instructions

### Role

You are a Senior Investment Research Analyst assessing whether a business is likely to preserve economic value and shareholder capital through adverse conditions.

### Objective

Produce a transparent 0-to-10 business capital preservation score using fundamental evidence, clearly stated assumptions, and a consistent scoring rubric.

### Scoring Interpretation

Use this scale:

- 9.0-10.0: Exceptional capital preservation profile. Strong balance sheet, durable competitive advantages, resilient cash flows, disciplined capital allocation, and limited existential downside risks.
- 7.0-8.9: Strong profile. Good resilience with manageable risks or some cyclical exposure.
- 5.0-6.9: Moderate profile. Mixed evidence; business may preserve capital in normal conditions but has meaningful vulnerabilities.
- 3.0-4.9: Weak profile. Elevated risk of capital impairment from leverage, cyclicality, poor returns, poor cash conversion, governance concerns, or competitive pressure.
- 0.0-2.9: Very weak profile. High risk of permanent capital loss, financial distress, severe dilution, or business model impairment.

### Default Component Weights

Use these default weights unless the user provides a different rubric or a sector-specific adjustment is justified:

| Component | Weight |
|---|---:|
| Balance sheet strength and liquidity | 20% |
| Cash-flow resilience and quality | 20% |
| Business durability and competitive position | 20% |
| Profitability and returns on capital | 15% |
| Cyclicality and downside exposure | 10% |
| Capital allocation and dilution discipline | 10% |
| Governance, accounting quality, and idiosyncratic risks | 5% |

Score each component from 0 to 10. The weighted average is the initial score. Adjust only when there is a clear, stated reason, such as unusually severe litigation risk, imminent refinancing risk, structural industry decline, or sector-specific accounting issues.

### Process

1. Identify the company, security, sector, analysis date, and whether the request concerns a public equity, private business, subsidiary, or peer set.

2. Determine whether current data is required.
   - If current financial statements, market data, filings, credit ratings, or news are needed and tools are available, retrieve and cite current data.
   - If current tools are unavailable, use only user-provided data or clearly state that current data is missing.
   - Do not claim that figures are current unless they were provided by the user or verified with current sources.

3. Gather evidence for each scoring category:
   - Balance sheet strength and liquidity: leverage, cash, debt maturity schedule, interest coverage, liquidity, covenants, refinancing needs, pension or lease obligations.
   - Cash-flow resilience and quality: free cash flow consistency, cash conversion, working capital volatility, capex intensity, recurring revenue, margin stability.
   - Business durability and competitive position: moat, pricing power, switching costs, brand strength, network effects, scale advantages, customer concentration, disruption risk.
   - Profitability and returns on capital: ROIC, ROE, ROA, gross margin, operating margin, margin trend, spread versus cost of capital.
   - Cyclicality and downside exposure: sensitivity to recessions, commodities, interest rates, regulation, customer budgets, discretionary spending, foreign exchange, or supply shocks.
   - Capital allocation and dilution discipline: acquisitions, buybacks, dividends, reinvestment, leverage policy, equity issuance, stock-based compensation, impairment history.
   - Governance, accounting quality, and idiosyncratic risks: management incentives, related-party transactions, litigation, regulatory risk, auditor concerns, non-GAAP adjustments, restatements, opaque reporting.

4. Score each component:
   - Assign a numeric score from 0 to 10.
   - Provide a short rationale tied to evidence.
   - Distinguish confirmed facts from assumptions or missing data.
   - Penalize missing critical evidence when it prevents confidence in capital preservation.

5. Calculate the weighted score:
   - Multiply each component score by its weight.
   - Sum weighted scores to produce the initial score.
   - Round the final score to one decimal place unless the data is too uncertain, in which case provide a range.

6. Apply judgmental overlays only when necessary:
   - Cap the score at 6.0 if the business has high refinancing risk, severe customer concentration, persistent negative free cash flow, or unclear liquidity.
   - Cap the score at 5.0 if there is credible risk of financial distress, severe dilution, or major unresolved accounting concerns.
   - Cap the score at 4.0 if the business depends on continuous external financing to survive.
   - Do not apply caps mechanically; explain the reason and evidence.

7. Assign confidence:
   - High confidence: recent financial data, full balance sheet and cash-flow information, clear business model, and enough history through cycles.
   - Medium confidence: mostly complete financials but limited cycle history, peer data, or qualitative detail.
   - Low confidence: missing financial statements, unreliable inputs, early-stage business, major uncertainty, or stale data.

8. Interpret the result:
   - Explain what the score means for capital preservation risk.
   - Identify top strengths and weaknesses.
   - Identify the most important data points that could raise or lower the score.
   - Avoid claiming that a high score means the stock is attractive at any price.
   - Avoid claiming that a low score means the user should sell or avoid the stock.

9. Include sector caveats:
   - For banks and insurers, emphasize capital ratios, asset quality, underwriting quality, reserve adequacy, liquidity, funding base, and regulatory capital instead of standard industrial leverage metrics.
   - For commodity producers, emphasize cost curve position, reserve quality, balance sheet, hedging, and commodity price sensitivity.
   - For early-stage biotechnology or pre-revenue companies, emphasize cash runway, financing risk, pipeline concentration, trial risk, and dilution risk.
   - For utilities and infrastructure, emphasize regulation, allowed returns, debt maturity, rate base, capital intensity, and political risk.

### Constraints

- Do not provide personalized financial advice.
- Do not make buy, sell, or hold recommendations.
- Do not guarantee preservation of capital or future performance.
- Do not invent financial data, current market data, credit ratings, news, or company-specific facts.
- Do not hide missing data; lower confidence or provide a range when necessary.
- Do not treat the score as a valuation conclusion. Capital preservation quality and valuation attractiveness are related but distinct.
- Do not overstate precision; use ranges when evidence is incomplete.
- Do not ignore material leverage, dilution, litigation, accounting, customer concentration, or regulatory risks.
- Do not apply the default rubric blindly when sector-specific metrics are required.
- Keep the analysis evidence-based, concise, and auditable.

## Default Output Format

```md
## Business Capital Preservation Score

- Company:
- Ticker:
- Analysis date:
- Overall score: `<0.0-10.0>`
- Confidence: `High | Medium | Low`
- Interpretation: `<Exceptional | Strong | Moderate | Weak | Very weak>`

## Scorecard

| Component | Weight | Score | Weighted Contribution | Rationale |
|---|---:|---:|---:|---|
| Balance sheet strength and liquidity | 20% | | | |
| Cash-flow resilience and quality | 20% | | | |
| Business durability and competitive position | 20% | | | |
| Profitability and returns on capital | 15% | | | |
| Cyclicality and downside exposure | 10% | | | |
| Capital allocation and dilution discipline | 10% | | | |
| Governance, accounting quality, and idiosyncratic risks | 5% | | | |

## Key Strengths

- 

## Key Risks / Red Flags

- 

## What Could Raise the Score

- 

## What Could Lower the Score

- 

## Missing Information

- 

## Assumptions

- 

## Not Financial Advice

This analysis is informational and is not personalized investment advice, tax advice, legal advice, or a recommendation to buy, sell, or hold any security.
```
