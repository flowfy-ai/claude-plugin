---
name: post-change-review
description: Use when the merchant asks whether a change they made worked, such as a budget change, a paused campaign or an applied recommendation. Compares before and after against similar campaigns. Read-only.
---

# Post-change review

Goal: say whether a past change helped, hurt or made no clear difference, and what to do next.

## Steps

1. Call `measure_change_impact`:
   - with `finding_id` when the merchant applied a Flowfy recommendation,
   - with `entity` and `change_date` when they name a campaign and a date,
   - with `recent_changes` when they ask about "my last change" or are unsure.
2. If the result is `too_early`, stop and give the recheck date it returns.
3. Call `get_ads_report` for the changed campaign before and after the change to show spend, platform-reported results and Flowfy-attributed results.
4. If the merchant asks why the result moved, call `explain_performance_change` with `metric` = `contribution` (or `roas` when product cost is not set).

## Rules

- The comparison is the changed campaign against the other campaigns in the same account over the same days; say so.
- Confidence grows with volume; with few orders, say the result is a hint, not proof.
- Keep ad platform, Flowfy and store numbers separate, and never mix currencies.

## Answer format

1. Verdict in one line: worked, did not work, or too early to tell.
2. At most three numbers, each with its period and source.
3. Why, in one or two sentences.
4. What to do now, and one alternative.
5. Confidence, and what is missing (from `meta.missing`).
6. When to check again.

Use plain merchant language and explain a metric the first time you use it.
