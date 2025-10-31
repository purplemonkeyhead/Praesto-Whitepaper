# 01 — Platform Architecture

## Overview

This document details the architecture of the Praesto platform, including components, on-chain vs off-chain decisions, and core integrations.

## Components

* API Gateway (REST + WebSocket) for order routing, market data, AI queries
* Matching & Risk Engine (off-chain, low-latency) for order matching, margin checks and liquidation triggers; periodically commits state to L2/L3
* Settlement Layer (EVM-compatible) for custody, margin accounts, staking, reward distribution and governance actions
* AI Service Mesh for hosting/connecting model endpoints; every call is priced in PRAESTO and recorded on-chain as a usage event
* Indexing & Analytics (subgraphs + time-series DB) to prepare features for the AI models

## On-Chain vs Off-Chain

* Off-chain: matching, risk checks, AI inferencing — for speed
* On-chain: settlement, staking, AI credit accounting, buyback-distribute, governance — for transparency

## Integrations

* Oracles: Chainlink/Pyth-style feeds for crypto, forex and synthetic equity prices
* Bridging / Custody: to support multi-asset trading while keeping capital on an EVM L2