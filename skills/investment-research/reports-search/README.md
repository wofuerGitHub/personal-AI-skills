# Report Search

Find checked links to public company financial reports.

This skill is designed to locate annual and quarterly financial-report documents for public companies. It prefers SEC EDGAR for U.S. filers and official company investor-relations websites for non-U.S. issuers or companies that publish report PDFs outside the SEC system.

## What it helps with

- Finding recent 10-K and 10-Q filings.
- Finding annual reports, Form 20-F reports, interim financial reports, half-year reports, and quarterly results reports.
- Returning clean table or JSON output for downstream use.
- Handling private companies or missing public reports with a clear `not found` result.

## Best inputs

Provide:

- Company name or ticker.
- Number of annual and quarterly reports needed.
- Desired output format: table or JSON.
- Any jurisdiction or source constraints.

Example:

```text
Find the last 3 annual reports and last 3 quarterly reports for Apple as JSON.
```

## Expected output

The skill returns only checked report links. It does not output verification text or report excerpts.

Required fields:

1. Company
2. Type
3. Report
4. Period ended
5. Filed
6. Report link

If no public checked report is available, the result uses `Report: "not found"`.
