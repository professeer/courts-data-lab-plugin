---
name: search-syntax
description: Write correct Courts Data Lab case searches, including quoted phrases, party and text filters, dates, case types and paging. Use when building a search_cases call, when a search returns nothing or too much, or when the user asks how to search.
---

# Search syntax and filters

`search_cases` takes these inputs:

| Input | Meaning |
|---|---|
| `litigant` | Petitioner and respondent names. |
| `q` | Indexed case text and extracted order text. |
| `court`, `bench` | Court code from `list_courts`, and an exact bench name. A bench needs a court. |
| `filed_from`, `filed_to` | Filing dates, `YYYY-MM-DD`, inclusive. These are not hearing dates. |
| `case_type`, `status` | One case type. Status is `pending` or `disposed`. |
| `cnr`, `filing_number` | Exact identifiers. |
| `limit`, `cursor` | Page size (default 50, maximum 200) and the `next_cursor` from the last page. |

## How matching works

1. Letter case does not matter.
2. Without quotes, every word must match within one indexed field.
3. Double quotes ask for a phrase: `"arbitration agreement"`.
4. With both `q` and `litigant`, both must match the same case. That does not prove they occur in the same passage.
5. Name variants and word forms can change the matches. Try variants.
6. Missing or unextracted order text cannot match.

## Paging

1. The search is complete only when `next_cursor` is `null`. An empty page does not mean the end.
2. Use the cursor with exactly the same filters. Never edit it.
3. Count distinct `public_id` values across pages. Results can change while you page.

## When a search goes wrong

- Nothing found: drop a filter, try a name variant, or remove the quotes.
- Too many results: add a court, a status or a filing date range. Lower `limit` to save the case allowance.

## Rules for every answer

1. Cite each case by its `public_id`. Cite each order by the `order_url` the tool returned. Never make up a link.
2. State the filters you used and what the results cover. Say "sample" when you read only some pages. Say "complete available search" only when `next_cursor` was `null`.
3. A missing value or an empty search does not prove that an event did not happen. Courts publish late, and extraction lags.
4. A name match is evidence from indexed text. It does not prove who a party is, and it is not a legal finding about a person or firm.
5. Keep the court record apart from your own summary. Quote order text only from returned excerpts.
6. Each distinct case returned counts towards the organisation's case allowance. Prefer small, narrow searches.
