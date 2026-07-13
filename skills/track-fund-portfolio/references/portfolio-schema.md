# Portfolio data contract

Use semantic roles rather than fixed Notion property IDs. Inspect the live schema before reading or writing.

## Holdings snapshot

One row represents one exact fund share class at a stated snapshot time.

Minimum fields:

| Semantic field | Common Chinese labels | Rule |
| --- | --- | --- |
| Fund name | 基金名称, 名称 | Keep the exact share class |
| Fund code | 基金代码, 代码 | Store as text to preserve leading zeros |
| Confirmed shares | 持有份额, 确认份额, 份额 | Do not include pending estimates |
| Current value | 持仓市值, 当前金额, 当前市值 | Pair with an as-of date |
| Snapshot time | 快照日期, 净值日期, 最近更新 | Required for freshness checks |

Useful optional fields include latest NAV, cumulative buys, cumulative sale proceeds, cash dividends, displayed profit or loss, displayed return, category, sector, market, currency, QDII flag, and notes.

Do not treat `累计净投入` as identical to current cost basis after partial redemptions. Prefer deriving total economic profit from the transaction ledger when enough history exists.

### Bootstrap value-only holdings

A screenshot may provide current value and profit but omit shares. Treat such rows as dated value snapshots, not continuously refreshable holdings.

Complete a one-time bootstrap using one of:

1. a platform holding-detail or confirmation screenshot showing confirmed shares;
2. a verified platform export;
3. a dated platform value divided by the matching official NAV, clearly labeled as a provisional derivation until reconciled.

Do not combine a current displayed value with a NAV from a different valuation date, especially for QDII products. Until bootstrap is complete, new confirmed transactions may be recorded separately but must not create a false exact total-share figure.

## Transaction ledger

One row represents one order or confirmed cash-flow event. Recommended fields:

| Field | Purpose |
| --- | --- |
| 操作名称 | Human-readable title |
| 基金名称 / 基金代码 | Exact entity identity |
| 操作类型 | Buy, redeem, switch, dividend, correction |
| 申请金额 / 申请份额 | Original request |
| 申请时间 | Timestamp visible on the order |
| 状态 | 交易进行中, 已自动核算, 已核验, 失败, 取消 |
| 确认方式 | 自动核算 or 用户截图 |
| 确认净值 / 确认份额 / 确认金额 | Confirmed or calculated values |
| 手续费 | Explicit fee; do not assume zero |
| 确认日期 | Applicable transaction confirmation date |
| 备注 / 最近更新 | Provenance, uncertainty, and audit time |

Reuse equivalent existing properties. Add a missing property only when the user asks to adopt this schema or the write cannot be represented safely without it.

## Update flow

### New order

1. Add a ledger row.
2. Mark it `交易进行中`.
3. Leave confirmed holdings unchanged.

### Automatic reconciliation

1. Verify the applicable NAV date and official NAV.
2. Calculate with the correct fee method.
3. Save provenance and mark `已自动核算`.
4. Add the calculated shares to holdings only if the portfolio explicitly allows estimated shares; otherwise keep them pending.

### User-confirmed reconciliation

1. Match the confirmation to the original order.
2. Replace the automatic estimate with confirmed NAV, shares, amount, fee, and date.
3. Mark `已核验` and update confirmed holdings.
4. Preserve the earlier calculation in the audit note rather than deleting its history.

### Valuation refresh

Calculate `current value = confirmed shares * dated NAV`. Keep pending orders separate. Record the NAV source and as-of date.

If confirmed shares are missing, preserve the last dated platform value and report `share bootstrap required` instead of recalculating.

## Portable interface

Future browser extensions, macOS apps, and scheduled jobs should pass the same small objects:

- `PortfolioSnapshot`: as-of time plus holdings;
- `Holding`: exact fund identity, confirmed shares, dated value, and classification;
- `Transaction`: request, status, confirmation method, confirmed figures, fees, and provenance.

The UI may collect screenshots or manual entries, but it must not contain the search or accounting rules.
