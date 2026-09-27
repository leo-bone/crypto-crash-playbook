# Technical Factors Reference — Crypto Shock Mechanics (verified)

Plain-language definitions + incident specifics for the `crypto-crash-playbook` skill's
technical-factors explainer. Sources: Binance official help/square posts, PANews ADL comparison,
Ethena official statements, Chaos Labs / LlamaRisk audits, Coindesk, Coinglass, multiple outlets.

## 1. Leverage & Liquidation
- Borrowed capital amplifies a position. 10x means a 10% adverse move wipes the margin.
- Liquidation = exchange auto-closes the position when margin < maintenance requirement.
- 2025.10.10: 87% of liquidations were longs, heavily 20–100x; BTC -18% triggered mass cascade.
- Action: catalyst-window leverage <=2x or flat; per-event risk <=1–2%; prefer isolated margin.

## 2. Mark Price
- Liquidation trigger uses a fair-value mark (usually multi-exchange spot avg + funding), not last trade.
- Risk: if the mark source is a single shallow order book, it becomes a "phantom price".
- Action: don't trust one venue's screen under stress; use limit orders; discount oracle-fed assets.

## 3. Funding Rate
- Perp has no expiry; funding (every 8h) pulls price to spot. >0 = longs pay shorts (crowded long);
  <0 = shorts pay longs.
- 2025.10.10: persistently high funding = crowded leveraged longs = fuel.
- Action: funding >+0.05%/8h or F&G >75 => de-risk warning.

## 4. Insurance Fund
- NOT user-loss insurance. Only covers the gap between bankruptcy price and liquidation execution price,
  so winners get paid. When exhausted, ADL triggers.
- COIN-M (coin-margined) funds are smaller => ADL earlier than USD-M (USDT-margined).
- Binance offers ADL guarantee compensation on major BTC/ETH/BNB USD-M contracts.
- Action: prefer USD-M major contracts; never treat the fund as a safety net.

## 5. ADL (Auto-Deleveraging) — most counter-intuitive
- Last resort after insurance fund exhausted. System force-closes PROFITABLE opposing positions at the
  bankrupt price to cover another trader's deficit. Winners pay for losers.
- ADL score (profitable side) = % PnL x effective leverage. Higher score = liquidated first.
- UI shows a 5-bar ADL indicator; 3+ bars = consider reducing leverage.
- 2025.10.10: ADL force-closed profitable market-maker neutral books => MMs became forced sellers,
  liquidity thinnest since 2022.
- Action: watch the ADL indicator; avoid high-leverage heavy-profitable positions in extremes; scale out profits.

## 6. Oracle / Phantom Price — infrastructure failure
- Oracles feed external prices on-chain. Healthy = multi-source aggregation (Binance+OKX+Coinbase+Chainlink).
- 2025.10.13 (aftershock, NOT 10.10): Binance unified account priced USDe/wBETH using ONLY its own shallow
  internal order book. A ~$90M USDe dump broke the thin book => oracle mis-priced USDe at $0.65.
  Premature liquidations -> more selling -> mis-price feedback loop. Binance froze deposits/withdrawals,
  crippling arbitrage. Same moment, Curve (DEX) USDe deviation was only 0.3% => protocol fine, CEX pricing broken.
- Binance acknowledged the oracle flaw and committed compensation (reported $283M USDe-specific to ~$600M broader).
- Action: cross-check prices; discount oracle-fed assets in events; watch for exchange deposit/withdrawal freezes.

## 7. Market Maker & Liquidity
- MMs continuously quote both sides; their withdrawal = empty order book = slippage.
- 2025.10.10: ADL blew up MM neutral books => MMs forced sellers => liquidity crisis, arb yield <4%.
- Action: limit orders only under stress; split large orders; treat thin book as hidden cost.

## 8. Stablecoin De-peg — three risk classes
- Fiat-backed (USDT/USDC): 1:1 off-chain reserves, most stable, issuer-credit risk.
- Synthetic/hedged (USDe): staked ETH + short ETH perp (delta-neutral); depends on CEX counterparty.
  2025.10.13 Binance oracle mis-price showed $0.65, but protocol stayed over-collateralized and processed
  $2B redemptions in 24h => pricing fault, not insolvency.
- Wrapped/yield (wBETH, BNSOL): derivative with staking leverage; oracle error => flash -90%.
- Action: reserve mostly USDT/USDC; keep USDe small; on de-peg, check 1:1 redeemability at protocol first.

## 9. Cross-Exchange Contagion
- Three channels: arbitrage bots (sync price across venues), shared collateral (one venue margin call
  hits others), shared/homologous oracles. Binance = 30–40% volume => epicenter spreads to all.
- 2025.10: Hyperliquid actually took $10.3B liquidations (4x Binance's $2.41B) => epicenter != biggest loser.
- Action: distribute assets across >=2 venues; understand collateral linkages before cross-venue hedging.

## 10. Slippage
- Difference between expected and executed price; worse when book is thin.
- 2025.10.10: stop-loss market orders filled several points below trigger.
- Action: use limit-stop (worst-price guard); split orders; accept partial fills.

## 11. On-chain / Market Indicators
- Stablecoin exchange net inflow: dip-buying "ammo" (Oct 2025: +$9.3B).
- Fear & Greed: extreme fear = potential reversal zone (not a buy alone).
- Spot ETF flows: institutional direction (Oct 2025 record -$3.47B outflow).
- Exchange net outflow: coins leaving venues = reduced sell pressure.
- Action: only call "bottom / bull returns" when all four align.

## Two-phase timeline (corrected)
- 10/10 (US evening): Trump 100% China tariff tweet -> VIX up, gold >$4,000, BTC $125K->$102K (-18%) in 3h.
- 10/10-10/11: ~$19.3B liquidations / 1.66M traders / 87% longs; Hyperliquid $10.3B, Bybit $4.65B, Binance $2.41B.
  Whale 0xb317... opened $1.1B short pre-crash, profited ~$192-200M (insider suspicion, disputed).
- 10/13: Binance internal-oracle failure -> USDe $0.65 on Binance, wBETH -90%, ATOM $4->$0.001; engine freeze
  ~100min, "order rejected"; Binance admitted oracle flaw + compensation.
- 10-end to 12: BTC ~$80K (-36%) mid-Nov; Dec weak bounce judged dead-cat; institutions still bought dips
  (Bitmine $480M ETH, Strategy), stablecoin +$9.3B ammo, but ETF -$3.47B.

## One-liner for the user
10/10 = leverage bubble lit by a political spark; 10/13 = exchange infrastructure fault that widened the wound.
