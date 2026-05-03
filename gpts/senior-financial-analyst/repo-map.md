# Senior Financial Analyst Repository Map

This repository is the source of truth for the Senior Financial Analyst GPT.

## GPT Package Files

- `gpts/senior-financial-analyst/config.md`
  - Scope, versioning, capabilities, boundaries.
- `gpts/senior-financial-analyst/instructions.md`
  - Behavioral contract and output standards.
- `gpts/senior-financial-analyst/test-prompts.md`
  - Manual validation prompts and expected behavior.

## Skill Sources

### 1) Company Analysis Skill

- `skills/investment-research/company-analysis/README.md`
- `skills/investment-research/company-analysis/skill.md`
- `skills/investment-research/company-analysis/examples.md`
- `skills/investment-research/company-analysis/test-cases.yaml`

Use for:

- 10-K/10-Q extraction
- Filing-based KPI normalization
- Trend and risk analysis
- Table/JSON fundamentals output

### 2) Reports Search Skill

- `skills/investment-research/reports-search/README.md`
- `skills/investment-research/reports-search/skill.md`
- `skills/investment-research/reports-search/test-cases.yaml`

Use for:

- Discovering relevant analyst/research reports
- Filtering by sector, region, report type, and date range
- Returning ranked, summarized results

### 3) Discounted Cash Flow Calculation Skill

- `skills/investment-research/discounted-cash-flow-calculation/README.md`
- `skills/investment-research/discounted-cash-flow-calculation/skill.md`
- `skills/investment-research/discounted-cash-flow-calculation/examples.md`
- `skills/investment-research/discounted-cash-flow-calculation/test-cases.yaml`

Use for:

- Building explicit DCF assumptions and valuation outputs
- Sensitivity framing and assumption transparency

### 4) Business Capital Preservation Score Skill

- `skills/investment-research/business-capital-preservation-score/README.md`
- `skills/investment-research/business-capital-preservation-score/skill.md`
- `skills/investment-research/business-capital-preservation-score/examples.md`
- `skills/investment-research/business-capital-preservation-score/test-cases.yaml`

Use for:

- Evaluating business durability and downside resilience
- Producing structured preservation scoring rationale

### 5) Shareholder Capital Preservation Score Skill

- `skills/investment-research/shareholder-capital-preservation-score/README.md`
- `skills/investment-research/shareholder-capital-preservation-score/skill.md`
- `skills/investment-research/shareholder-capital-preservation-score/examples.md`
- `skills/investment-research/shareholder-capital-preservation-score/test-cases.yaml`

Use for:

- Evaluating shareholder-level dilution, payout quality, and capital protection
- Producing structured preservation scoring rationale

## Shared Quality References

- `repo-config/quality-checklist.md`
- `repo-config/skill-template.md`

## Conflict Rule

When repository skill guidance conflicts with generic defaults, prefer repository guidance unless clearly unsafe or impossible.
