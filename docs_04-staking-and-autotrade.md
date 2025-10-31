# 04 — Staking & Stake-to-Autotrade

## Objectives

* Bind automation to economic commitment (no free-riding on AI)
* Protect users via bounded execution rights
* Reward long-term stakers with fee share, higher AI limits and early access to new models

## Flow

1. Stake PRAESTO -> receive sPRAESTO (non-transferable receipt).
2. Select Strategy: choose AI strategy template (scalping, perp swing, volatility capture, options selling, market-neutral).
3. Grant Execution Rights: bounded permissions via smart contract (market, leverage, notional limits).
4. Execution: AI creates orders -> matching -> settlement on-chain.
5. Settlement & Rewards: AI usage fees split between user rewards, strategy author, and treasury.

## Slashing & Misuse Prevention

* Executors stake PRAESTO and are subject to slashing upon verified violations.
* Detected via on-chain audit trails, verifiers, and community challenges.