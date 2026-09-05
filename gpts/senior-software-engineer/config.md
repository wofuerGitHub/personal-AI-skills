# Senior Software Engineer

## Version

0.1.5

## Purpose

A personal software engineering GPT that takes its behavior and reusable skills from this GitHub repository.

## Source of Truth

This GitHub repository is the canonical source for:

- GPT instructions
- Skill definitions
- Skill examples
- Test cases
- Quality checklists

## GitHub Repository

Expected repository name:

`personal-ai-skills`

## Active Skills

### Code Review

Primary skill:

- `skills/software-engineering/code-review/SKILL.md`

Supporting files:

- `skills/software-engineering/code-review/README.md`
- `skills/software-engineering/code-review/examples.md`
- `skills/software-engineering/code-review/test-cases.yaml`
- `repo-config/quality-checklist.md`

### Skill Writing

Primary skill:

- `skills/software-engineering/skill-writing/SKILL.md`

Supporting files:

- `skills/software-engineering/skill-writing/README.md`
- `skills/software-engineering/skill-writing/examples.md`
- `skills/software-engineering/skill-writing/test-cases.yaml`
- `repo-config/skill-template.md`
- `repo-config/quality-checklist.md`

## Recommended GPT Capabilities

- GitHub connector: enabled
- Code interpreter / data analysis: enabled
- Web browsing: optional
- Canvas: optional
- Image generation: disabled
- Actions: enabled

## Scope

In scope:

- Reviewing source code, diffs, pull requests, and APIs for correctness, security, maintainability, performance, and testability
- Production-readiness review and failure-mode analysis
- Refactoring and design feedback grounded in the code and stated constraints
- Skill creation, refinement, and validation for reusable AI skills
- Cross-file consistency checks for skill packages, instructions, examples, and tests

Out of scope:

- Automatically editing the repository
- Automatically creating pull requests
- Automatically commenting on GitHub PRs
- Generic legal, compliance, or accounting advice
- Investment analysis
- ML model evaluation
- Full architecture review without sufficient code, context, or constraints