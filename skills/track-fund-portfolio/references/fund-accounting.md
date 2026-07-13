# Fund transaction accounting

Use these rules for off-exchange funds unless the product's official rules say otherwise.

## Determine the applicable NAV first

Do not choose the NAV date from the calendar date alone. Verify:

- request timestamp to the finest visible precision and the platform cutoff;
- whether the request day is a trading day for the fund;
- product type, including QDII, FOF, LOF, cross-border, or commodity-linked products;
- suspended subscriptions, delayed valuation, holidays in relevant markets, and platform-specific confirmation rules;
- whether the order was accepted, failed, cancelled, or partially confirmed.

Use the fund manager or another authoritative product source for official NAV and confirmation rules. A market-data site may help discovery but should not silently replace the primary source.

## Purchase calculations

When a percentage subscription fee is included in the requested amount:

`net subscription = requested amount / (1 + fee rate)`

`fee = requested amount - net subscription`

`confirmed shares = net subscription / applicable NAV`

When the fee is deducted separately:

`confirmed shares = requested amount / applicable NAV`

Record the fee separately. Use the platform-confirmed formula when it differs because of discounts, fixed fees, rounding, or product rules.

Do not report exact shares when the actual fee method is unknown. Report a provisional calculation or range and keep status `已自动核算` at most.

## Redemption calculations

For share-based redemption:

`gross proceeds = confirmed redeemed shares * applicable NAV`

`net proceeds = gross proceeds - redemption fee`

Redemption fees often depend on holding period and lot history. If the relevant lots or confirmed fee are unavailable, do not invent a precise net amount.

## Evidence and status

- `交易进行中`: order exists but applicable NAV, shares, or final outcome is not yet established.
- `已自动核算`: calculated from official NAV and verified order metadata; still subject to platform confirmation.
- `已核验`: matched to platform or fund-manager confirmation, or explicitly verified by the user from equivalent confirmation data.
- `失败` or `取消`: preserve the row; do not add it to holdings.

Confirmation evidence overrides an estimate. Automatic refreshes must never overwrite `已核验` figures.

## Rounding and reconciliation

Keep calculation precision internally, then follow the product's documented rounding rules. Small differences can arise from fee discounts, rounding, dividend reinvestment, or platform processing.

Reconcile against a later confirmation screenshot or periodic platform snapshot. Record the correction and its source rather than rewriting history without explanation.
