---
name: company-litigation-research
description: Find and summarise Indian court cases where a company or person is a party, using the Courts Data Lab tools. Use when the user asks about a company's or person's litigation, cases against or by a party, or a party's case history in the Supreme Court, Bombay High Court, Delhi High Court, NCLT or NCLAT.
---

# Company litigation research

Use this procedure to find the cases of one party.

## Procedure

1. Get the party name as the courts spell it. Ask for common variants (for example "Ltd" and "Limited", old names, group companies). Search each variant separately.
2. If the user names a court, call `list_courts` to get its code. A listed court can still be outside the user's access.
3. Call `search_cases` with `litigant` set to the name in double quotes, for example `"Tata Capital"`. Set `limit` to 5 for a first look. Add `court`, `status` or `filed_from` and `filed_to` when the user gives them.
4. For each match, show the matched party name, court, bench, case type, CNR or filing number, filing date, status and `public_id`.
5. Ask the user which matches are the right party before you go further. Different entities can share a name.
6. For a selected case, call `get_case` for parties, status and hearings. Use `list_hearings` when you need only the hearings.
7. If `next_cursor` is present, offer the next page. Use the same filters. An empty page with a cursor does not mean the end.
8. End with a coverage statement: the names searched, the filters, the number of cases returned, and whether the search is a sample or complete.

## Rules for every answer

1. Cite each case by its `public_id`. Cite each order by the `order_url` the tool returned. Never make up a link.
2. State the filters you used and what the results cover. Say "sample" when you read only some pages. Say "complete available search" only when `next_cursor` was `null`.
3. A missing value or an empty search does not prove that an event did not happen. Courts publish late, and extraction lags.
4. A name match is evidence from indexed text. It does not prove who a party is, and it is not a legal finding about a person or firm.
5. Keep the court record apart from your own summary. Quote order text only from returned excerpts.
6. Each distinct case returned counts towards the organisation's case allowance. Prefer small, narrow searches.
