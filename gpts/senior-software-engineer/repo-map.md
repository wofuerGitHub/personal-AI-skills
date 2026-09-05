# Senior Software Engineer Repository Map

This repository is the source of truth for the Senior Software Engineering Copilot GPT's reusable skills, examples, tests, templates, and repository-specific behavior.

## Primary GPT Files

### `gpts/senior-software-engineer/instructions.md`

Main behavioral instructions for the GPT.

Defines:

- Primary role
- Repository source-of-truth behavior
- Skill routing
- Mixed-skill routing
- Default code-review behavior
- User override behavior

### `gpts/senior-software-engineer/config.md`

Human-readable GPT configuration and scope.

### `gpts/senior-software-engineer/test-prompts.md`

Manual regression prompts used to verify:

- Correct skill selection
- Skill isolation
- Mixed-skill routing
- Review behavior
- Repository fallback behavior
- User-format overrides
- Confidence and production-readiness behavior

## Repository-Level Configuration

### `repo-config/system-directive.md`

Shared repository-level behavioral guidance.

This file is subordinate to higher-priority platform, safety, privacy, and tool requirements.

It must not be interpreted as overriding those constraints.

### `repo-config/skill-template.md`

Required base template for new `SKILL.md` files.

Used primarily by the Skill Writing workflow.

### `repo-config/quality-checklist.md`

Shared quality checklist for reusable skill files and repository consistency.

Use it when:

- Creating skills
- Refining skills
- Reviewing skill packages
- Checking cross-file consistency

It may also support domain-skill maintenance where relevant.

# Active Workflows

## Code Review Workflow

### Purpose

Review source code and code-level changes for engineering quality.

### Primary Skill

- `skills/software-engineering/code-review/SKILL.md`

### Supporting Files

- `skills/software-engineering/code-review/README.md`
- `skills/software-engineering/code-review/examples.md`
- `skills/software-engineering/code-review/test-cases.yaml`
- `repo-config/quality-checklist.md`

### Use When

The user asks for:

- Code review
- Pull request review
- Diff review
- Security review of source code
- Production-readiness review
- Test recommendations for submitted code
- Maintainability review
- Performance review
- API review
- Refactoring review
- Bug or edge-case analysis

### Do Not Automatically Load

Do not automatically load:

- `skills/software-engineering/skill-writing/*`
- `repo-config/skill-template.md`

for ordinary code reviews.

Those files concern reusable skill authoring rather than application-code review.

## Skill Writing Workflow

### Purpose

Create, refine, review, and validate reusable assistant skills.

### Primary Skill

- `skills/software-engineering/skill-writing/SKILL.md`

### Supporting Files

- `skills/software-engineering/skill-writing/README.md`
- `skills/software-engineering/skill-writing/examples.md`
- `skills/software-engineering/skill-writing/test-cases.yaml`
- `repo-config/skill-template.md`
- `repo-config/quality-checklist.md`

### Use When

The user asks to:

- Create a reusable skill
- Create a `SKILL.md`
- Generate a complete skill package
- Refine an existing skill
- Review an existing skill
- Review skill examples
- Review skill tests
- Validate skill scope or safety
- Validate consistency between skill files
- Convert a workflow into a reusable skill

### Do Not Automatically Load

Do not automatically load the Code Review workflow merely because the user says "review."

The artifact being reviewed must determine the route.

# Mixed Workflow Routing

Use multiple workflows only when they are directly relevant.

## Rule

If the target artifact is itself a reusable skill:

- Skill Writing is the primary workflow.
- A domain skill may be loaded as supporting context when the reusable skill concerns that domain.

## Example: Review a Code Review Skill

User request:

> Review my Code Review `SKILL.md`.

Primary workflow:

- Skill Writing

Supporting workflow:

- Code Review

Skill Writing evaluates:

- Skill structure
- Scope
- Metadata
- Template alignment
- Instructions
- Examples
- Tests
- Cross-file consistency

Code Review contributes:

- Domain-specific review expectations
- Appropriate severity behavior
- Review completeness
- Engineering-review quality

## Example: Ordinary Pull Request Review

User request:

> Review this pull request.

Primary workflow:

- Code Review

Do not load:

- Skill Writing

## Example: Create a New Code Review Skill

User request:

> Create a reusable code-review skill.

Primary workflow:

- Skill Writing

Supporting workflow:

- Code Review

# Routing Matrix

| User intent | Primary workflow | Supporting workflow |
|---|---|---|
| Review application code | Code Review | None by default |
| Review a pull request | Code Review | None by default |
| Review a diff | Code Review | None by default |
| Security-review submitted code | Code Review | None by default |
| Review code performance | Code Review | None by default |
| Recommend tests for submitted code | Code Review | None by default |
| Create a reusable skill | Skill Writing | Domain skill when relevant |
| Refine a `SKILL.md` | Skill Writing | Domain skill when relevant |
| Review a skill package | Skill Writing | Domain skill when relevant |
| Review Code Review `SKILL.md` | Skill Writing | Code Review |
| Create a Code Review skill | Skill Writing | Code Review |
| Explain a software concept | General engineering behavior | None |
| Discuss architecture without reviewing code | General engineering behavior | None unless a relevant skill exists |

# Routing Principle

Route based on the target artifact and requested operation, not isolated keywords.

In particular:

- `"review"` does not always mean Code Review.
- `"code"` does not always mean Code Review.
- `"skill"` does not automatically require every domain skill.
- Supporting skills should be loaded only when they materially improve the primary workflow.

Conceptually:

```text
User request
    |
    v
What is the target artifact?
    |
    +-- reusable skill / SKILL.md / skill package
    |       |
    |       +--> Skill Writing
    |               |
    |               +--> relevant domain skill only if needed
    |
    +-- source code / PR / diff / implementation
    |       |
    |       +--> Code Review when review behavior is requested
    |
    +-- general software-engineering question
            |
            +--> General senior software engineering behavior
```

# Source-of-Truth Rule

When answering questions governed by an active skill:

1. Load the applicable primary skill.
2. Load its relevant supporting files.
3. Apply repository-specific behavior over generic behavior where they differ.
4. Do not load unrelated skills by default.
5. Use mixed workflows only when the task genuinely crosses domains.

If repository content is unavailable, state that limitation and continue with best-effort general behavior.

If repository instructions are unsafe, impossible, contradictory to higher-priority instructions, or incompatible with available tools, do not follow the conflicting portion.

# Repository Structure

```text
personal-ai-skills/
├── gpts/
│   └── senior-software-engineer/
│       ├── instructions.md
│       ├── config.md
│       ├── repo-map.md
│       └── test-prompts.md
│
├── skills/
│   └── software-engineering/
│       ├── code-review/
│       │   ├── README.md
│       │   ├── SKILL.md
│       │   ├── examples.md
│       │   └── test-cases.yaml
│       │
│       └── skill-writing/
│           ├── README.md
│           ├── SKILL.md
│           ├── examples.md
│           └── test-cases.yaml
│
└── repo-config/
    ├── system-directive.md
    ├── skill-template.md
    └── quality-checklist.md
```
