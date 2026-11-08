---
name: case-history
description: Read the hearing history and court orders of one Indian court case from its CNR or filing number, using the Courts Data Lab tools. Use when the user gives a CNR, a case number or filing number, or asks what happened in a specific case.
---

# Case history from a CNR

Use this procedure to read one case.

## Procedure

1. Get the CNR exactly as the court prints it, for example `SCIN010499592024`. Without a CNR, get the court and the filing number, and the case type if the user knows it.
2. Call `lookup_case` with the `cnr`, or with `court` and `filing_number`.
   - One result: continue.
   - Several results: list them and ask which one. Never choose silently.
   - No result: ask the user to check the number and the court. The case can also be outside their access.
3. Call `get_case` with the `public_id`. It returns the parties, court, bench, filing date, status and hearings.
4. List the hearings from oldest to newest: date, judges, purpose or summary, and the order link when there is one.
5. Count how many hearings have an order link. Mark each missing value as "not recorded".
6. A listing date in an order is a date the court set. It does not prove that a hearing took place on that date.
7. End with the `public_id`, the number of hearings returned, and the number with an order link.

## Rules for every answer

1. Cite each case by its `public_id`. Cite each order by the `order_url` the tool returned. Never make up a link.
2. State the filters you used and what the results cover. Say "sample" when you read only some pages. Say "complete available search" only when `next_cursor` was `null`.
3. A missing value or an empty search does not prove that an event did not happen. Courts publish late, and extraction lags.
4. A name match is evidence from indexed text. It does not prove who a party is, and it is not a legal finding about a person or firm.
5. Keep the court record apart from your own summary. Quote order text only from returned excerpts.
6. Each distinct case returned counts towards the organisation's case allowance. Prefer small, narrow searches.
