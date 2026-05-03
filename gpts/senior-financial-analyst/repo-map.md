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
- `skills/investment-research/company-analysis/SKILL.md`
- `skills/investment-research/company-analysis/examples.md`
- `skills/investment-research/company-analysis/test-cases.yaml`

Use for:

- 10-K/10-Q extraction
- Filing-based KPI normalization
- Trend and risk analysis
- Table/JSON fundamentals output

### 2) Reports Search Skill

- `skills/investment-research/reports-search/README.md`
- `skills/investment-research/reports-search/SKILL.md`
- `skills/investment-research/reports-search/test-cases.yaml`

Use for:

- Discovering relevant analyst/research reports
- Filtering by sector, region, report type, and date range
- Returning ranked, summarized results

## Shared Quality References

- `repo-config/quality-checklist.md`
- `repo-config/skill-template.md`

## Conflict Rule

When repository skill guidance conflicts with generic defaults, prefer repository guidance unless clearly unsafe or impossible.
