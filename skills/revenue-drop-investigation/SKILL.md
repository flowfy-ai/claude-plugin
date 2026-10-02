---
name: revenue-drop-investigation
description: Use when the merchant says sales, revenue or orders dropped, or asks why a number went down. Separates a real sales drop from a tracking or measurement drop and names the main driver. Read-only.
---

# Revenue drop investigation

Goal: find out whether sales really dropped or only the measurement did, how much each cause explains, and what to do.

## Steps

1. Call `get_business_overview` with `compare_to` = `previous_period` to confirm the drop and its size.
2. Call `explain_performance_change` with `metric` = `revenue` for the same period. Read the drivers in order: order volume, average order value, per-platform moves and `tracking_coverage`.
3. Call `detect_anomalies` for the same period to find the day the drop started and its linked cause.
4. If a `tracking_coverage` driver or a purchase delivery drop appears, call `get_tracking_health` and `get_connection_health`; this is a measurement problem, not lost sales.
5. If cancellations or refunds drive the change, call `get_store_outcomes` with `breakdown` = `payment` to see whether cash-on-delivery failures rose.
6. Call `get_attribution_summary` to see which channel or platform lost orders.

## Rules

- Say clearly whether the drop is in real store sales or only in what was measured.
- The drivers add up to the total change; quote the top one or two with their share.
- Never add amounts in different currencies or average ratios.

## Answer format

1. Verdict in one line: real drop or measurement drop, and the main driver.
2. At most three numbers, each with its period and source.
3. Why, in one or two sentences.
4. What to do now, and one alternative.
5. Confidence, and what is missing (from `meta.missing`).
6. When to check again.

Use plain merchant language and explain a metric the first time you use it.
