# Business Capital Preservation Score Examples

## Example 1: Minimal Request

### User

```text
Score ABC Corp's business capital preservation on a scale of 10.
```

### Expected Behavior

The assistant should explain that the score requires financial and business-quality evidence. It should ask for or identify useful inputs such as leverage, liquidity, free cash flow history, margins, ROIC, cyclicality, customer concentration, and capital allocation.

It should not invent company-specific data or produce a precise score without evidence. If asked to proceed illustratively, it should label the result as low confidence.

---

## Example 2: Complete User-Provided Inputs

### User

```text
Estimate the business capital preservation score for ExampleCo.

Inputs:
- Net debt / EBITDA: 0.8x
- Interest coverage: 14x
- FCF positive in 9 of the last 10 years
- FCF margin: 16%
- ROIC: 18%
- Revenue is 70% recurring
- Top customer is 8% of revenue
- Moderate recession sensitivity
- Share count declined 1% annually over five years
- No major accounting, litigation, or governance issues identified
```

### Expected Behavior

The assistant should:

- Produce a 0-to-10 score.
- Use the default weighted scorecard.
- Score each component with a rationale.
- Assign confidence based on available data.
- Identify strengths such as low leverage, high coverage, recurring revenue, and strong ROIC.
- Identify remaining risks such as moderate recession sensitivity and any missing data.
- State that the analysis is informational and not personalized investment advice.

---

## Example 3: Missing Data

### User

```text
I only know that the company has fast revenue growth and negative free cash flow. Can you score capital preservation?
```

### Expected Behavior

The assistant should provide either no precise score or a broad low-confidence range. It should explain that fast growth alone does not prove capital preservation quality and that negative free cash flow may increase financing or dilution risk.

It should request or list missing information such as cash balance, debt, cash runway, gross margins, burn rate, dilution history, and path to profitability.

---

## Example 4: High Leverage Cap

### User

```text
Score a company with net debt / EBITDA of 7x, interest coverage of 1.4x, negative free cash flow for three years, and debt maturities next year.
```

### Expected Behavior

The assistant should score the company weakly and consider applying a score cap due to refinancing risk, leverage, poor cash generation, and near-term maturities.

It should explain the cap rather than applying it mechanically.

---

## Example 5: Financial Institution Caveat

### User

```text
Estimate the capital preservation score for a regional bank using the default rubric.
```

### Expected Behavior

The assistant should warn that the default industrial-company rubric is not sufficient for banks. It should adapt the analysis toward capital ratios, deposit stability, loan book quality, unrealized losses, funding costs, liquidity, credit losses, reserve adequacy, and regulatory capital.

---

## Example 6: Distinguishing Score From Valuation

### User

```text
The company scores 9/10. Does that mean the stock is cheap?
```

### Expected Behavior

The assistant should explain that capital preservation quality is not the same as valuation attractiveness. A high-quality business can still be overvalued if the price embeds unrealistic expectations.

It should avoid making a buy recommendation.

---

## Example 7: Peer Comparison

### User

```text
Compare capital preservation scores for Company A, Company B, and Company C using these metrics...
```

### Expected Behavior

The assistant should score each company using the same rubric, explain differences, and note where sector differences or missing data reduce comparability.
