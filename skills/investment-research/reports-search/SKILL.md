# Investment Research Reports Search

## Description
Search and retrieve investment research reports using a natural language query and structured filters. The skill locates relevant analyst notes, company briefings, sector studies, and market outlooks, then returns report metadata and concise summaries.

## Inputs
- `query` (string): The user’s search query, such as a company name, sector, event, or investment thesis.
- `sector` (string, optional): Filter results by industry sector.
- `region` (string, optional): Filter results by geographic region or market.
- `date_range` (string, optional): Filter results by publication date or range (e.g. `last 12 months`).
- `report_type` (string, optional): Filter by report category such as `equity research`, `credit analysis`, `macro outlook`, or `industry note`.
- `limit` (integer, optional): Maximum number of report results to return.

## Outputs
- `reports` (array): A list of matching report objects.
- Each report object should include:
  - `title` (string)
  - `source` (string)
  - `publication_date` (string)
  - `authors` (array of strings)
  - `summary` (string)
  - `report_url` (string)
  - `relevance_score` (number)

## Behavior
1. Validate the query and optional filters.
2. Construct a search request against the investment research repository.
3. Apply filters for sector, region, date range, and report type.
4. Rank results by relevance and recency.
5. Return the top matching reports with metadata and summaries.
6. Links always point to the original source with a unique URL.
7. Check for access limitations and note if full report content is unavailable.
8. If no reports are found, return an empty list and a message indicating no matches.

## Example
Input:
- query: "latest semiconductor industry outlook"
- sector: "semiconductors"
- date_range: "last 6 months"
- limit: 5

Output:
- A list of up to 5 reports about semiconductor industry outlook, including titles, sources, publication dates, authors, summaries, and links.
