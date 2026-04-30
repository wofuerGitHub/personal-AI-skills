# Code Review Examples
## Example 1: Python function review
### User

```text
Review this Python function:

def average(values):
    return sum(values) / len(values)
```

## Review Summary

The function is simple and readable, but it does not handle empty input and may fail for non-numeric values.

## Merge Recommendation

Approve with comments

## Findings

### Critical

- None found.

### High

- None found.

### Medium

- Empty input raises `ZeroDivisionError`. Decide whether this should return `None`, raise a domain-specific error, or require callers to validate input.

### Low

- Consider adding a type hint to document expected input and output.

### Questions

- Should empty input be valid in this domain?

## Suggested Changes

```python
from collections.abc import Sequence

def average(values: Sequence[float]) -> float:
    if not values:
        raise ValueError("values must not be empty")

    return sum(values) / len(values)
```

## Example 2: Security-focused review

### User

```text
Review this endpoint for security:

@app.get("/users/{user_id}")
def get_user(user_id: int):
    return db.query(User).filter(User.id == user_id).first()
```

## Review Summary

The endpoint is concise, but it appears to return arbitrary user records without checking whether the caller is authenticated and authorized.

## Merge Recommendation

Request changes

## Findings

### Critical

- None found.

### High

- Missing authorization check. Any caller who can guess or enumerate `user_id` may be able to access another user's profile.

### Medium

- Missing not-found handling. Returning `None` may produce unclear API behavior depending on the framework configuration.

### Low

- The function name is clear.

### Questions

- Is authentication handled globally by middleware?
- Should users only access their own profile, or can admins access any profile?

## Suggested Changes

```python
@app.get("/users/{user_id}")
def get_user(user_id: int, current_user: User = Depends(require_user)):
    user = db.query(User).filter(User.id == user_id).first()

    if user is None:
        raise HTTPException(status_code=404, detail="User not found")

    if user.id != current_user.id and not current_user.is_admin:
        raise HTTPException(status_code=403, detail="Forbidden")

    return user
```

## Example 3: Async performance review

### User

```text
Review this JavaScript code:

async function loadUsers(ids) {
  const users = [];
  for (const id of ids) {
    users.push(await fetchUser(id));
  }
  return users;
}
```

## Review Summary

The function is easy to understand, but it fetches users sequentially. If each request is independent, this can be much slower than necessary.

## Merge Recommendation

Approve with comments

## Findings

### Critical

- None found.

### High

- None found.

### Medium

- Sequential `await` inside the loop causes each request to wait for the previous one. This may significantly increase latency for large `ids` arrays.

### Low

- Consider naming `ids` more specifically if the surrounding context is ambiguous.

### Questions

- Does `fetchUser` have rate limits or side effects that require sequential execution?
- Should the result preserve the same order as the input IDs?

## Suggested Changes

If requests are independent:

```js
async function loadUsers(ids) {
  return Promise.all(ids.map((id) => fetchUser(id)));
}
```

## Example 4: SQL Injection Review

### User

```text
Review this Python database code:

def find_user(username):
    query = f"SELECT * FROM users WHERE username = '{username}'"
    return db.execute(query).fetchone()
```

## Review Summary

This function contains a likely SQL injection vulnerability because user input is interpolated directly into the SQL query string.

## Merge Recommendation

Request changes

## Findings

### Critical

- SQL injection risk. A malicious `username` value could alter the query and access, modify, or delete data depending on database permissions.

### High

- The function returns `SELECT *`, which may expose more columns than needed.

### Medium

- There is no explicit behavior for nonexistent users.
- The database API usage is unclear, so the exact parameter syntax may vary.

### Low

- The function name is clear.

### Questions

- Which database library is being used?
- Which fields does the caller actually need?
- Should username lookup be case-sensitive?

## Suggested Changes

Use parameterized queries instead of string interpolation.

Example:

```python
def find_user(username: str):
    query = "SELECT id, username, email FROM users WHERE username = ?"
    return db.execute(query, (username,)).fetchone()
```

## Example 5: React Component Review

### User

```text
Review this React component:

function UserCard({ user }) {
  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.email}</p>
      <img src={user.avatarUrl} />
    </div>
  );
}
```

## Review Summary

The component is simple and readable, but it assumes `user` and all nested fields are always present. The image also lacks accessibility metadata.

## Merge Recommendation

Approve with comments

## Findings

### Critical

- None found.

### High

- None found.

### Medium

- Missing null handling. If `user` is `null` or `undefined`, the component will throw at render time.
- The image is missing an `alt` attribute, which harms accessibility.

### Low

- Consider adding a CSS class or component wrapper if this is part of a larger design system.
- Consider making the displayed fields explicit through prop typing.

### Questions

- Should this component render a loading or fallback state when `user` is missing?
- Is `avatarUrl` always trusted and validated?
- Should email addresses be displayed publicly?

## Suggested Changes

```jsx
function UserCard({ user }) {
  if (!user) {
    return <p>User unavailable</p>;
  }

  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.email}</p>
      {user.avatarUrl && (
        <img src={user.avatarUrl} alt={`${user.name}'s avatar`} />
      )}
    </div>
  );
}
```

## Example 6: Error Handling Review

### User

```text
Review this Node.js function:

async function getProfile(userId) {
  const response = await fetch(`/api/users/${userId}`);
  const data = await response.json();
  return data;
}
```

## Review Summary

The function is concise, but it does not handle failed HTTP responses, network errors, invalid JSON, or unsafe `userId` values.

## Merge Recommendation

Approve with comments

## Findings

### Critical

- None found.

### High

- None found.

### Medium

- The function does not check `response.ok`. A `404` or `500` response may still be parsed and returned as if it were successful.
- Network errors are not handled or contextualized.
- `userId` is interpolated directly into the URL without encoding.

### Low

- The function name is clear.
- Consider documenting the expected shape of the returned profile.

### Questions

- Should callers handle errors, or should this function normalize them?
- What should happen for `404` responses?
- Is this used in browser code or server-side code?

## Suggested Changes

```js
async function getProfile(userId) {
  const encodedUserId = encodeURIComponent(userId);
  const response = await fetch(`/api/users/${encodedUserId}`);

  if (!response.ok) {
    throw new Error(`Failed to load profile: ${response.status}`);
  }

  return response.json();
}
```

## Example 7: Production Readiness Review

### User

```text
Is this code production-ready?

def process_payment(user_id, amount):
    charge_card(user_id, amount)
    save_payment(user_id, amount)
    send_receipt(user_id, amount)
```

## Review Summary

This code is not ready to evaluate as production-ready from the snippet alone. The happy path is clear, but important payment concerns are missing or not visible: validation, idempotency, error handling, transaction boundaries, auditability, and observability.

## Merge Recommendation

Not enough context

## Findings

### Critical

- Potential idempotency issue. If this function is retried after `charge_card` succeeds but before `save_payment` completes, the user may be charged multiple times.

### High

- No visible validation for `amount`.
- No visible error handling for failed card charges, failed database writes, or failed receipt delivery.
- No transaction or consistency strategy is visible between charging the card and saving the payment record.

### Medium

- No logging, metrics, or tracing are visible.
- No currency handling is shown.
- No audit trail is shown.
- Receipt sending appears synchronous and may make the payment flow less reliable.

### Low

- The function is easy to read, but it hides important business behavior inside helper functions.

### Questions

- Is `charge_card` idempotent?
- Is there an idempotency key per payment attempt?
- What happens if `save_payment` fails after the card is charged?
- Is `amount` represented as integer minor units, decimal, or float?
- Should receipt sending happen asynchronously?

## Suggested Changes

At minimum, introduce:

- Amount and currency validation
- Idempotency key
- Persistent payment attempt record
- Clear state transitions
- Error handling and retry strategy
- Asynchronous receipt sending
- Logging and audit events

Conceptual example:

```python
def process_payment(user_id, amount, currency, idempotency_key):
    validate_payment_input(user_id, amount, currency)

    payment = create_or_get_payment_attempt(
        user_id=user_id,
        amount=amount,
        currency=currency,
        idempotency_key=idempotency_key,
    )

    if payment.status == "succeeded":
        return payment

    charge = charge_card(
        user_id=user_id,
        amount=amount,
        currency=currency,
        idempotency_key=idempotency_key,
    )

    mark_payment_succeeded(payment.id, charge.id)
    enqueue_receipt(payment.id)

    return payment
```

## Example 8: Pull Request Diff Review

### User

```text
Review this diff:

- if user.role == "admin":
-     delete_project(project_id)
+ delete_project(project_id)
```

## Review Summary

This change removes an authorization check before deleting a project. Unless authorization has been moved elsewhere, this is a serious security regression.

## Merge Recommendation

Request changes

## Findings

### Critical

- Possible authorization bypass. Removing the admin role check may allow non-admin users to delete projects.

### High

- The diff does not show a replacement authorization mechanism.
- The destructive operation is not protected in the visible code.

### Medium

- The code does not show audit logging for project deletion.
- The code does not show whether project ownership or organization-level permissions are checked.

### Low

- None found.

### Questions

- Has authorization been moved into `delete_project`?
- Are there tests proving non-admin users cannot delete projects?
- Should project owners or only admins be allowed to delete projects?

## Suggested Changes

If authorization is handled at this call site, restore the check:

```python
if user.role != "admin":
    raise ForbiddenError("Only admins can delete projects")

delete_project(project_id)
```

## Example 9: Data Processing Review

### User

```text
Review this pandas code:

df["conversion_rate"] = df["conversions"] / df["visits"]
df = df[df["conversion_rate"] > 0.1]
```

## Review Summary

The code is simple, but it does not handle zero or missing visits. This can create infinite or missing conversion rates and may affect filtering results.

## Merge Recommendation

Approve with comments

## Findings

### Critical

- None found.

### High

- None found.

### Medium

- Division by zero can produce `inf` values when `visits` is zero.
- Missing values in `conversions` or `visits` may silently propagate into `conversion_rate`.
- Filtering immediately after computing the metric may hide problematic rows instead of surfacing data quality issues.

### Low

- Consider naming the threshold as a constant if it has business meaning.

### Questions

- Should rows with zero visits be excluded, treated as zero conversion rate, or flagged as invalid?
- Should missing values fail the pipeline or be imputed?
- Is `0.1` a fixed business threshold or an experiment-specific parameter?

## Suggested Changes

One possible approach:

```python
import numpy as np

df["conversion_rate"] = np.where(
    df["visits"] > 0,
    df["conversions"] / df["visits"],
    np.nan,
)

filtered_df = df[df["conversion_rate"] > 0.1]
```

## Example 10: Over-Engineered Code Review

### User

```text
Review this code:

class StringProcessorFactoryManager:
    def create_processor(self, mode):
        if mode == "uppercase":
            return lambda value: value.upper()
        if mode == "lowercase":
            return lambda value: value.lower()
        raise ValueError("Unknown mode")
```

## Review Summary

The implementation works for the visible cases, but the abstraction appears heavier than necessary. A simpler function or mapping would likely be easier to maintain unless the project expects many processor types with complex behavior.

## Merge Recommendation

Approve with comments

## Findings

### Critical

- None found.

### High

- None found.

### Medium

- The class name and factory pattern may be over-engineered for two simple string transformations.
- The returned lambdas do not validate that `value` is a string, so non-string inputs will fail at runtime.

### Low

- The name `StringProcessorFactoryManager` is verbose and vague.
- Consider using a dictionary for simple mode dispatch.

### Questions

- Is this expected to grow into a larger plugin system?
- Should non-string values be rejected with a clear error?
- Are modes user-facing values that need documentation?

## Suggested Changes

For a simple implementation:

```python
PROCESSORS = {
    "uppercase": str.upper,
    "lowercase": str.lower,
}

def create_processor(mode: str):
    try:
        return PROCESSORS[mode]
    except KeyError:
        raise ValueError(f"Unknown mode: {mode}") from None

```

## Example 11: Code Review With Limited Context

### User

```text
Review this:

result = service.run(data)
```

## Review Summary

There is not enough context to perform a meaningful code review. The line is syntactically simple, but correctness depends entirely on what `service`, `run`, and `data` represent.

## Merge Recommendation

Not enough context

## Findings

### Critical

- None found from the visible snippet.

### High

- Not enough context to assess correctness, safety, performance, or maintainability.

### Medium

- Error handling is not visible.
- Input validation is not visible.
- The meaning and expected type of `result` are not visible.

### Low

- The line is readable in isolation.

### Questions

- What does `service.run` do?
- Can `service.run` fail?
- What type and shape should `data` have?
- What should happen if `result` is empty or invalid?
- Is this call synchronous, remote, expensive, or state-changing?

## Suggested Changes

Provide more surrounding code, especially:

- The definition of `service.run`
- The type or example value of `data`
- The expected behavior
- Error handling requirements
- Tests or failure cases

## Test Recommendations

Unable to recommend specific tests without more context. At minimum, test successful execution, invalid input, and failure behavior once the function behavior is known.

## Assumptions

- No reliable assumptions can be made from this one line alone.

Review this Python function:

def normalize_email(email: str) -> str:
    email = email.strip().lower()

    if "@" not in email:
        raise ValueError("Invalid email address")

    return email

## Review Summary

The function is clear, small, and easy to test. It handles basic normalization and rejects obviously invalid input.

## Merge Recommendation

Approve with comments

## Findings

### Critical

- None found.

### High

- None found.

### Medium

- The validation is intentionally minimal. It accepts some invalid email-like strings, such as `"@"` or `"user@"`.

### Low

- Consider renaming the error message to clarify that this is basic validation only.
- Consider documenting whether full RFC-compliant email validation is intentionally out of scope.

### Questions

- Is basic validation sufficient for this use case?
- Should internationalized emails be supported?
- Should this preserve case in the local part of the email address?

## Suggested Changes

If basic validation is enough, the current implementation is acceptable.

If slightly stricter validation is desired:

```python
def normalize_email(email: str) -> str:
    email = email.strip().lower()

    local_part, separator, domain = email.partition("@")
    if not separator or not local_part or not domain:
        raise ValueError("Invalid email address")

    return email
```