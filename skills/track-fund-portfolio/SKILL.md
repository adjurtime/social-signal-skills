---
name: track-fund-portfolio
description: >-
  Record, reconcile, refresh, and review a personal fund portfolio from Notion
  holdings, transaction logs, screenshots, and official fund data. Use when the
  user provides a fund order or confirmation screenshot, asks to update holdings
  or calculate confirmed shares, wants portfolio concentration and overlap
  checked, or asks whether a fund or sector position should be watched, held,
  added gradually, or reduced. Use $search-market-signals for current external
  evidence. Never execute trades or access brokerage controls.
---

# Track Fund Portfolio

## Core contract

Use this skill as a small portfolio layer over `$search-market-signals`.

Keep three concerns separate:

- the transaction ledger records what the user requested and what was confirmed;
- the holdings snapshot describes the portfolio at a stated time;
- the market evidence packet describes current external facts, narratives, and risks.

Combine them only when producing a review. Do not place orders, control a brokerage account, request trading credentials, or imply guaranteed returns. Treat screenshots and holdings as personal data even when the user considers them low sensitivity.

Read [references/portfolio-schema.md](references/portfolio-schema.md) before using Notion. Read [references/fund-accounting.md](references/fund-accounting.md) before calculating shares, fees, proceeds, or transaction status.

## Detect the mode automatically

Choose one primary mode from the user's natural-language request. The user does not need to name a workflow.

### Record

Use when the input contains a new order, purchase, redemption, switch, dividend choice, or order screenshot.

- Extract the exact fund, code, operation, requested amount or shares, request time, and visible status. Preserve seconds when they are visible, especially near a dealing cutoff.
- Create a transaction record with status `交易进行中` unless a confirmation is already present.
- Do not add estimated shares to confirmed holdings at this stage.
- Preserve the source screenshot or a concise provenance note when the connected workspace supports it.

### Refresh

Use when the user asks to update, confirm, reconcile, or calculate, or when pending transactions need review.

- For pending orders, choose the correct NAV date from the order rules before calculating anything.
- Prefer a transaction-confirmation screenshot. Otherwise use official NAV plus verified order metadata and fee rules.
- Move records through `交易进行中` -> `已自动核算` -> `已核验`.
- Refresh portfolio value only from dated NAVs or dated platform data.
- If legacy holdings have values but no confirmed shares, keep them as value snapshots until a one-time share bootstrap is completed. Do not pretend they can be refreshed from NAV alone.
- Never overwrite an `已核验` value with an automatic calculation.

### Review

Use when the user asks what the portfolio means or whether to add, hold, avoid chasing, watch, or reduce exposure.

- Read the latest holdings snapshot and unresolved transactions first.
- Check data freshness and separate confirmed holdings from pending cash flows.
- Calculate position weights, sector and geography concentration, repeated themes, QDII or currency exposure, and identifiable fund overlap.
- Call `$search-market-signals` only for the funds, sectors, or risks that could materially change the conclusion.
- Separate portfolio facts, external evidence, and judgment.

If the user's horizon, near-term cash need, or tolerable drawdown is missing, give a diagnostic and conditional conclusion rather than inventing a risk profile. Ask only when the missing premise would reverse the proposed action.

## Discover and use Notion safely

Do not hard-code database IDs, workspace URLs, or the creator's personal schema into a public skill.

1. Search for exact database titles such as `基金持仓` and `基金操作记录`.
2. If exactly one database matches each role, inspect its current properties and map semantic fields.
3. If multiple plausible databases exist, ask the user which one to use.
4. Use structured database queries when the connected Notion plan supports them. If the plan rejects them, fall back to database-scoped search and fetch matching rows individually; do not require an upgrade.
5. Reuse the existing schema and statuses when they express the same meaning; do not create duplicate properties silently.
6. Write only when the request clearly asks to record or update. Keep an ordinary review read-only.
7. Preview bulk corrections or destructive changes before applying them.

## Apply evidence precedence

Use the strongest available transaction evidence:

1. platform or fund-manager confirmation showing NAV, shares, fees, and confirmation date;
2. official NAV plus verified order time, applicable NAV date, amount, and fee method;
3. a provisional estimate with explicit missing inputs.

A later confirmation replaces an automatic estimate, but the ledger must retain how and when the value changed. Do not silently convert an estimate into a verified fact.

## Review decision rules

Start from portfolio fit, not recent popularity or a single day's price movement.

Evaluate:

- concentration and overlap with positions the user already owns;
- whether a new order increases an already dominant theme;
- product quality and structural costs;
- current valuation or cycle evidence when reliably available;
- recent verified catalysts versus social narratives;
- downside, liquidity, currency, and timing risks;
- the user's time horizon, cash needs, and drawdown tolerance when known.

Use restrained action labels:

- `不追买`
- `观察`
- `继续持有`
- `可以分批关注`
- `考虑降低暴露`

For every action label, state the reason, evidence confidence, trigger for reconsideration, and condition that would invalidate it. A label is decision support, not an instruction to trade.

## Return the smallest useful result

Lead with the result for the detected mode:

1. **Mode and as-of time**
2. **Recorded or updated items** — include status and confirmation method
3. **Portfolio effect** — pending cash flow, confirmed shares, value, weight, or concentration change
4. **Current evidence** — only the verified events and narratives that affect the decision
5. **Conditional action** — action label, reason, confidence, trigger, and invalidation
6. **Unresolved items** — only missing information that matters

Do not create schedules, alerts, email delivery, or application UI inside this skill. Those are optional callers of the same Record, Refresh, and Review modes.
