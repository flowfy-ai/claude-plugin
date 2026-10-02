---
name: weekly-optimization-review
description: Use when the merchant wants a weekly check of their store and ads, asks what to improve this week, or says optimize. Produces a short prioritized review with one action per issue. Read-only; nothing is changed.
---

# Weekly optimization review

Goal: tell the merchant in a few lines what changed this week, what needs attention, and the one or two actions worth doing now.

## Steps

1. Call `review_account` with `period` = `last_7_days`. It returns the health summary, up to five findings ranked by impact, and the tool to call for each finding.
2. Call `get_business_overview` with `period` = `last_7_days` and `compare_to` = `previous_period` for the headline numbers.
3. For the top finding only, call the tool named in its `next_tool` (for example `find_wasted_spend`, `find_growth_opportunities`, `get_tracking_health` or `get_connection_health`) to get the evidence.
4. If revenue, orders or spend moved by more than 10%, call `explain_performance_change` for that metric to name the driver.
5. If any result has `meta.decision_safe` = false, call `get_data_confidence` and say what is missing before recommending anything.

## Rules

- Lead with the biggest money impact, not with the longest list.
- Keep ad platform numbers, Flowfy-attributed numbers and store numbers apart, and name the source of each number.
- Never add amounts in different currencies or average ratios across campaigns; use the totals the tools return.
- A missing value is unknown, not zero.
- "Optimize" means analyze and recommend. You cannot change budgets, campaigns or settings; tell the merchant where to apply the change in Flowfy.

## Answer format

1. Verdict in one line.
2. At most three numbers, each with its period and source (store, Flowfy or ad platform).
3. Why, in one or two sentences.
4. What to do now, and one alternative.
5. Confidence, and what is missing (from `meta.missing`).
6. When to check again (usually in 7 days).

Use plain merchant language and explain a metric the first time you use it.
