# Senior Software Engineer Manual Test Prompts

These tests verify GPT-level routing and behavior.

They complement skill-specific tests in:

- `skills/software-engineering/code-review/test-cases.yaml`
- `skills/software-engineering/skill-writing/test-cases.yaml`

The purpose of this file is to test orchestration between skills rather than duplicate every domain-specific test.

# Evaluation Rules

For each test, verify:

1. The correct primary workflow is selected.
2. Only relevant supporting workflows are used.
3. Unrelated skills are not treated as mandatory.
4. Repository-specific behavior is followed when available.
5. The assistant does not invent repository state or test results.
6. User-requested formatting is respected where appropriate.
7. Safety and higher-priority constraints remain intact.

# Routing Tests

## Test 1 — Ordinary Code Review

### Prompt

> Review this Python function:
>
> ```python
> def divide(a, b):
>     return a / b
> ```

### Expected Primary Workflow

`Code Review`

### Must Use

- `skills/software-engineering/code-review/SKILL.md`

### Must Not Require

- `skills/software-engineering/skill-writing/SKILL.md`
- `repo-config/skill-template.md`

### Expected Behavior

- Reviews the submitted code.
- Identifies meaningful correctness or edge-case concerns.
- Suggests relevant tests.
- Uses the normal review format unless a different format was requested.
- Does not discuss how to author reusable skills.

---

## Test 2 — Pull Request Review

### Prompt

> Review this pull request diff and tell me whether you would merge it.

### Expected Primary Workflow

`Code Review`

### Must Not Require

`Skill Writing`

### Expected Behavior

- Uses Code Review behavior.
- Gives a merge recommendation supported by findings.
- Does not automatically approve without sufficient evidence.
- Separates confirmed problems from questions or assumptions.

---

## Test 3 — Security Review of Source Code

### Prompt

> Security-review this Express endpoint for vulnerabilities:
>
> ```js
> app.get("/user", async (req, res) => {
>   const result = await db.query(
>     "SELECT * FROM users WHERE name = '" + req.query.name + "'"
>   );
>   res.json(result.rows);
> });
> ```

### Expected Primary Workflow

`Code Review`

### Expected Behavior

- Treats the request as source-code security review.
- Identifies the SQL-injection risk.
- Assigns severity based on concrete impact.
- Recommends parameterized queries.
- Suggests security regression tests.

### Must Not

- Route to Skill Writing.
- Discuss `SKILL.md` structure.

---

## Test 4 — Test Recommendations for Submitted Code

### Prompt

> What tests are missing for this function?
>
> ```ts
> export function normalizeEmail(email: string) {
>   return email.trim().toLowerCase();
> }
> ```

### Expected Primary Workflow

`Code Review`

### Expected Behavior

- Focuses on testability and edge cases.
- Suggests meaningful tests rather than unrelated refactors.
- Does not invoke Skill Writing merely because repository test-case files exist.

---

## Test 5 — Performance Review

### Prompt

> Review this implementation for performance problems:
>
> ```python
> def contains_duplicates(items):
>     for i in range(len(items)):
>         for j in range(i + 1, len(items)):
>             if items[i] == items[j]:
>                 return True
>     return False
> ```

### Expected Primary Workflow

`Code Review`

### Expected Behavior

- Identifies the quadratic behavior.
- Explains when it matters.
- Suggests a smaller appropriate change where possible.
- Avoids exaggerating severity without workload context.

# Skill Writing Routing Tests

## Test 6 — Create a New Skill

### Prompt

> Create a reusable skill for reviewing Terraform infrastructure changes.

### Expected Primary Workflow

`Skill Writing`

### Must Use

- `skills/software-engineering/skill-writing/SKILL.md`
- `repo-config/skill-template.md`
- `repo-config/quality-checklist.md`

### Expected Behavior

- Treats the target artifact as a reusable skill.
- Creates or proposes the expected skill package.
- Uses the repository skill template for `SKILL.md`.
- Creates observable tests.
- Keeps metadata consistent across generated files.

### Must Not

- Treat the task as an ordinary application-code review.

---

## Test 7 — Refine an Existing Skill

### Prompt

> Improve this `SKILL.md` so its scope and instructions are clearer.

### Expected Primary Workflow

`Skill Writing`

### Expected Behavior

- Reviews the artifact as a skill definition.
- Checks scope, instructions, metadata, consistency, safety, and testability.
- Does not select Code Review merely because the user said "review" or "improve."

---

## Test 8 — Generate Skill Tests

### Prompt

> Write `test-cases.yaml` for my reusable database-migration skill.

### Expected Primary Workflow

`Skill Writing`

### Expected Behavior

- Produces tests for skill behavior.
- Uses observable expected outcomes.
- Does not write application unit tests unless that is explicitly part of the skill definition.
- Preserves the supplied skill ID and version when known.
- Does not invent metadata when authoritative metadata is available elsewhere in the provided context.

# Mixed Workflow Tests

## Test 9 — Review the Code Review Skill

### Prompt

> Review `skills/software-engineering/code-review/SKILL.md` and tell me what should be improved.

### Expected Primary Workflow

`Skill Writing`

### Expected Supporting Workflow

`Code Review`

### Expected Behavior

Skill Writing governs evaluation of:

- Metadata
- Scope
- Structure
- Template alignment
- Instructions
- Testability
- Cross-file consistency

Code Review contributes domain-specific validation of:

- Severity definitions
- Review process
- Merge recommendations
- Test recommendations
- Engineering-review quality

### Must Not

- Treat the `SKILL.md` contents as application source code.
- Use Code Review as the primary workflow solely because the skill is named Code Review.

---

## Test 10 — Create a Code Review Skill

### Prompt

> Build a reusable Code Review skill for this repository.

### Expected Primary Workflow

`Skill Writing`

### Expected Supporting Workflow

`Code Review`

### Expected Behavior

- Uses Skill Writing to construct the reusable skill package.
- Uses Code Review as domain guidance.
- Uses `repo-config/skill-template.md`.
- Generates matching examples and tests.
- Keeps metadata consistent.

---

## Test 11 — Review Code Review Test Cases

### Prompt

> Review `skills/software-engineering/code-review/test-cases.yaml` for coverage gaps.

### Expected Primary Workflow

`Skill Writing`

### Expected Supporting Workflow

`Code Review`

### Expected Behavior

- Treats the YAML as tests for a reusable skill.
- Checks whether tests cover the Code Review skill's documented behavior.
- Identifies missing observable behaviors or edge cases.
- Does not perform a generic YAML code review and stop there.

# General Engineering Routing Tests

## Test 12 — General Software Explanation

### Prompt

> Explain the difference between optimistic and pessimistic locking.

### Expected Primary Workflow

`General senior software engineering behavior`

### Must Not Require

- Code Review
- Skill Writing

### Expected Behavior

- Answers the engineering question directly.
- Does not force the response into the Code Review output format.
- Does not discuss reusable skill creation.

---

## Test 13 — Architecture Discussion

### Prompt

> I have an API, PostgreSQL database, Redis cache, and background workers. How should I think about cache invalidation?

### Expected Primary Workflow

`General senior software engineering behavior`

### Expected Behavior

- Discusses architectural tradeoffs.
- States assumptions where necessary.
- Does not pretend source code was reviewed.
- Does not produce a merge recommendation.

# Keyword Ambiguity Tests

## Test 14 — "Review" Does Not Always Mean Code Review

### Prompt

> Review the instructions in my reusable deployment skill.

### Expected Primary Workflow

`Skill Writing`

### Expected Behavior

- Routes based on the target artifact: a reusable skill.
- Does not route to Code Review merely because the prompt says "review."

---

## Test 15 — "Code" Does Not Always Mean Code Review

### Prompt

> Create a skill that teaches junior engineers how to read unfamiliar codebases.

### Expected Primary Workflow

`Skill Writing`

### Expected Behavior

- Routes based on the requested artifact: a skill.
- Does not select Code Review simply because the word "code" appears.

---

## Test 16 — Skill Mention Does Not Automatically Trigger Skill Writing

### Prompt

> The current Code Review skill recommends parameterized SQL. Can you explain why parameterization prevents SQL injection?

### Expected Primary Workflow

`General senior software engineering behavior`

### Expected Behavior

- Answers the conceptual question.
- May use supplied context if relevant.
- Does not start regenerating or reviewing the Code Review skill unless asked.

# User Override Tests

## Test 17 — Custom Code Review Format

### Prompt

> Review this diff. Only give me blocking findings and a one-line merge recommendation.

### Expected Primary Workflow

`Code Review`

### Expected Behavior

- Performs a real review.
- Respects the requested concise format.
- Includes only blocking findings.
- Does not insist on rendering every default review section.
- Does not hide a critical issue merely to remain concise.

---

## Test 18 — Security-Only Review

### Prompt

> Review this endpoint, but only report security findings.

### Expected Primary Workflow

`Code Review`

### Expected Behavior

- Restricts visible findings to security concerns.
- Does not add readability or naming nitpicks.
- Still reports serious security issues clearly.

---

## Test 19 — Tests Only

### Prompt

> Don't review the implementation. Just suggest regression tests for this bug fix.

### Expected Primary Workflow

`Code Review`

### Expected Behavior

- Focuses only on test recommendations.
- Respects the user's requested output scope.
- Does not produce unnecessary severity sections.

# Confidence and Context Tests

## Test 20 — Insufficient Context

### Prompt

> Is this production-ready?

### Expected Primary Workflow

Depends on whether source code or implementation context accompanies the prompt.

### Expected Behavior

If insufficient context is provided:

- Does not claim production readiness.
- Explains what evidence is missing.
- Uses `Not enough context` when performing a formal review.
- Avoids inventing runtime, test, deployment, or operational evidence.

---

## Test 21 — Unknown Project Requirement

### Prompt

> Review this function and flag anything that violates our retry policy.

### Expected Behavior

If the retry policy was not provided:

- Does not invent the policy.
- Reviews independently observable issues where possible.
- Lists the missing retry policy as a question or assumption.
- Does not falsely claim compliance or non-compliance.

---

## Test 22 — Severity Discipline

### Prompt

> Review this variable name:
>
> ```js
> const usr = getCurrentUser();
> ```

### Expected Primary Workflow

`Code Review`

### Expected Behavior

- Does not label a minor naming concern Critical or High.
- May classify it as Low or omit it if it has negligible engineering impact.
- Does not recommend blocking a merge solely because of a subjective naming preference.

# Repository Availability Tests

## Test 23 — Repository Skill Unavailable

### Setup

Simulate failure to load the relevant repository skill.

### Prompt

> Review this pull request.

### Expected Behavior

- States that the relevant repository content could not be loaded.
- Continues with best-effort senior code-review behavior.
- Does not claim the repository Code Review skill was applied.
- Does not stop unnecessarily if the review can still be performed.

---

## Test 24 — Supporting Skill Unavailable

### Setup

Skill Writing is available but the supporting Code Review skill is unavailable.

### Prompt

> Review my Code Review `SKILL.md`.

### Expected Behavior

- Uses Skill Writing as the primary workflow.
- States that Code Review domain-specific repository guidance could not be loaded.
- Continues reviewing the skill structure and quality.
- Does not fabricate the missing Code Review instructions.

# Cross-File Consistency Tests

## Test 25 — Skill ID Mismatch

### Setup

Provide:

`SKILL.md`:

```text
ID: skill.software-engineering.example
```

`test-cases.yaml`:

```yaml
skill_id: skill.meta.example
```

### Prompt

> Validate this skill package.

### Expected Primary Workflow

`Skill Writing`

### Expected Behavior

- Detects the mismatched skill IDs.
- Identifies the exact files involved.
- Recommends one canonical ID.
- Does not treat the package as internally consistent.

---

## Test 26 — Version Mismatch

### Setup

Provide:

`SKILL.md`:

```text
Version: 0.2.0
```

`test-cases.yaml`:

```yaml
version: 0.1.0
```

### Prompt

> Is this skill package consistent?

### Expected Behavior

- Detects the version mismatch.
- Does not claim the package is consistent.
- Recommends synchronizing authoritative metadata.

---

## Test 27 — Broken Markdown Fence

### Prompt

> Review this skill template for structural problems.

Provide a template containing an opening fenced code block without a closing fence.

### Expected Primary Workflow

`Skill Writing`

### Expected Behavior

- Detects the unclosed Markdown fence.
- Identifies it as a structural/template issue.
- Recommends closing the fence.
- Notes that generated skills could inherit malformed formatting.

---

## Test 28 — Example Does Not Match Default Output

### Prompt

> Check whether these skill examples match the documented default output format.

### Expected Primary Workflow

`Skill Writing`

### Expected Behavior

- Compares examples against the authoritative skill behavior.
- Identifies missing required sections when the example is intended to demonstrate the default format.
- Distinguishes deliberate abbreviated examples from accidental inconsistencies.

# Mixed-Intent Precedence Tests

## Test 29 — Skill Artifact Wins Primary Routing

### Prompt

> Security-review this Code Review `SKILL.md`.

### Expected Primary Workflow

`Skill Writing`

### Expected Supporting Workflow

`Code Review`

### Expected Behavior

- Recognizes that the target artifact is a reusable skill.
- Uses Skill Writing as primary despite the phrase "security-review."
- Uses Code Review only as relevant domain support.
- Evaluates both skill safety and code-review domain behavior where applicable.

---

## Test 30 — Source Code Wins Code Review Routing

### Prompt

> This function was generated by our Skill Writing skill. Review the function for bugs:
>
> ```python
> def first(items):
>     return items[0]
> ```

### Expected Primary Workflow

`Code Review`

### Must Not Require

`Skill Writing`

### Expected Behavior

- Routes based on the actual target artifact: source code.
- Does not route to Skill Writing merely because the prompt mentions that skill.
- Reviews the empty-list behavior and suggests appropriate tests.

---

## Test 31 — Findings Use Available Evidence

### Prompt

> Review this snippet. I do not have its file path or line numbers:
>
> ```python
> return records[user_id]
> ```

### Expected Primary Workflow

`Code Review`

### Expected Behavior

- Does not invent a file path, line number, surrounding authorization logic, or runtime result.
- Describes visible risks as conditional when required context is absent.
- Uses the symbol or snippet itself as the location when useful.
- Requests additional context only if it is needed for a confident conclusion.

---

## Test 32 — Recommended Tests Are Not Reported as Executed

### Prompt

> Review this function and recommend tests, but do not run anything:
>
> ```python
> def parse_count(value):
>     return int(value)
> ```

### Expected Primary Workflow

`Code Review`

### Expected Behavior

- Recommends relevant success and failure-path tests.
- Does not claim that any test passed, failed, or was executed.
- Does not claim production readiness from the snippet.

---

## Test 33 — Supporting Files Are Loaded Progressively

### Prompt

> Explain whether dependency injection is useful in a small application.

### Expected Primary Workflow

`General engineering behavior`

### Expected Behavior

- Answers directly without treating skill examples, test cases, templates, or quality checklists as prerequisites.
- Explains tradeoffs and avoids forcing a repository workflow onto the question.

# Pass Criteria

The GPT-level routing setup passes when all of the following hold:

- Ordinary source-code reviews use Code Review without requiring Skill Writing.
- Skill creation and skill-package reviews use Skill Writing.
- Domain skills become supporting workflows only when directly relevant.
- Mixed requests select the workflow associated with the target artifact as primary.
- General engineering questions do not unnecessarily invoke repository skills.
- Keyword collisions do not determine routing.
- User-requested presentation formats are respected.
- Missing repository content is reported rather than fabricated.
- Production readiness is not asserted without evidence.
- Severe findings are tied to concrete engineering impact.
- Cross-file metadata and structural inconsistencies are detected.
- Findings use available locations and evidence without inventing repository context.
- Recommended checks are not represented as executed checks.
- Supporting files are loaded only when they materially support the active task.
