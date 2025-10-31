# Praesto: Native Token for the Praesto Trading Platform

> **Version:** 0.2 (Draft)
> **Status:** WIP
> **Last Updated:** 31 Oct 2025
> **License:** MIT

## Suggested GitHub Repository Layout

```text
praesto-whitepaper/
├── README.md               # Short overview for GitHub landing page
├── WHITEPAPER.md           # Full version (this document)
├── docs/
│   ├── 01-platform-architecture.md
│   ├── 02-market-structure.md
│   ├── 03-tokenomics.md
│   ├── 04-staking-and-autotrade.md
│   ├── 05-governance.md
│   ├── 06-security-and-compliance.md
│   └── 07-roadmap.md
├── diagrams/
│   ├── praesto-platform.png
│   └── ai-autotrade-flow.png
└── contracts/              # (future) Solidity / Rust / Move smart contracts
```

---

## 1. Executive Summary

Praesto is the **native utility and coordination token** of the Praesto trading platform — a multi-market venue where users can trade **spot, perpetuals, options, and futures with leverage** across **crypto, forex, and tokenized/ synthetic stocks** in a single interface.

What differentiates Praesto is the **AI Trading Layer**. This is a set of on-chain-accountable, off-chain-inferenced AI agents that can:

1. **Assist human traders** in real time by estimating trade success probabilities based on indicators, market depth, order flow and on-chain signals;
2. **Manage open positions** automatically (adjust TP/SL, deleverage, hedge, re-enter) following user-defined risk envelopes;
3. **Trade autonomously** on behalf of users **only if** they have staked PRAESTO for a certain period (“**Stake-to-Autotrade**”), so that automation is tied to economic commitment.

The PRAESTO token coordinates access, priority, discounts, AI capacity, rewards and governance.

---

## 2. Problem Statement

Current trading platforms — both centralized exchanges and most DEXes — suffer from five structural problems:

* **Market fragmentation**: crypto, forex and stocks live on different infrastructure, making cross-asset strategies expensive and slow.
* **AI is paywalled**: high-quality signal engines and strategy optimizers are available only to funds or in closed SaaS products.
* **No user–platform alignment**: users do not share in the upside of platform growth, even though their trading activity *creates* the value.
* **Inefficient fee capture**: trading fees are not recycled back to the tokenholders who provide liquidity, governance and model capacity.
* **Non-trustless automation**: most trading bots run off-chain without guardrails, so users must trust a black box.

Praesto addresses these with a single token, a single incentive system and a trading stack built for low latency but settled on-chain.

---

## 3. Solution Overview

Praesto combines **three layers**:

1. **Trading Layer**

   * Markets: spot, perpetual futures, dated futures, vanilla options
   * Assets: crypto (L1/L2 majors, midcaps), forex pairs (via oracles & synthetics), tokenized/synthetic equities
   * Margin: cross and isolated
   * Leverage: configurable per asset through risk parameters

2. **AI & Signal Layer**

   * Ingests: indicators (EMA, MA, RSI, MACD, VWAP, Bollinger, ATR), orderbook imbalance, funding, open interest, volatility, correlation, on-chain flows
   * Outputs: win probability, expected move, liquidation probability, scenario analysis
   * Operates in 3 modes: manual assist, semi-auto, full auto (stake-gated)

3. **Token, Staking & Governance Layer**

   * PRAESTO as **access token** for AI calls and trading fee discounts
   * PRAESTO as **value capture** for protocol fees, AI usage and liquidation proceeds
   * PRAESTO as **governance** for listings, risk, AI catalog and treasury

---

## 4. Platform Architecture

### 4.1 Components

* **API Gateway** (REST + WebSocket) for order routing, market data, AI queries
* **Matching & Risk Engine** (off-chain, low-latency) for order matching, margin checks and liquidation triggers; periodically commits state to L2/L3
* **Settlement Layer** (EVM-compatible) for custody, margin accounts, staking, reward distribution and governance actions
* **AI Service Mesh** for hosting/connecting model endpoints; every call is priced in PRAESTO and recorded on-chain as a usage event
* **Indexing & Analytics** (subgraphs + time-series DB) to prepare features for the AI models

### 4.2 On-Chain vs Off-Chain

* **Off-chain**: matching, risk checks, AI inferencing — for speed
* **On-chain**: settlement, staking, AI credit accounting, buyback-distribute, governance — for transparency

### 4.3 Integrations

* **Oracles**: Chainlink/Pyth-style feeds for crypto, forex and synthetic equity prices
* **Bridging / Custody**: to support multi-asset trading while keeping capital on an EVM L2

---

## 5. PRAESTO Token

**Name:** Praesto
**Ticker:** `$PRAESTO`
**Standard:** ERC-20 (EVM)
**Max Supply:** 7,000,000,000 PRAESTO

### 5.1 Core Utilities

1. **Trading Fee Discounts** – staking PRAESTO unlocks lower maker/taker fees and higher API rate limits.
2. **AI Compute Credits** – every AI request (signal, probability, portfolio optimization) is paid in PRAESTO.
3. **Stake-to-Autotrade** – users who lock PRAESTO for 30/60/90 days can authorize AI agents to trade on their behalf within predefined risk boxes.
4. **Priority & Capacity** – during high load, users with more staked PRAESTO get priority AI compute and faster order processing.
5. **Collateral Boost (optional, governance-gated)** – part of the staked PRAESTO can count toward the account health score.

### 5.2 Governance Utilities

PRAESTO is used to vote on:

* new market listings (new forex pairs, synthetic stocks, new perps)
* leverage ceilings and maintenance margin per market
* AI model catalog (which models become public and which stay premium)
* treasury allocations and incentive schedules

### 5.3 Value Capture

Protocol revenue flows through PRAESTO:

* a fixed share of **all trading fees** is periodically used to **buy PRAESTO from the market** and distribute it to stakers;
* **AI usage fees** are denominated in PRAESTO; revenue is split between treasury, AI providers and stakers;
* **liquidation fees** are directed to the **Safety Module** where PRAESTO is staked to underwrite risk.

---

## 6. Tokenomics

The token distribution follows the scheme shown in the image provided.

**Total / Max Supply:** **7,000,000,000 PRAESTO**

| Allocation        | %   | Tokens        | Description                                                                 |
| ----------------- | --- | ------------- | --------------------------------------------------------------------------- |
| Public Sale       | 25% | 1,750,000,000 | TGE + vesting; broad distribution and liquidity on CEX/DEX                  |
| Staking & Rewards | 15% | 1,050,000,000 | Emissions for traders, stakers, AI users; can be streamed over 4–5 years    |
| Liquidity Pool    | 10% | 700,000,000   | DEX/AMM liquidity, CEX market making, cross-chain liquidity                 |
| Team & Advisors   | 13% | 910,000,000   | 12-month cliff, then 36–48 month linear vesting; subject to performance/DAO |
| KOL               | 5%  | 350,000,000   | Influencer, partner, growth collaborations; vesting to avoid dumps          |
| Ecosystem Growth  | 25% | 1,750,000,000 | Grants, listings, AI model rewards, strategic integrations                  |
| Treasury Fund     | 7%  | 490,000,000   | DAO-controlled reserves for buybacks, audits, legal, market stabilization   |

**Check:** 1.75B + 1.05B + 0.7B + 0.91B + 0.35B + 1.75B + 0.49B = **7.0B** total.

### 6.1 Vesting & Release Logic (Example)

* **Public Sale:** 20% at TGE, 80% linear over 6–12 months depending on sale round.
* **Staking & Rewards:** streamed block-by-block; early years emit more to bootstrap liquidity and AI usage.
* **Team & Advisors:** 12-month cliff to align with long-term platform success; weekly or monthly linear vesting afterwards.
* **Ecosystem Growth & Treasury:** 100% on-chain, spend gated by DAO proposals and time-locks.

### 6.2 Emissions Policy

* The protocol can run a **declining emissions curve** for Staking & Rewards so that year 1 has the largest incentives.
* DAO may vote to **burn unallocated emissions** if the market doesn’t need them (supply-side discipline).

---

## 7. Staking & Stake-to-Autotrade

### 7.1 Objectives

* Bind automation to economic commitment (no free-riding on AI)
* Protect users via bounded execution rights
* Reward long-term stakers with fee share, higher AI limits and early access to new models

### 7.2 Flow

1. **Stake**: user stakes PRAESTO → receives sPRAESTO (non-transferable receipt).
2. **Select Strategy**: user chooses an AI strategy template (scalping, perp swing, volatility capture, options selling, market-neutral). Each template specifies market universe, max leverage, max notional per trade, max daily drawdown, and allowed order types.
3. **Grant Execution Rights**: user grants the AI executor a *bounded* permission via smart contract (e.g. "trade only BTC-PERP, ETH-PERP, max 5x, max 2% per order, max 5 orders per hour").
4. **Execution**: AI monitors market → creates orders → engine matches → settlement on-chain.
5. **Settlement & Rewards**: protocol charges AI usage fees (in PRAESTO) and distributes: **user rewards**, **strategy author share**, **protocol treasury**.

### 7.3 Slashing & Misuse Prevention

* AI executors must stake PRAESTO themselves — if they violate constraints (over-leverage, trading a non-whitelisted market, frontrunning), their stake can be **slashed**.
* Violation can be detected via:

  * on-chain order audit trail
  * periodic verifier scripts
  * community challenge mechanism

---

## 8. AI Layer (Deeper Dive)

### 8.1 Inputs

* Price & volume from CEX and DEX venues
* Orderbook snapshots and depth metrics
* On-chain transfers and CEX inflow/outflow heuristics
* Indicator stack computed per timeframe (1m, 5m, 15m, 1h, 4h, 1d)
* Funding, OI, perp skew, basis
* Correlation matrix across BTC, ETH, majors, forex majors and synthetic equities

### 8.2 Outputs

* **Trade Confidence Score** (0–100)
* **Target Direction** (long/short/flat)
* **Position Size Recommendation** based on volatility and liquidity
* **Risk Flags** ("high liquidation density below", "thin book", "funding spike", "macro event imminent")

### 8.3 Human–in-the-Loop vs Full Auto

* **Human-in-the-Loop**: AI produces signals, trader confirms → lowest risk, no stake requirement
* **Semi-Auto**: AI places entries, trader manages exits → requires small stake
* **Full Auto**: AI manages entries, TP/SL, trailing, hedges and deleverage → requires time-locked stake and stricter limits

---

## 9. Business Model & Revenue Streams

Praesto’s business model is intentionally simple and transparent. The platform earns in three primary ways and recycles a meaningful part of that revenue back into the token economy.

### 9.1 Core Revenue Sources

1. **Trading Fees (primary)**

   * Every spot, perp, options or futures trade pays a small fee.
   * Example baseline (can be tuned by DAO): **0.08% taker / 0.02% maker**.
   * Users who **stake PRAESTO** or reach higher volume tiers pay less.
   * Because the platform supports **crypto, forex and synthetic stocks**, this becomes a very broad, multi-venue fee stream.

2. **Liquidation & Risk Fees**

   * When overleveraged users are liquidated, the protocol charges a **liquidation fee**.
   * Part of this fee is used to compensate the **Safety Module** (PRAESTO stakers underwriting risk), and part is pure **protocol revenue**.
   * Since leveraged products (perps/futures/options) are a major part of Praesto, this is a non-trivial revenue line.

3. **Treasury / Proprietary Investments**

   * Revenue that accumulates in the DAO Treasury (from trading fees, AI fees, listing fees, liquidation fees) can be **actively deployed**:

     * to provide protocol-owned liquidity (POL) on DEXes;
     * to backstop markets with low liquidity;
     * to earn low-risk on-chain yield;
     * to co-invest in ecosystem integrations.
   * This makes the treasury a **productive asset** instead of a passive wallet.
   * Returns from these deployments flow back to the treasury and can be directed by governance.

4. **(Optional) AI Usage Fees**

   * Every AI inference, signal or portfolio optimization call is priced in PRAESTO.
   * This creates a second, usage-based revenue line next to trading fees.
   * AI revenue can be split 40% treasury / 40% AI providers / 20% stakers (example split).

### 9.2 Value Recycling (Buyback & Distribute)

Praesto is designed so that protocol success → token demand.

* A fixed percentage of **net protocol revenue** (trading + liquidation + AI + treasury returns) is periodically used to **buy $PRAESTO on the open market**.
* Bought tokens are then:

  1. **Distributed to stakers** (staking & rewards pool) to reward long-term alignment; or
  2. **Sent to the DAO treasury** for future emissions; or
  3. **Burned** if the DAO wants to make supply increasingly scarce.

This turns trading activity and liquidations — which are natural byproducts of leveraged markets — into **direct demand** for the token.

### 9.3 Why This Model Works

* **Simple to explain:** “We charge a small fee on every trade and on every liquidation. We use that money to buy back the token.”
* **Aligned with power users:** high-volume and quant traders get lower fees if they stake; they also benefit from a healthier token because it improves liquidity.
* **Cyclical upside:** in volatile markets, liquidations rise → protocol revenue rises → buybacks rise.
* **Treasury optionality:** the DAO can choose to be conservative (hold stablecoins) or aggressive (deploy into POL/yield) depending on market conditions.

---

## 10. Security, Compliance & Risk

* Two or more **independent smart contract audits** before mainnet
* **Module isolation**: staking, trading, governance and AI accounting are separate contracts
* **Oracle risk mitigation**: multiple feeds, medianizers, circuit breakers for volatile pairs
* **Geo-/KYC-gated front-end** for high leverage or restricted assets, while keeping contracts permissionless
* **AI decision logging** for post-trade analysis and disputes

---

## 11. Governance (Praesto DAO)

* PRAESTO holders can **propose**, **vote** and **execute** protocol changes through a timelock
* Voting power = staked PRAESTO × lock multiplier
* Delegation supported for strategy builders, market makers, and AI providers
* DAO treasury controls ecosystem growth (25%) and treasury fund (7%) allocations

---

## 12. Roadmap (Indicative)

**Phase 0 – Foundation (Q4 2025)**

* Testnet trading (spot + perps)
* Base AI signal API
* Staking MVP
* Token deployment on EVM L2

**Phase 1 – Multi-Asset (Q1–Q2 2026)**

* Add forex & synthetic equities
* Launch options & dated futures
* Start fee buyback & distribute
* AI catalog v1

**Phase 2 – Permissionless AI (Q3 2026)**

* External AI providers onboard
* Revenue share to model authors
* Full Stake-to-Autotrade for all users

**Phase 3 – Full DAO (Q4 2026)**

* Treasury fully DAO-controlled
* Risk parameters on-chain
* Long-term incentive program

---

## 13. README.md (Short GitHub Version)

```markdown
# Praesto — AI-Powered Multi-Asset Trading

Praesto is a trading platform for spot, perpetuals, options and futures with leverage, covering crypto, forex and synthetic stocks. The native token **$PRAESTO** powers fee discounts, AI access, staking, governance and the unique Stake-to-Autotrade feature.

## Key Features
- Trade crypto, forex and stocks in one place
- AI integrated for probability-based trading
- Stake-to-Autotrade (let AI trade for you)
- Fee share + buyback & distribute to stakers
- DAO-governed listings, risk and treasury

See the full whitepaper in `WHITEPAPER.md`.
```

---

## 14. Disclaimer

This document describes a **technical and economic design** for the Praesto protocol. It is **not** financial, investment or legal advice. Launch parameters, vesting schedules, token allocations, supported assets and AI features may change based on audits, regulation or DAO votes.