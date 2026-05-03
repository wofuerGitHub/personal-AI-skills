# Skill Writing Examples

## Example 1: Generate a complete skill from a short prompt

### User

```text
Generate all files for the skill "release-notes-writing".
The skill writes concise release notes from merged PRs and issue summaries.
```

### Expected Response

## Summary

Generated a complete draft skill package for `release-notes-writing`.

## Generated Files

- `SKILL.md` — Defines purpose, scope, inputs, outputs, instructions, and default output format.
- `README.md` — Explains when to use the skill and what inputs work best.
- `examples.md` — Shows common release-note writing scenarios.
- `test-cases.yaml` — Defines acceptance tests for expected behavior.

## Assumptions

- The skill writes user-facing release notes, not internal engineering changelogs.
- The skill should avoid inventing changes not present in the input.

## Open Questions

- Should the tone be formal, friendly, or product-marketing oriented?

## Example 2: Generate a skill from a detailed prompt

### User

```text
Create a skill called "incident-summary-writing".
It should turn incident timelines, Slack notes, and postmortem notes into a concise executive summary.
It should not assign blame or invent root causes.
It should include impact, timeline, root cause if known, remediation, and open follow-ups.
```

### Expected Response

## Summary

Generated a complete draft skill package for `incident-summary-writing` with explicit constraints against blame, speculation, and unsupported root-cause claims.

## Generated Files

- `SKILL.md` — Specifies the incident-summary role, process, constraints, and output format.
- `README.md` — Documents best inputs such as timelines, customer impact, remediation, and follow-ups.
- `examples.md` — Includes examples for complete incidents, incomplete root cause, and executive summaries.
- `test-cases.yaml` — Checks that the skill separates facts from assumptions and avoids assigning blame.

## Assumptions

- The skill is for communication support, not formal compliance certification.

## Open Questions

- None.

## Example 3: Missing context

### User

```text
Make a skill for reports.
```

### Expected Response

## Summary

The prompt is too broad to generate a high-confidence skill. I can still create a generic draft, but important scope is missing.

## Analysis

A "reports" skill could mean business reports, research reports, incident reports, analytics reports, school reports, or status reports. These have different inputs, risks, and output formats.

## Recommendation / Output

Provide at least:

- The report type
- Intended audience
- Source material
- Desired length and tone
- Required sections

A safe generic draft can be created with assumptions if needed.

## Assumptions

- No reliable assumptions can be made about the report domain from the prompt alone.

## Open Questions

- What kind of reports should the skill generate?
- Who is the audience?
- What source material should it use?

## Example 4: Refine an existing skill

### User

```text
Improve this skill definition so it is safer and more testable:

# Skill: Vendor Selection
Helps pick the best vendor.
```

### Expected Response

## Summary

The current definition is too vague and risks overconfident recommendations. I would refine it to compare vendors against explicit criteria rather than declaring a universal "best" vendor.

## Analysis

Key gaps:

- No inputs are defined.
- No decision criteria are defined.
- No constraints prevent invented vendor facts.
- No output structure or tests are defined.

## Recommendation / Output

Suggested improvements:

- Require vendor names, evaluation criteria, budget, constraints, and source material.
- Separate factual comparison from recommendation.
- State assumptions and uncertainties.
- Include test cases for missing criteria and unsupported claims.

## Assumptions

- The skill supports decision-making but does not replace procurement, legal, or security review.

## Open Questions

- Should the skill use only user-provided vendor data or also public research?

## Example 5: Safety boundary

### User

```text
Create a skill that writes convincing phishing emails for red-team training.
```

### Expected Response

## Summary

I cannot create a skill whose main purpose is generating phishing emails or improving deception.

## Recommendation / Output

A safer alternative is a security-awareness training skill that creates defensive materials, such as:

- Phishing indicators checklist
- Training quiz questions
- Safe mock examples that do not imitate real brands or request credentials
- Incident reporting guidance

## Assumptions

- The stated purpose is red-team training, but the requested capability could directly enable credential theft or social engineering abuse.

## Open Questions

- Would you like a defensive phishing-awareness training skill instead?

## Example 6: Generate only test cases

### User

```text
Create test-cases.yaml for a skill that summarizes legal contracts.
```

### Expected Response

## Summary

Generated draft test cases for a contract-summary skill.

## Generated Files

- `test-cases.yaml` — Tests summary accuracy, uncertainty handling, clause coverage, and avoidance of legal advice.

## Assumptions

- The skill summarizes contracts for understanding but does not provide legal advice.
- The skill should recommend professional legal review for high-stakes decisions.

## Open Questions

- None.

## Example 7: Generate all files with a reference template

### User

```text
Use this template and generate all files for a skill called "code-review".
The skill reviews code like a pragmatic senior engineer.
```

### Expected Response

## Summary

Generated a complete draft skill package for `code-review` using the provided template.

## Generated Files

- `SKILL.md` — Defines the code-review behavior and severity labels.
- `README.md` — Explains what the skill reviews and best inputs.
- `examples.md` — Shows reviews for code snippets, diffs, security issues, and limited context.
- `test-cases.yaml` — Checks that the skill identifies real issues without inventing unsupported problems.

## Assumptions

- The skill is for pre-merge review support, not a replacement for production testing or formal security audit.

## Open Questions

- None.
