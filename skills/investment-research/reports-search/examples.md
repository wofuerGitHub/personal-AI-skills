# Examples: Report Search Skill

These examples demonstrate expected behavior for the Report Search Skill, which finds valid links to company reports and returns them in a plain link table or JSON.

The examples are intentionally concise. Real responses should verify links where possible, preserve user-requested output formats, and clearly note access limitations.

---

## Example 1: Minimal request for annual reports

### User request

```text
Find the last 3 annual reports of Apple Inc. (AAPL).
```

### Expected assistant behavior

- Identify the company as Apple Inc. and ticker as AAPL.
- Search for the latest three annual reports from reliable official sources where possible.
- Prefer company investor-relations pages, SEC filings, or official annual-report PDF pages.
- Check that each link resolves or appears valid.
- Return a plain link table unless another format is requested.
- Include the report year, report type, source, and URL.
- Note any access or verification limitations.

### Example response shape

```md
## Report Links

| Company | Ticker | Report Type | Fiscal Year | Source | Link Status | URL |
|---|---|---|---:|---|---|---|
| Apple Inc. | AAPL | Annual report / 10-K | <year> | <SEC or Apple Investor Relations> | Valid | <url> |
| Apple Inc. | AAPL | Annual report / 10-K | <year> | <SEC or Apple Investor Relations> | Valid | <url> |
| Apple Inc. | AAPL | Annual report / 10-K | <year> | <SEC or Apple Investor Relations> | Valid | <url> |

## Notes

- I prioritized official company or SEC sources.
- Link status reflects availability at the time checked.
```

---

## Example 2: JSON output request

### User request

```text
Find the last 3 annual reports of Apple Inc. (AAPL) then output as JSON.
```

### Expected assistant behavior

- Return machine-readable JSON.
- Include company, ticker, report type, fiscal year, source, URL, and link status.
- Do not include unrelated analyst reports unless the user asks for research reports.
- Note if a link could not be verified.

### Example response shape

```json
{
  "company": "Apple Inc.",
  "ticker": "AAPL",
  "query": "last 3 annual reports",
  "reports": [
    {
      "report_type": "annual_report_10_k",
      "fiscal_year": "<year>",
      "source": "<official source>",
      "url": "<url>",
      "link_status": "valid",
      "notes": "Official filing or investor-relations source"
    },
    {
      "report_type": "annual_report_10_k",
      "fiscal_year": "<year>",
      "source": "<official source>",
      "url": "<url>",
      "link_status": "valid",
      "notes": "Official filing or investor-relations source"
    },
    {
      "report_type": "annual_report_10_k",
      "fiscal_year": "<year>",
      "source": "<official source>",
      "url": "<url>",
      "link_status": "valid",
      "notes": "Official filing or investor-relations source"
    }
  ],
  "limitations": [
    "Link status reflects availability at the time checked.",
    "Some sources may require cookies, JavaScript, or regional access."
  ]
}
```

---

## Example 3: Quarterly reports for a ticker

### User request

```text
Find Microsoft’s last 4 quarterly reports.
```

### Expected assistant behavior

- Identify Microsoft and ticker MSFT.
- Search for the latest four quarterly reports or 10-Q filings.
- Prefer SEC or Microsoft investor-relations sources.
- Return a table with links and filing dates if available.
- Avoid summarizing fundamentals unless asked.

### Example response shape

```md
## Report Links

| Company | Ticker | Report Type | Fiscal Quarter | Filing Date | Source | Link Status | URL |
|---|---|---|---|---|---|---|---|
| Microsoft Corporation | MSFT | 10-Q | <quarter> | <date> | <SEC or Microsoft Investor Relations> | Valid | <url> |
| Microsoft Corporation | MSFT | 10-Q | <quarter> | <date> | <SEC or Microsoft Investor Relations> | Valid | <url> |
| Microsoft Corporation | MSFT | 10-Q | <quarter> | <date> | <SEC or Microsoft Investor Relations> | Valid | <url> |
| Microsoft Corporation | MSFT | 10-Q | <quarter> | <date> | <SEC or Microsoft Investor Relations> | Valid | <url> |

## Notes

- These are links to report documents or filing pages.
- I did not extract financial data because the request was only to find reports.
```

---

## Example 4: Request using an ISIN

### User request

```text
Find the latest annual report for ISIN US5949181045.
```

### Expected assistant behavior

- Resolve the ISIN to the matching company and ticker if possible.
- State the resolved entity.
- Find the latest annual report.
- Return the report link with source and validation status.
- If the ISIN cannot be resolved confidently, ask for confirmation or provide the uncertainty.

### Example response shape

```md
## Resolved Entity

- ISIN: US5949181045
- Company: <resolved company>
- Ticker: <resolved ticker>

## Report Links

| ISIN | Company | Ticker | Report Type | Fiscal Year | Source | Link Status | URL |
|---|---|---|---|---:|---|---|---|
| US5949181045 | <company> | <ticker> | Annual report / 10-K | <year> | <official source> | Valid | <url> |

## Notes

- I resolved the ISIN before searching for the report.
- Link status reflects availability at the time checked.
```

---

## Example 5: User provides a report link

### User request

```text
Check this annual report link and return it in a table:
https://example.com/company/annual-report.pdf
```

### Expected assistant behavior

- Check whether the provided URL is reachable.
- Return a plain table.
- Preserve the original URL.
- Note whether the source appears official or third-party.
- Do not extract report contents unless requested.

### Example response shape

```md
## Report Links

| Report Type | Source Type | Link Status | URL | Notes |
|---|---|---|---|---|
| Annual report | <official / third-party / unknown> | <valid / invalid / unable to verify> | https://example.com/company/annual-report.pdf | <brief note> |

## Notes

- I checked the provided link only.
- I did not search for alternate reports because the request was to check the supplied link.
```

---

## Example 6: Multiple companies

### User request

```text
Find the latest annual reports for Apple, Microsoft, and NVIDIA.
```

### Expected assistant behavior

- Search each company separately.
- Return one latest annual report per company.
- Include ticker when confidently identified.
- Prefer official sources.
- Keep output compact.

### Example response shape

```md
## Report Links

| Company | Ticker | Report Type | Fiscal Year | Source | Link Status | URL |
|---|---|---|---:|---|---|---|
| Apple Inc. | AAPL | Annual report / 10-K | <year> | <official source> | Valid | <url> |
| Microsoft Corporation | MSFT | Annual report / 10-K | <year> | <official source> | Valid | <url> |
| NVIDIA Corporation | NVDA | Annual report / 10-K | <year> | <official source> | Valid | <url> |

## Notes

- I selected the latest available annual report for each company.
- If multiple official sources were available, I prioritized SEC or company investor-relations links.
```

---

## Example 7: Search with date range

### User request

```text
Find Tesla annual reports from 2021 to 2023.
```

### Expected assistant behavior

- Identify Tesla and ticker TSLA.
- Return annual reports for fiscal years 2021, 2022, and 2023 where available.
- Do not include reports outside the requested years.
- Note missing years if any are not found.

### Example response shape

```md
## Report Links

| Company | Ticker | Report Type | Fiscal Year | Source | Link Status | URL |
|---|---|---|---:|---|---|---|
| Tesla, Inc. | TSLA | Annual report / 10-K | 2023 | <official source> | Valid | <url> |
| Tesla, Inc. | TSLA | Annual report / 10-K | 2022 | <official source> | Valid | <url> |
| Tesla, Inc. | TSLA | Annual report / 10-K | 2021 | <official source> | Valid | <url> |

## Missing Reports

- None found.

## Notes

- I limited results to fiscal years 2021 through 2023.
```

---

## Example 8: Missing company context

### User request

```text
Find the last three annual reports.
```

### Expected assistant behavior

- Ask for the missing company, ticker, ISIN, or report source.
- Do not guess the company.
- Keep the clarification concise.

### Example response

```md
Which company should I search for? Please provide a company name, ticker, ISIN, or an existing report link.
```

---

## Example 9: No reports found

### User request

```text
Find annual reports for ExamplePrivateStartup Ltd.
```

### Expected assistant behavior

- Search for official or credible report sources.
- Return an empty result if no reports are found.
- State what was searched and why results may be unavailable.
- Avoid fabricating links.

### Example response shape

```md
## Report Links

| Company | Report Type | Fiscal Year | Source | Link Status | URL |
|---|---|---:|---|---|---|
| ExamplePrivateStartup Ltd. | Annual report | Not found | Not found | Not found | Not found |

## Result

No matching annual reports were found.

## Notes

- I did not fabricate report links.
- The company may be private, may not publish annual reports, or may use a different legal name.
- Try providing a ticker, ISIN, investor-relations page, or report URL.
```

---

## Example 10: Link access limitation

### User request

```text
Find the latest annual report for Nestlé and check the link.
```

### Expected assistant behavior

- Identify Nestlé and its relevant listing or company page.
- Find the latest annual report.
- Check whether the link is accessible.
- If the report page blocks access or requires JavaScript, state the limitation.
- Provide the best available official link.

### Example response shape

```md
## Report Links

| Company | Ticker / Identifier | Report Type | Fiscal Year | Source | Link Status | URL |
|---|---|---|---:|---|---|---|
| Nestlé S.A. | <identifier> | Annual report | <year> | <official source> | Unable to fully verify | <url> |

## Notes

- The link appears to point to an official report source.
- Full verification may be limited if the page requires cookies, JavaScript, regional access, or authentication.
```

---

## Example 11: User asks for report links plus summaries

### User request

```text
Find the latest semiconductor industry outlook reports and summarize each one.
```

### Expected assistant behavior

- Treat this as an investment research report search, not a company annual-report search.
- Search for relevant semiconductor industry outlook reports.
- Return report metadata, links, publication dates, and concise summaries.
- Note if full report access is restricted.
- Rank by relevance and recency.

### Example response shape

```md
## Reports

| Title | Source | Publication Date | Authors | Relevance | Access / Link Status | URL |
|---|---|---|---|---:|---|---|
| <report title> | <source> | <date> | <authors or Not found> | <score> | <open / restricted / unknown> | <url> |
| <report title> | <source> | <date> | <authors or Not found> | <score> | <open / restricted / unknown> | <url> |

## Summaries

### <Report Title>

<Concise summary of the report based on available metadata or accessible content.>

### <Report Title>

<Concise summary of the report based on available metadata or accessible content.>

## Notes

- Some investment research reports may require subscription access.
- Summaries are based only on accessible content and metadata.
```

---

## Example 12: User asks for analysis instead of links

### User request

```text
Find the latest Amazon annual report and analyze its fundamentals.
```

### Expected assistant behavior

- First find and validate the report link.
- Then, if the assistant has access to the report content, proceed with company fundamentals extraction.
- If only the link is available, provide the link and state that full analysis requires access to the report contents.
- Do not invent financial metrics.

### Example response shape

```md
## Report Link

| Company | Ticker | Report Type | Fiscal Year | Source | Link Status | URL |
|---|---|---|---:|---|---|---|
| Amazon.com, Inc. | AMZN | Annual report / 10-K | <year> | <official source> | Valid | <url> |

## Analysis Status

I found the report link. To analyze fundamentals, I need access to the report contents or a reachable filing page/PDF.

## Next Output After Access

Once the filing content is available, I can extract:

- Revenue
- Gross profit
- Operating income
- Net income
- EPS
- Cash
- Debt
- Total assets
- Total liabilities
- Shareholders’ equity
- Operating cash flow
- Capital expenditures
- Free cash flow
- Key trends, outlook, and risks

## Limitation

I will not invent financial metrics from a link alone.
```
