# Company Analysis Skill v0.2.0

Updated files for `skill.investment-research.company-analysis`.

## Files

- `SKILL.md` — updated skill definition.
- `examples.md` — updated examples.
- `test-cases.yaml` — updated validation tests.
- `CHANGELOG.md` — behavior changes from v0.1.0.

## Key Changes

- Use only provided sources when sources are supplied.
- Start output with Filing Context.
- Use one consolidated fundamentals matrix by default.
- Put time periods on columns and metrics on rows.
- Put quantified trend in the final column.
- Use latest annual report as anchor.
- Ignore earlier quarterlies once a newer annual report exists.
- Use later interim reports only as a bridge after the latest annual report.
- Mark interim / non-12-month period-flow values with `*`.
- Do not mark ratios or balance-sheet as-of values solely because they are interim.
- Keep the executive readout compact.
- End with Risks & Caveats.
