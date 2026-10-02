---
name: tracking-fix-plan
description: Use when the merchant asks whether tracking works, why ad platforms report fewer or more purchases than the store, or how to fix tracking. Produces an ordered fix list. Read-only.
---

# Tracking fix plan

Goal: an ordered list of fixes that recovers the most lost purchase signals first.

## Steps

1. Call `get_tracking_health` for `last_7_days`. Unsupported events are expected and are not failures; focus on failed and not-mapped events.
2. Call `get_delivery_failures` for the destination or event with the most failures to read the error reasons.
3. Call `get_event_mappings` to find events that are not mapped to the destination's purchase event.
4. Call `get_connection_health` to find connections that need to be reconnected.
5. Call `get_conversion_readiness` for each Google Ads account to check conversion setup.
6. Call `get_data_confidence` to show how many store orders currently have a tracked purchase (`matched_purchase_coverage`).

## How to order the fixes

1. Reconnect anything disconnected or expired.
2. Fix delivery errors that block purchases.
3. Map unmapped purchase events.
4. Finish conversion setup on ad accounts.

## Rules

- Never call unsupported events a failure.
- Say how much each fix is expected to recover in purchase signals, not in sales.
- You cannot change settings; point the merchant to the place in Flowfy where each fix is made.

## Answer format

1. Verdict in one line: tracking is healthy, or the main problem.
2. At most three numbers, each with its period and source.
3. Why, in one or two sentences.
4. The fix list in order, and one alternative.
5. Confidence, and what is missing (from `meta.missing`).
6. When to check again (usually 2 days after the fix).

Use plain merchant language and explain a metric the first time you use it.
