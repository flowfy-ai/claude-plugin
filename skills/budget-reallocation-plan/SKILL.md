---
name: budget-reallocation-plan
description: Use when the merchant asks how to split or move their ad budget between platforms or campaigns. Produces a step-by-step plan with amounts as ranges in the store currency. Read-only; nothing is changed and no outcome is simulated.
---

# Budget reallocation plan

Goal: move money from spend that returns too little to campaigns that are profitable and have room to grow, without changing the total unless the merchant asks.

## Steps

1. Call `get_data_confidence` for `last_30_days`. If `meta.decision_safe` is false, explain what is missing and give no amounts.
2. Call `get_profitability` for `last_30_days`, first at platform level, then at campaign level for the platforms that matter.
3. Call `find_wasted_spend` for the same period to list where money is lost and how much.
4. Call `find_growth_opportunities` for the same period to list campaigns above break-even with headroom.
5. Call `get_month_forecast` so the plan fits what is left of this month's budget and pacing.

## How to build the plan

- Take money first from the largest loss in `find_wasted_spend`, then the next.
- Give it to growth opportunities in order of their estimated upside.
- Change any one campaign by at most about 20% per step, and give every amount as a range in the store currency.
- Keep each currency separate; never move money between ad accounts in different currencies in one number.
- Say plainly that this is a plan, not a forecast: Flowfy does not simulate the result. Suggest `measure_change_impact` after 7 days to see what happened.

## Answer format

1. Verdict in one line: how much to move, from where, to where.
2. At most three numbers, each with its period and source.
3. Why, in one or two sentences.
4. The plan as up to three moves, and one alternative.
5. Confidence, and what is missing (from `meta.missing`).
6. When to check again (7 days after the change).

Use plain merchant language and explain a metric the first time you use it.
