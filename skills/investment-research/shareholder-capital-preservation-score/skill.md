---
name: shareholder-capital-preservation-score
description: Score a company’s ability to preserve shareholder capital on a 0-to-10 scale using evidence from financial statements, capital allocation, balance-sheet risk, dilution, governance, and downside-risk indicators.
---

# Shareholder Capital Preservation Score

## Purpose

Use this skill to estimate how well a company preserves shareholder capital. The output is a practical 0-to-10 score, where higher scores indicate stronger evidence that shareholder capital is protected from permanent impairment, dilution, excessive leverage, poor capital allocation, weak governance, and fragile business economics.

This skill is for analytical support only. It is not investment, legal, accounting, or tax advice.

## When to Use

Use this skill when the user asks for any of the following:

- A shareholder capital preservation score
- A 0-to-10 capital preservation rating
- A quality, downside-risk, capital allocation, or permanent-capital-impairment assessment
- A comparison of companies by shareholder capital preservation
- A checklist-style review of whether a company protects shareholder value

## Required Inputs

Prefer the following inputs when available:

1. Company name and ticker
2. Reporting period or fiscal year
3. Latest annual report, quarterly report, investor presentation, or financial statements
4. Market capitalization and enterprise value
5. Balance sheet, income statement, and cash flow statement data
6. Share count history
7. Debt maturity schedule and interest expense
8. Capital allocation history, including buybacks, dividends, acquisitions, equity issuance, and debt issuance
9. Governance data, including insider ownership, related-party transactions, compensation, and shareholder voting structure
10. Industry context and major business risks

If the user provides incomplete data, still produce a score, but clearly label assumptions and confidence level.

## Output Format

Use this structure by default:

```markdown
## Shareholder Capital Preservation Score

**Company:** <name / ticker>
**Period reviewed:** <period>
**Score:** <x.x>/10
**Confidence:** High | Medium | Low

## Rationale

<brief overall assessment>

## Score Breakdown

| Category | Weight | Raw Score | Weighted Contribution | Key Evidence |
|---|---:|---:|---:|---|
| Balance-sheet resilience | 20% | x/10 | x.xx | ... |
| Cash generation and earnings quality | 20% | x/10 | x.xx | ... |
| Capital allocation discipline | 20% | x/10 | x.xx | ... |
| Dilution and shareholder treatment | 15% | x/10 | x.xx | ... |
| Business durability and downside protection | 15% | x/10 | x.xx | ... |
| Governance and alignment | 10% | x/10 | x.xx | ... |

## Main Strengths

- ...

## Main Risks

- ...

## Watch Items

- ...

## Assumptions and Limitations

- ...
```

## Scoring Scale

Use this 0-to-10 interpretation:

- **9.0-10.0:** Exceptional preservation profile. Strong balance sheet, durable cash generation, disciplined capital allocation, minimal dilution, aligned governance, and low risk of permanent impairment.
- **7.0-8.9:** Strong profile. Some risks exist, but evidence generally supports capital preservation.
- **5.0-6.9:** Adequate or mixed profile. Capital preservation depends on execution, cycle conditions, valuation, or unresolved risks.
- **3.0-4.9:** Weak profile. Meaningful risk of dilution, leverage stress, poor allocation, cyclicality, governance concerns, or cash-flow fragility.
- **0.0-2.9:** Very poor profile. Severe capital impairment risk, persistent cash burn, high leverage, major governance concerns, distress risk, or shareholder-unfriendly behavior.

## Category Weights

Default weights:

| Category | Weight |
|---|---:|
| Balance-sheet resilience | 20% |
| Cash generation and earnings quality | 20% |
| Capital allocation discipline | 20% |
| Dilution and shareholder treatment | 15% |
| Business durability and downside protection | 15% |
| Governance and alignment | 10% |

The weights may be adjusted when the user requests a sector-specific model, but any changes must be stated explicitly.

## Category Rubrics

### 1. Balance-Sheet Resilience, 20%

Score high when the company has:

- Low net leverage relative to durable cash flows
- Ample liquidity
- Manageable maturity schedule
- Interest coverage through a downturn
- Limited off-balance-sheet obligations
- Conservative working-capital and inventory risk
- No obvious solvency or refinancing pressure

Score low when there is:

- Excessive leverage
- Near-term maturities without clear funding
- Weak interest coverage
- Covenant pressure
- Reliance on external capital
- Large unfunded obligations
- Balance-sheet opacity

Suggested anchors:

- **10:** Net cash or very low leverage, abundant liquidity, resilient coverage under stress.
- **5:** Manageable leverage but dependent on stable earnings or refinancing access.
- **0:** Distress, liquidity shortfall, covenant breach risk, or unsustainable debt load.

### 2. Cash Generation and Earnings Quality, 20%

Score high when the company has:

- Positive and recurring free cash flow
- High conversion of earnings to cash
- Conservative revenue recognition
- Stable or improving margins
- Low reliance on adjustments
- Reasonable working-capital behavior
- Limited capital intensity relative to returns

Score low when there is:

- Persistent free-cash-flow burn
- Large gap between adjusted earnings and cash flow
- Aggressive accounting indicators
- High capital expenditure needs without adequate returns
- Unstable gross margins or customer concentration
- Unexplained receivable, inventory, or capitalization growth

Suggested anchors:

- **10:** Durable free cash flow, clean accounting, high earnings-to-cash conversion.
- **5:** Positive but cyclical or inconsistent cash generation.
- **0:** Persistent cash burn, poor conversion, or serious accounting-quality concerns.

### 3. Capital Allocation Discipline, 20%

Score high when management:

- Reinvests at attractive returns
- Acquires businesses prudently and integrates them well
- Repurchases shares below intrinsic value or when leverage is conservative
- Pays sustainable dividends
- Avoids empire building
- Uses debt and equity conservatively
- Provides clear hurdle rates and accountability

Score low when management:

- Overpays for acquisitions
- Buys back stock aggressively at inflated prices or while overleveraged
- Issues equity at unattractive prices
- Maintains an unsustainable dividend
- Pursues low-return projects
- Frequently changes strategy without accountability

Suggested anchors:

- **10:** Long record of high-return reinvestment and shareholder-aware decisions.
- **5:** Mixed history, with both value-creating and questionable decisions.
- **0:** Repeated value-destructive allocation, distressed issuance, or unsustainable distributions.

### 4. Dilution and Shareholder Treatment, 15%

Score high when:

- Share count is stable or declining without compromising financial resilience
- Stock-based compensation is reasonable and transparently reported
- Equity issuance is rare and value-accretive
- Buybacks exceed dilution over time
- Minority shareholders are treated fairly

Score low when:

- Share count grows materially without proportional value creation
- Stock-based compensation is excessive
- Repeated equity issuance funds operating losses
- Related-party transactions transfer value away from shareholders
- Dual-class or control structures harm minority owners

Suggested anchors:

- **10:** Long-term per-share value compounding with minimal dilution.
- **5:** Moderate dilution that may be offset by growth.
- **0:** Severe or recurring dilution, shareholder value leakage, or coercive financing.

### 5. Business Durability and Downside Protection, 15%

Score high when the business has:

- Durable competitive advantages
- Recurring or mission-critical revenue
- Pricing power
- Diversified customers, suppliers, geographies, and products
- Resilience across cycles
- Low disruption risk
- Favorable industry structure

Score low when the business has:

- Commodity exposure without cost advantage
- High cyclicality
- High customer concentration
- Weak competitive position
- Obsolescence risk
- Heavy regulatory, litigation, or geopolitical exposure
- Fragile unit economics

Suggested anchors:

- **10:** Durable moat and resilient demand through stress.
- **5:** Viable business but exposed to cycles, competition, or execution.
- **0:** Structurally challenged, obsolete, or highly fragile business model.

### 6. Governance and Alignment, 10%

Score high when:

- Management and board incentives align with long-term per-share value
- Insider ownership is meaningful but not abusive
- Compensation metrics emphasize returns, cash flow, and per-share outcomes
- Board independence and oversight are credible
- Disclosure quality is high
- Related-party transactions are limited and fair

Score low when:

- Incentives reward size, revenue, or adjusted metrics regardless of value creation
- Related-party transactions are material or opaque
- Management has a record of poor disclosure
- Control structure disadvantages minority shareholders
- Governance has recurring controversies

Suggested anchors:

- **10:** Strong alignment, clean governance, high-quality disclosure.
- **5:** Standard governance with some misalignment or disclosure gaps.
- **0:** Serious governance red flags or shareholder-hostile control.

## Calculation Method

1. Assign a raw score from 0 to 10 for each category.
2. Multiply each raw score by its weight.
3. Sum weighted contributions.
4. Round the final score to one decimal place.
5. Assign confidence:
   - **High:** Multiple primary-source filings and enough financial history are available.
   - **Medium:** Some primary data is available, but important details are missing.
   - **Low:** The assessment relies on limited, stale, unaudited, or user-provided data only.

Formula:

```text
Final Score =
0.20 * Balance Sheet +
0.20 * Cash Generation +
0.20 * Capital Allocation +
0.15 * Dilution +
0.15 * Business Durability +
0.10 * Governance
```

## Evidence Rules

- Prefer primary filings, audited financial statements, regulatory filings, and company disclosures.
- Separate facts from judgments.
- Do not invent missing figures.
- Do not use current market data unless available in the conversation or through an explicitly permitted data source.
- When data is missing, state what is unknown and reduce confidence.
- Distinguish valuation risk from capital preservation risk. A wonderful company can still be a poor investment at an excessive valuation, but this score primarily assesses preservation of shareholder capital through business quality, financing risk, governance, and allocation discipline.
- Be careful with financial advice language. Present analysis, not recommendations to buy, sell, or hold.

## Red Flags That Should Cap the Score

Apply these caps unless strong contrary evidence is available:

- **Score cap 6.0:** Persistent free-cash-flow burn without a clear funding path.
- **Score cap 6.0:** Material and recurring dilution above underlying value creation.
- **Score cap 5.0:** High leverage with weak interest coverage.
- **Score cap 5.0:** Major acquisition integration failure or repeated value-destructive M&A.
- **Score cap 4.0:** Serious accounting-quality concerns or restatements affecting core metrics.
- **Score cap 4.0:** Related-party transactions that appear to transfer value from shareholders.
- **Score cap 3.0:** Going-concern warning, distressed refinancing, or acute liquidity risk.
- **Score cap 2.0:** Evidence of fraud, insolvency, coercive recapitalization, or severe shareholder impairment.

If a cap is applied, explain it clearly.

## Sector Adjustments

Use default scoring unless the user asks for a sector-specific approach. Consider these adjustments:

- **Banks and insurers:** Emphasize regulatory capital, asset quality, reserve adequacy, liquidity, underwriting discipline, and book-value protection.
- **REITs:** Emphasize funds from operations, leverage, asset quality, debt maturity ladder, tenant concentration, payout ratio, and access to capital.
- **Utilities and infrastructure:** Emphasize regulatory compact, debt maturity schedule, allowed returns, capital intensity, and dividend coverage.
- **Commodity producers:** Emphasize cost curve position, reserve quality, hedging, balance-sheet strength, and cycle survival.
- **Biotech and pre-revenue companies:** Emphasize cash runway, trial risk, financing need, dilution risk, pipeline concentration, and partnership quality.
- **Software and subscription businesses:** Emphasize net retention, customer concentration, cash conversion, stock-based compensation, competitive durability, and Rule-of-40 context.

## Refusal and Safety Boundaries

Do not provide personalized investment advice. Avoid commands such as “buy,” “sell,” “hold,” or “short.” When the user asks for a recommendation, redirect to analytical framing:

- “Here is the capital preservation profile and the key risks to evaluate.”
- “This does not determine suitability for your portfolio.”

Do not fabricate financial statements, legal conclusions, or audit opinions.
