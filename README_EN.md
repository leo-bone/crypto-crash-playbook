# crypto-crash-playbook

[简体中文](README.md) | English

A reusable WorkBuddy skill that turns any extreme crypto / high-beta risk-asset shock into (1) a verified causal-chain post-mortem and (2) a directly executable risk-control SOP.

Core stance: **don't predict direction, prepare instead** — the value lies in leverage discipline + exchange-infrastructure-risk hedging, not in directional calls.

---

## Contents

| File | Purpose |
|---|---|
| `SKILL.md` | Workflow (10 steps): fact-check → causal chain → P&L → on-chain signals → technical factors → master console → companion live dashboard → delivery |
| `references/technical_factors.md` | Verified definitions (ADL, oracle / phantom pricing, funding rate, stablecoin de-peg, cross-exchange contagion) + 2025-10-10 case specifics |
| `references/data_sources.md` | Live data-source mapping for every warning-dashboard indicator |
| `tools/rwa_yield_radar.html` | **Companion live tool**: RWA yield-spread radar — browser-only, keyless (DefiLlama + Alternative.me APIs), real-time spread table + carry-signal lights + stablecoin panel + F&G alert tie-in + spread-history trend chart (local snapshots, JSON export) |
| `crypto-crash-playbook.zip` | Packaged skill for one-click install |

## Install

**Option A (source):** copy this folder to `~/.workbuddy/skills/crypto-crash-playbook/`

**Option B (zip):** unzip `crypto-crash-playbook.zip` into `~/.workbuddy/skills/`

## Built-in case study

Uses the **2025-10-10 BTC flash crash** (3h $123K→$102K, $19.3B liquidated, 87% long) as the worked example, covering: macro policy catalyst (tariffs) → centralized-exchange infrastructure anomaly (oracle / ADL — an amplifier, not the origin) → market-maker liquidity withdrawal → long-position cascade → retail wiped out / whales profit. See `SKILL.md` and the referenced deliverables.

## Usage

Next time any extreme move occurs (crash / record liquidation / macro black swan), just say:
> "Run crypto-crash-playbook: post-mortem + strategy"

to reuse the whole workflow.

## Disclaimer

This skill produces event post-mortems and risk-control methodology, **not investment advice**. Crypto assets are highly risky; make your own decisions.
