# Senior Financial Analyst

## Version

0.2.0

## Purpose

A filing-first financial analysis GPT that produces structured, date-explicit investment research outputs grounded in primary company disclosures.

## Source of Truth

This GitHub repository is the canonical source for:

- GPT operating instructions
- Skill definitions and workflows
- Skill examples
- Test prompts / test cases
- Quality and review checklists

## GitHub Repository

Expected repository name:

`personal-ai-skills`

## Active Skills

### Company Analysis

Path:

`skills/investment-research/company-analysis/`

Files:

- `README.md`
- `SKILL.md`
- `examples.md`
- `test-cases.yaml`

### Reports Search

Path:

`skills/investment-research/reports-search/`

Files:

- `README.md`
- `SKILL.md`
- `test-cases.yaml`

## Recommended GPT Capabilities

- Knowledge / file retrieval: enabled
- Web browsing: enabled
- Code interpreter / data analysis: enabled
- Canvas: optional
- Image generation: disabled
- Actions: disabled for v0.2

## Primary Users

- Individual investors performing structured due diligence
- Research analysts preparing company snapshots
- Operators/founders benchmarking peers
- Students learning financial statement analysis

## v0.2 Scope

In scope:

- 10-K and 10-Q fundamentals extraction
- Filing metadata normalization (period, filing date, currency, reporting units)
- Structured outputs (tables and JSON)
- Period-over-period trend commentary
- Research report search and ranking
- Assumption and uncertainty disclosure

Out of scope:

- Personalized financial advice
- Buy/sell/hold recommendations
- Portfolio allocation decisions
- Trade execution
- Tax, legal, or accounting assurance opinions
