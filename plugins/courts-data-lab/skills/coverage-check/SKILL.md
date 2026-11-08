---
name: coverage-check
description: Check what Courts Data Lab covers before answering a question about Indian court data, so the answer states its limits. Use before any count, trend, "all cases" or "no cases" claim, and when the user asks which courts, benches or dates are covered.
---

# Coverage check before an answer

Do this check before you give a count, a trend, or a claim that a party has no cases.

## Procedure

1. Call `list_courts`. It lists the published courts and benches. It does not show the user's access, the date range, or how complete a court is.
2. For a court the user names, call `list_benches` with its code.
3. Call `get_dictionary` when the answer depends on a field. It explains each field and the difference between raw, clean and inferred values.
4. Tell the user which courts you searched and which you did not.
5. If the question needs a total, read every page until `next_cursor` is `null`, and count distinct `public_id` values. If you stop early, say the number is a sample.
6. Say "coverage unknown" when you cannot confirm the date range or completeness for a court.
7. Never answer "no cases" from an empty search. Say "no cases found in the courts and filters searched", and name them.

## What the data does not hold today

- No judge filter, no hearing-date filter, no advocate filter. Use free text in `q` with care.
- No bulk export and no change feed.
- Courts outside the published list, for example most other high courts and consumer commissions.

## Rules for every answer

1. Cite each case by its `public_id`. Cite each order by the `order_url` the tool returned. Never make up a link.
2. State the filters you used and what the results cover. Say "sample" when you read only some pages. Say "complete available search" only when `next_cursor` was `null`.
3. A missing value or an empty search does not prove that an event did not happen. Courts publish late, and extraction lags.
4. A name match is evidence from indexed text. It does not prove who a party is, and it is not a legal finding about a person or firm.
5. Keep the court record apart from your own summary. Quote order text only from returned excerpts.
6. Each distinct case returned counts towards the organisation's case allowance. Prefer small, narrow searches.
