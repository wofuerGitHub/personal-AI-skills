# Personal AI Skills

A lightweight repository for designing, documenting, and maintaining reusable AI “skills” (instruction sets/workflows) for personal and team use.

## Repository Structure

- `README.md` — project overview and usage guide.
- `docs/roadmap.md` — roadmap and future plans.
- `repo-config/skill-template.md` — base template for authoring new skills.
- `repo-config/quality-checklist.md` — quality criteria for reviewing skills.

## What Is a Skill?

A skill is a focused set of instructions that helps an AI assistant perform a specific class of tasks consistently (for example: writing API docs, generating test plans, or reviewing architecture decisions).

Each skill should define:

- **Scope**: what it is for (and not for)
- **Inputs**: what user/context data it expects
- **Process**: how the assistant should think and act
- **Outputs**: the structure and quality bar for results
- **Constraints**: safety, uncertainty, and limits

## Getting Started

1. Open `repo-config/skill-template.md`.
2. Copy the template into a new skill file (for example `skills/<name>/SKILL.md`).
3. Fill in metadata, purpose, use cases, and process steps.
4. Review the draft against `repo-config/quality-checklist.md`.
5. Iterate with real examples and edge cases.

## Authoring Guidelines

When writing a new skill:

- Keep instructions actionable and testable.
- Prefer explicit output formats.
- Separate facts, assumptions, and recommendations.
- Call out failure modes and “not for” boundaries.
- Update metadata and version on every meaningful revision.

## Suggested Workflow

- **Draft**: create an initial version from the template.
- **Review**: run through the quality checklist.
- **Pilot**: try the skill on 3–5 realistic prompts.
- **Refine**: tighten ambiguous instructions.
- **Publish**: mark status as ready and document examples.

## Contributing

Contributions are welcome.

- Add or improve skills using the shared template.
- Keep changes small and focused.
- Include rationale for instruction changes.
- Prefer clear, descriptive commit messages.

## License

This project is licensed under the terms in `LICENSE`.
