---
name: cut-or-scale-decision
description: Use when the merchant asks whether to stop, cut, keep or scale a campaign, ad set or platform. Gives one decision with the numbers behind it, or says what is missing. Read-only; the merchant applies the change in Flowfy.
---

# Cut or scale decision

Goal: a clear keep, cut or scale call for one campaign or platform, based on what it really returned to the store.

## Steps

1. Call `get_data_confidence` with `period` = `last_30_days`. If `meta.decision_safe` is false, stop: say what is missing and how to fix it (each item in `meta.missing` has a `fix_url`).
2. Call `get_profitability` for `last_30_days` at campaign level to get contribution after ads and the break-even ROAS.
3. Call `get_ads_report` at campaign level for the same period to read spend, platform-reported results and Flowfy-attributed results side by side.
4. Call `find_wasted_spend` and `find_growth_opportunities` for the same period to see whether the campaign is flagged.
5. Call `measure_change_impact` with `recent_changes` to see whether a change in the last 14 days is still settling. If it returns `too_early`, wait for its recheck date before cutting.

## How to decide

- Cut or pause when Flowfy-attributed contribution after ads stayed below zero over the period and spend is above the minimum the tools apply.
- Scale when the campaign is above break-even and has a growth finding, in steps of about 20% of its budget.
- Keep when results sit near break-even, volume is low, or a recent change is still settling.
- Never decide on platform-reported ROAS alone; platforms often count more sales than the store received.

## Rules

- Name the source of every number: ad platform, Flowfy or store.
- Never add amounts in different currencies or average ratios across campaigns.
- You cannot pause, cut or change budgets; tell the merchant where to do it in Flowfy.

## Answer format

1. Verdict in one line: keep, cut or scale, and for which campaign.
2. At most three numbers, each with its period and source.
3. Why, in one or two sentences.
4. What to do now, and one alternative.
5. Confidence, and what is missing (from `meta.missing`).
6. When to check again.

Use plain merchant language and explain a metric the first time you use it.
