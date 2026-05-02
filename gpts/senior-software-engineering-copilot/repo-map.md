# Senior Software Engineering Copilot Repository Map

This repository is the source of truth for the Senior Software Engineering Copilot GPT.

## Primary GPT Files

- `gpts/senior-engineering-copilot/instructions.md`
  - Main behavior instructions for the GPT.

- `gpts/senior-engineering-copilot/config.md`
  - Human-readable configuration and scope.

- `gpts/senior-engineering-copilot/test-prompts.md`
  - Manual prompts used to test whether the GPT behaves correctly.

## Active Skills

### Code Review

Skill path:

- `skills/software-engineering/code-review/README.md`
- `skills/software-engineering/code-review/skill.md`
- `skills/software-engineering/code-review/examples.md`
- `skills/software-engineering/code-review/test-cases.yaml`

Use this skill when the user asks for:

- Code review
- Pull request review
- Diff review
- Security review
- Production-readiness review
- Test recommendations
- Maintainability feedback
- Performance review
- API review

## Repository Config

- `repo-config/skill-template.md`
  - Template for new skills.

- `repo-config/quality-checklist.md`
  - Checklist for reviewing skill quality.

## Source-of-Truth Rule

When answering questions about skill behavior, prefer the files in this repository over general model knowledge.

If the repo and general knowledge conflict, follow the repo unless it is clearly unsafe, incorrect, or impossible.