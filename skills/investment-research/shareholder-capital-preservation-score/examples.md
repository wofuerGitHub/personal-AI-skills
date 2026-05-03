# Examples: Shareholder Capital Preservation Score

## Example 1: Minimal Prompt

### User Request

```text
Score XYZ Corp for shareholder capital preservation on a 0-to-10 scale. It has net cash, stable free cash flow, low cyclicality, and trades at about 14x free cash flow.
```

### Expected Behavior

The assistant should provide a provisional score, explain that the limited data reduces confidence, and avoid inventing missing financial metrics. It should use the weighted rubric and identify missing items such as debt maturity details, governance, capital allocation history, and accounting quality.

## Example 2: Detailed Equity Data

### User Request

```text
Evaluate ABC plc for shareholder capital preservation.

Data:
- Cash: £900M
- Total debt: £350M
- Free cash flow: £210M, positive for 10 straight years
- Revenue: low single-digit growth
- Operating margin: 22%, stable
- Interest coverage: 18x
- Share count: down 1% annually for 5 years
- Dividends: 35% payout ratio
- Acquisitions: small bolt-ons, no major write-offs
- Valuation: 12x normalized FCF
- Risks: mature market, modest customer concentration
```

### Expected Behavior

The assistant should calculate a high but not perfect score, likely in the strong or exceptional band depending on assumptions. It should cite balance-sheet strength, free-cash-flow durability, conservative payout, and reasonable valuation as positives, while noting mature-market and concentration risks.

## Example 3: Missing Context

### User Request

```text
Give Tesla a shareholder capital preservation score.
```

### Expected Behavior

The assistant should ask for the desired time period and data source or provide a clearly provisional framework if data is not available. It should not invent current metrics. It should explain that current filings, cash, debt, free cash flow, valuation, governance, and business-risk data are needed for a reliable score.

## Example 4: Red-Flag Case

### User Request

```text
Score DEF Inc. It has negative free cash flow, debt due in six months, no committed refinancing, a going-concern warning, and repeated equity dilution.
```

### Expected Behavior

The assistant should identify severe capital-preservation risks and apply a red-flag cap. The final score should be low, likely capped at 3 or below, with clear rationale around liquidity, refinancing, dilution, and going-concern risk.

## Example 5: Scope Boundary

### User Request

```text
Score this stock and tell me whether I should buy it today.
```

### Expected Behavior

The assistant should provide the research score if enough data is available but should not give personalized buy/sell/hold advice. It should state that the result is investment research support, not a trading recommendation.

## Example 6: Peer Comparison

### User Request

```text
Compare Companies A, B, and C on shareholder capital preservation using these supplied metrics.
```

### Expected Behavior

The assistant should score each company with the same rubric, show a comparable table, and explain where differences are driven by balance sheet, cash flow, valuation, capital allocation, or governance.

## Example 7: Test Request

### User Request

```text
Create test cases for the shareholder-capital-preservation-score skill.
```

### Expected Behavior

The assistant should generate tests that check scoring structure, financial-advice boundaries, red-flag caps, missing-data handling, and consistency of the 0-to-10 scale.
