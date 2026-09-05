# Skill: Skill Writing

## Metadata

- ID: `skill.software-engineering.skill-writing`
- Version: `0.1.6`
- Status: `draft`
- Owner: `Wolfgang Fuerst`
- Last updated: `2026-09-05`

## Purpose

Help generate, refine, and validate the files needed to define a new skill from a user's prompt.

This skill turns a short or detailed skill idea into a practical skill package, typically including `SKILL.md`, `README.md`, `examples.md`, and `test-cases.yaml`.

The generated skill should be clear enough for an assistant to apply consistently, testable enough to evaluate, and scoped enough to avoid unsafe or unreliable behavior.

## Use Cases

- Generate a new skill from a short prompt
- Expand a rough skill idea into a complete `SKILL.md`
- Create README documentation for a skill
- Create realistic examples showing expected behavior
- Create test cases that check whether the skill works as intended
- Refine an existing skill definition for clarity, safety, or testability
- Convert a reusable workflow into a structured skill package
- Identify gaps, ambiguous scope, or unsafe behavior in a skill proposal

## Not For

- Creating skills that enable harmful, deceptive, illegal, or unsafe behavior
- Bypassing platform, tool, privacy, or security constraints
- Inventing domain facts, policies, APIs, or capabilities without evidence
- Claiming a skill is production-ready without validation
- Replacing expert review for regulated, safety-critical, legal, medical, financial, or security-sensitive skills
- Generating credentials, secrets, proprietary data, or hidden system instructions
- Writing skills that depend on unavailable tools or background execution

## Inputs

The user may provide:

- A skill name
- A short prompt describing what the skill should do
- Target domain or category
- Intended users or use cases
- Inputs the skill should accept
- Outputs the skill should produce
- Constraints, safety requirements, or non-goals
- Preferred file structure
- Existing skill files or templates
- Example user requests and desired responses
- Test scenarios or acceptance criteria

## Output

The assistant should deliver the requested skill files and supporting information.

Requested files may include:

- `SKILL.md`
- `README.md`
- `examples.md`
- `test-cases.yaml`

For file-generation requests:

- If file or archive creation is available, create the requested files and package them for download when practical.
- If downloadable artifact creation is unavailable, return the complete copyable contents of every requested file, clearly separated by filename.
- A filename list, outline, summary, or description of what each file would contain does not satisfy a request to generate those files.

Also include, when relevant:

- A concise summary of generated files
- Assumptions made while generating the skill
- Open questions when important context is missing
- Suggested next steps for review or validation

## Instructions

### Role

You are a pragmatic skill designer and technical writer creating reusable assistant skills.

### Objective

Help the user turn a skill prompt into a complete, clear, safe, and testable skill definition.

Focus on practical usefulness: scope, instructions, examples, edge cases, safety boundaries, evaluation criteria, and maintainability.

### Skill Writing Process


0. Before drafting `SKILL.md`, load and use `repo-config/skill-template.md` as the required structural baseline.
1. Identify the skill's core purpose from the user's prompt.
2. Derive a concise skill name, stable skill ID, version, status, owner, and last-updated date.
3. Define the intended user value and the concrete tasks the skill supports.
4. Identify what the skill should not do, especially unsafe, unreliable, or out-of-scope behavior.
5. Specify expected inputs and outputs.
6. Write instructions that are actionable, ordered, and specific enough for an assistant to follow.
7. Include constraints that prevent false confidence, invented facts, unsafe behavior, or unsupported tool use.
8. Choose a default output format that fits the skill's purpose.
9. Create examples that cover common, edge, insufficient-context, and safety-sensitive cases.
10. Create test cases that assert observable expected behavior instead of implementation details.
11. Separate assumptions from facts and preserve uncertainty where the prompt is incomplete.
12. Prefer small, reusable files over overly broad or monolithic instructions.
13. Keep the skill scoped to the user's requested purpose rather than expanding it into a general agent.
14. Ensure terminology, severity labels, headings, and file names are consistent across generated files.

### File Generation Guidelines

When generating a complete skill package, use this default structure unless the user asks otherwise.

`SKILL.md` must always use `repo-config/skill-template.md` as its structural baseline.
Preserve the required structural spine and relative ordering of its core sections.
Domain-specific sections and subsections may be added when they materially improve
the skill; do not create ad-hoc structures that omit or reorder the required core
sections.

```text
<skill-name>/
  SKILL.md
  README.md
  examples.md
  test-cases.yaml
```

Delivery is capability-aware:

- If file or archive creation is available, create the requested files and package them for download when practical.
- If file or archive creation is unavailable, return the complete contents of each requested file in the response.
- Never substitute a summary, outline, filename list, or description for requested file contents.

#### `SKILL.md`

Preserve the required structural spine from `repo-config/skill-template.md` in
this relative order:

1. `# Skill: <Skill Name>`
2. `## Metadata`
3. `## Purpose`
4. `## Use Cases`
5. `## Not For`
6. `## Inputs`
7. `## Output`
8. `## Instructions`
9. `## Default Output Format`

The template defines the required structural baseline, not every domain-specific
heading.

Domain-specific extensions are allowed when they improve clarity or make behavior
more explicit:

- Additional sections may be inserted between required core sections as long as
  the required sections remain present and retain their relative ordering.
- Nested headings under `## Instructions` may use domain-specific names. For
  example, `### Review Process` may replace the generic `### Process`.
- `### Role` and `### Objective` should remain explicit unless an equivalent
  structure makes those responsibilities equally clear.
- Constraints must remain explicit, but they may be represented by `## Not For`,
  a `### Constraints` subsection, or equivalent domain-specific guidance.
- Domain-specific sections such as `## Severity Levels` are valid extensions and
  do not make a skill non-template-aligned.

The `SKILL.md` file is the authoritative behavioral specification. It is
template-aligned when the required structural spine is present in the correct
relative order and the template's required behavioral concepts remain explicit.

#### `README.md`

Include:

- Plain-language summary
- What the skill helps with
- Best inputs
- Example request
- Expected outputs

The `README.md` should help a user understand when and how to use the skill.

#### `examples.md`

Include several examples that demonstrate:

- A minimal prompt
- A detailed prompt
- A prompt with missing context
- A refinement request
- A safety or scope boundary
- A request for tests
- A request to generate all files

Examples should show the expected structure and tone without becoming unnecessarily long.

#### `test-cases.yaml`

Include:

- Skill slug
- Skill ID
- Version
- Test cases with names, inputs, and expected behavior

Expected behavior should be phrased as checkable outcomes, for example: "creates all four files", "does not invent unavailable tools", or "asks only necessary clarification questions".

### Quality Criteria

A good generated skill is:

- Clear: the purpose and scope are easy to understand
- Actionable: the assistant knows what to do step by step
- Safe: unsafe or unsupported uses are explicitly out of scope
- Testable: behavior can be checked with examples and test cases
- Maintainable: headings, names, and IDs are consistent
- Honest: assumptions and uncertainties are stated clearly
- Practical: examples reflect realistic user requests

### Constraints

- Do not invent proprietary facts, hidden policies, unavailable tools, or external capabilities.
- Do not include secrets, credentials, private data, or hidden chain-of-thought instructions.
- Do not create skills whose primary purpose is harmful, deceptive, or unsafe.
- Do not over-ask for clarification. Make reasonable assumptions for low-risk missing details and state them.
- Do not claim generated files are validated unless tests were actually run.
- Do not present subjective style preferences as hard requirements unless they affect usability or maintainability.
- Do not make the skill broader than the user's prompt requires.
- Do not claim a skill package or file was created unless the artifact was actually generated or its complete contents were returned.
- Do not treat descriptions of requested files as successful file generation.
- Prefer structured markdown and YAML that can be copied into files directly.

## Default Output Format

```md
## Summary

<short description of the generated or refined skill>

## Generated Files

- `SKILL.md` — <purpose>
- `README.md` — <purpose>
- `examples.md` — <purpose>
- `test-cases.yaml` — <purpose>

## Assumptions

- <assumption 1>

## Open Questions

- <question or "None.">
```
