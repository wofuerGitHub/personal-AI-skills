# Examples: Report Search

## Example 1: U.S. SEC filer

### User

```text
Find the last 3 annual and last 3 quarterly reports for MSFT.
```

### Expected behavior

Returns a table with Microsoft Corporation rows for the last three Form 10-K filings and last three Form 10-Q filings. Each row has one SEC main filing document link, not an SEC index page.

## Example 2: JSON output

### User

```text
Find the last 3 annual and quarterly reports for Apple as JSON.
```

### Expected behavior

Returns a JSON array using the exact keys:

```json
[
  {
    "Company": "Apple Inc.",
    "Type": "Annual",
    "Report": "Form 10-K",
    "Period ended": "YYYY-MM-DD",
    "Filed": "YYYY-MM-DD",
    "Report link": "https://www.sec.gov/Archives/..."
  }
]
```

No `Checked`, `verified`, `content check`, or source-notes fields are included.

## Example 3: Non-U.S. company

### User

```text
Find the last 3 annual and last 3 quarterly reports for Munich Re.
```

### Expected behavior

Uses Munich Re official annual reports and quarterly/interim report PDFs. Does not force 10-K or 10-Q terminology.

## Example 4: Private company or no public reports

### User

```text
Find annual and quarterly reports for SpaceX as JSON.
```

### Expected behavior

Returns a single object similar to:

```json
[
  {
    "Company": "SpaceX",
    "Type": "not found",
    "Report": "not found",
    "Period ended": "not found",
    "Filed": "not found",
    "Report link": "not found"
  }
]
```

## Example 5: Multiple companies

### User

```text
Run the skill against Berkshire Hathaway, Investor AB, RACE, and Apple.
```

### Expected behavior

Runs the lookup independently for each company. Uses SEC where available and official company sources where SEC quarterly reports are not available.

## Example 6: Avoid unchecked links

### User

```text
Give me annual report links for a company, but I do not care if they are checked.
```

### Expected behavior

Still checks links before output. The skill must not return unchecked links.

## Example 7: One canonical link only

### User

```text
Find AAPL reports and include SEC and Apple links.
```

### Expected behavior

Returns one canonical link per report unless the user explicitly requests alternative links. By default, SEC main filing document links are preferred for SEC filers.
