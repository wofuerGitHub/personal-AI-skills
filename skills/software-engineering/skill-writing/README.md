# Skill Writing

This skill helps generate the files needed for a new assistant skill from a user-provided prompt.

It is useful when a user has an idea like "create a skill for code review" or "make a skill that writes release notes" and wants a complete, reusable skill package.

## What it creates

- `SKILL.md` — the main behavior specification (always generated from `repo-config/skill-template.md`)
- `README.md` — user-facing documentation
- `examples.md` — realistic examples of how the skill should behave
- `test-cases.yaml` — checkable scenarios for evaluating the skill

## What it helps with

- Turning a rough skill idea into a structured skill definition
- Defining purpose, scope, inputs, outputs, and constraints
- Writing clear assistant instructions
- Adding examples that cover normal, edge, and limited-context cases
- Adding tests that verify observable behavior
- Improving an existing skill for clarity, safety, and maintainability

## Best inputs

Provide one or more of:

- Skill name
- Short prompt describing the desired skill
- Target users or domain
- Expected inputs and outputs
- Non-goals or unsafe cases
- Example requests
- Preferred file names or folder structure
- Existing template or reference skill

## Example request

```text
Generate all files for a skill called "Release Notes Writing".
The skill should turn merged pull requests and issue summaries into concise release notes for users.
```

## Expected output

The assistant should produce a complete skill package with:

- A clear `SKILL.md`
- A concise `README.md`
- Multiple examples in `examples.md`
- Practical acceptance tests in `test-cases.yaml`
