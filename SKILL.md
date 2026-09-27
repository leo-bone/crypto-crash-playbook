---
name: crypto-crash-playbook
description: This skill should be used when a crypto or high-beta risk-asset market experiences an extreme move (single-day drop over 10 percent, record liquidations, or a macro/geopolitical black-swan), and the user wants a full post-mortem plus an executable trading strategy. It produces a fact-checked causal-chain decomposition, a plain-language technical-factors explainer (ADL, oracle, funding rate, stablecoin de-peg, cross-exchange contagion), and a self-contained HTML strategy playbook (warning dashboard, hard risk rules, event-driven playbook, position/size template, post-mortem checklist, bull-market health dashboard).
agent_created: true
---

# Crypto Crash Playbook

## Overview

Turn any extreme crypto / risk-asset shock into (1) a verified causal-chain post-mortem and (2) a directly executable trading strategy SOP. The skill does NOT predict direction; its value is converting "what just happened" into "what to do before / during / after the next shock" — centered on leverage discipline and exchange-infrastructure-risk hedging.

## When To Use

- A major crypto crash, flash crash, record liquidation event, or macro/geopolitical headline (tariffs, rate decisions, regulation) triggers a cascade.
- User asks: "分析这次崩盘原因 + 给出可操作策略", "复盘 X 月 X 日暴跌", "做成可以执行的策略".
- Any request to build a reusable playbook for market-shock risk control.

## Workflow (execute in order)

### Step 1 — Fact-check first, never assume
Do NOT take the user's narrative or any single source at face value. Run parallel `WebSearch` queries across multiple independent sources:
- Aggregators / data: Coinglass (liquidation totals, long/short split, per-exchange breakdown), VanEck monthly recap (exchange mechanics).
- News: major financial outlets (Reuters, Bloomberg, Yahoo Finance, 澎湃, 经济日报).
- On-chain: Lookonchain / Blockscope / Gate.io whale tracking, stablecoin flow data, ETF flow data.
Cross-check numbers. Same event shows divergent dates, labels ("Black Friday/Tuesday/Saturday"), and liquidation totals ($19.3B official vs $30–40B with delayed reporting). Always label each fact as **已坐实 (confirmed)** vs **存疑 (disputed/unresolved)**.

### Step 2 — Build the five-link causal chain
Model every shock as: ① Macro/political catalyst → ② Exchange/infrastructure anomaly (oracle/ADL/engine freeze) → ③ Market-maker liquidity withdrawal → ④ Long-position cascade liquidation → ⑤ Retail wiped out / whales profit, with on-chain stablecoin inflow as the reversal fuel. Render as a compact SVG flow in the HTML output.

### Step 3 — Per-actor P&L table
Quantify separately: Retail (forced liquidations, % long), Market makers (delta-neutral blown by ADL, liquidity thinnest-since-2022, funding-arb yield collapse), Whales (pre-positioned shorts / dip-buying, note insider-trading suspicion as disputed), Exchange (compensation paid, founder denial). This exposes where the asymmetry came from.

### Step 4 — On-chain signal panel
Always include: stablecoin exchange net inflows, Fear & Greed Index (extreme = reversal zone), spot ETF flows, hash rate, funding rate. These are the leading indicators for the strategy, not just commentary.

### Step 5 — Fact-check section (confirmed vs disputed)
Explicitly separate: what is established (trigger, liquidation scale, exchange glitch, MM retreat, whale pre-positioning) from what remains unresolved (whether a single exchange "caused" it, whether a whale had insider info, the true liquidation total, whether the bottom is in). Avoid assigning sole blame without evidence; frame exchange failures as structural risk to hedge, not as a single guilty party.

### Step 6 — Produce the executable strategy SOP (core deliverable)
Output a self-contained HTML report with these sections, using tables + checklists:
- **Warning dashboard**: indicator → threshold → action (funding rate >+0.05%, OI/mcap ratio, F&G >75/<25, stablecoin weekly inflow, single-whale >$500M near macro event, policy keywords, exchange ADL/outage status). Map every indicator to a live feed via `references/data_sources.md` so the dashboard is executable, not theoretical.
- **Hard risk rules (non-negotiable)**: zero naked leverage in known catalyst windows (≤2x or flat 72h before; no naked leverage over weekends/holidays); per-event account risk ≤1–2%; total leverage ≤5x; mandatory stop-loss + account drawdown circuit breaker (-15% → flat); move collateral off-exchange across ≥2 venues; limit orders only under stress; never all-in on dip-buys (scale in 1/3 tranches).
- **Event-driven playbook**: T-72h (de-lever, move collateral, set alerts) → crash first 30–60 min (stay still, no market orders, avoid ADL/phantom-pricing window) → after (enter only when F&G extreme + stablecoin inflow + reversal signal coincide, scale in, tight stop) → aftershock weeks (do not assume V-bottom).
- **Position & stop template**: account event-risk cap, max leverage, tranche size, hard stop, circuit breaker, venue distribution.
- **Post-mortem checklist**: did I breach the rules, which warning lit up, did I fall into market-order/hold/all-in traps, was collateral safe, did on-chain signals give quantifiable entries, lessons written back into SOP.
- **Bull-market health dashboard**: ETF flows flip positive, BTC reclaims key levels, altseason broadens, stablecoin+settiment normalize — all four = "bull returns"; BTC-only + ETF outflows = relief bounce.

### Step 7 — Technical-factors explainer (for non-expert users)
Many users do not understand the *mechanics* that actually ate their PnL (ADL, oracle / phantom price, funding rate, stablecoin de-peg, cross-exchange contagion, slippage). When the user says they "don't understand the technical stuff" or asks to "sort out the other technical factors and mechanisms", produce a second, standalone, plain-language HTML (`<event>_technical_factors.html`) that decomposes each mechanism with the same 4-part template per factor: **是什么 / 10.x 那天怎么炸的 / 对你意味着什么 / 该怎么做**, plus intuitive analogies, 2–3 SVG diagrams (ADL cascade, oracle phantom-price loop, stablecoin de-peg classes), a factor→discipline mapping table, a corrected two-phase timeline, and a printable glossary card. Use `references/technical_factors.md` for the verified definitions and incident specifics so explanations stay accurate and consistent.

### Step 8 — Consolidate into one master console (preferred deliverable)
When the user wants the analysis "optimized / pushed forward / made executable as one thing", DO NOT leave three separate files. Produce a single self-contained `<event>_master_playbook.html` that consolidates everything into one interactive console with sticky nav:
- §0 Event overview (corrected two-phase timeline + responsibility split)
- §1 Warning dashboard (indicator / threshold / action + monitored checkboxes)
- §2 Hard risk rules (10 non-negotiable, "written into system" checkboxes)
- §3 Event-driven playbook (T-72h / crash 30-60min / after / aftershock weeks)
- §4 Technical-factors quick reference (11 mechanisms: one-line mechanic + what-to-do)
- §5 Bull-market health dashboard (4 interactive lights)
- §6 Post-mortem checklist
- §card Printable discipline card (print-optimized, @media print isolates it)
All checkboxes persist via `localStorage` (single key). Add a "print / export PDF" and "reset" button. This is the primary deliverable for execution; the deeper `<event>_technical_factors.html` remains the appendix for mechanics.

### Step 9 — Deliver & make reusable
Use `present_files` to preview the HTML(s). For repeating workflows, the user may ask to turn the analysis into a skill (this skill itself is the template).

## Key Principles

- **Don't predict, prepare.** Actionable value = leverage discipline + infrastructure-risk hedging, not directional calls.
- **Verify, don't assume.** Triangulate every number; mark disputed claims explicitly.
- **Structural framing for exchange risk.** When an exchange fails under stress, conclude "structural risk — hedge via off-exchange collateral and multi-venue distribution", never an unevidenced single-party blame.
- **Numbers need sources +口径.** State both official and estimated figures; note date/label discrepancies.
- **Consolidate for execution.** Prefer one interactive master console over scattered reports; deep-dives become appendices.

## Output

Self-contained HTML deliverables (light professional theme, tables, SVG diagrams):
1. `<event>_master_playbook.html` (PREFERRED): one consolidated interactive console (event overview + warning dashboard + risk rules + event playbook + technical quick-ref + health dashboard + post-mortem + printable card), localStorage-persisted checklists, print/export button.
2. `<event>_technical_factors.html` (appendix, when the user needs mechanics explained): per-factor 是什么/怎么炸的/意味着什么/该怎么做 + analogies + SVG diagrams + factor→discipline table + two-phase timeline + printable glossary.
3. `<event>_discipline_card.html` (optional): A4 print/PDF-ready one-pager for sticking on screen.

The skill repo also ships `README.md` (install + usage) and `references/data_sources.md` (live feed mapping for every dashboard indicator) so the SOP is executable end-to-end.

Interactive checklists (localStorage-persisted) are preferred for reusability.
