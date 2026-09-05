# Code Review

This skill helps review code like a pragmatic senior software engineer.

## What it reviews

- Correctness
- Edge cases
- Security
- Performance
- Maintainability
- API design
- Test coverage

## Best inputs

Provide one or more of:

- Code snippet
- Pull request diff
- Intended behavior
- Programming language and framework
- Test results
- Relevant constraints

## Example request

```text
Review this Python function for correctness, security, and maintainability.
```

## Expected output

By default, the skill returns an evidence-based review with a merge recommendation, severity-grouped findings, concrete suggested changes, test recommendations, and explicit assumptions. Findings use available file and line locations without inventing missing context.
