# SunDAI — The First Autonomous Stable Asset Class

**Dev Team:** [ELITE TEAM6](https://t.me/eliteteam6)  
**Website:** [www.sundaitoken.com](https://www.sundaitoken.com)  
**License:** MIT  
**Chains:** PulseChain (pSunDAI), Base (bSunDAI), with cross-chain expansion planned.

---

## Abstract

**SunDAI** introduces a new category of decentralized assets: the **Autonomous Stable Asset (ASA)** — a self-regulating, self-pricing synthetic unit of account requiring no governance, oracles, or external upkeep.

Each SunDAI deployment (such as **pSunDAI** on PulseChain) combines a self-refreshing on-chain oracle with an immutable collateralized vault to produce a fully autonomous stable ecosystem.

SunDAI demonstrates that stable assets can exist without centralized price feeds, trusted parties, or administrative intervention — forming the foundation of a new, **self-sustaining DeFi primitive**.

---

## 1. Introduction — Why Autonomy Matters

Traditional stablecoins rely on external oracles, governance, and custodianship.  
Even decentralized models (e.g., MakerDAO) depend on **Chainlink feeds**, **DAOs**, or **multisigs** to maintain parity and safety.

SunDAI removes those dependencies entirely.  
It defines a **mathematically closed feedback system** where:

- Oracle prices are derived **autonomously on-chain**,  
- Vaults enforce collateralization **without governance**,  
- And the system’s stability emerges **without human intervention**.

This makes SunDAI the first truly **autonomous stable asset class** — an experiment in fully self-referential, cryptoeconomic design.

---

## 2. System Architecture

### Overview

SunDAI consists of two immutable contracts:

1. **pSunDAIoraclePLSX2** – a multi-pair autonomous oracle.  
2. **pSunDAIVault_ASA_Autonomous_Stable_Asset** – the vault system managing collateral, minting, and liquidation.

No administrators, no upgrade paths, and no off-chain dependencies.

---

## 3. Oracle Design — The Five-Pair Autonomous Oracle

### Concept

The **pSunDAIoraclePLSX2** is a **median-filtered, self-refreshing oracle** that replaces traditional Chainlink-style feeds.

It aggregates data from **five stable pairs** on PulseChain:

| Pair | Purpose |
|------|----------|
| DAI v1 / WPLS | Stable anchor 1 |
| DAI v2 / WPLS | Stable anchor 2 |
| USDC v1 / WPLS | Stable anchor 3 |
| USDC v2 / WPLS | Stable anchor 4 |
| USDT v1 / WPLS | Stable anchor 5 |

Each pair contributes a **time-weighted average price (TWAP)** and spot value.  
These are **median-filtered** to reject outliers and produce a single robust USD/PLS quote.

### Key Properties

- **Autonomous updates:** refreshes itself each block (no keeper calls).  
- **Median filtering:** removes manipulation via flash loans or low-liquidity pools.  
- **TWAP + Spot hybrid:** combines long-term average with short-term reactivity.  
- **Staleness guard:** auto-freezes if price data becomes too old (>24h).  
- **Deviation clamp:** limits jumps to ±10% per update for anti-volatility safety.

### Simplified math

prices = [TWAP_DAIv1, TWAP_DAIv2, TWAP_USDCv1, TWAP_USDCv2, TWAP_USDT]
validPrices = removeInvalid(prices)
medianPrice = median(validPrices)
clampedPrice = clamp(medianPrice, ±10%)



Output: **1e18-scaled USD/PLS** price feed.  
All autonomous, on-chain, immutable.

---

## 4. Vault Mechanics — The Autonomous Stable Engine

### Core Design

The **Vault Contract** allows users to deposit PLS (wrapped as WPLS), mint pSunDAI, repay, and withdraw — all without intermediaries.

Each vault tracks:

collateral
debt
timestamps (deposit, withdraw, accrual)



### Collateralization

Collateral Ratio = (Collateral * Price * 100) / (Debt * 1e18)



- Minimum Collateral Ratio: **150%**
- Liquidation threshold: **110%**
- Minimum system ratio: **130%**

Vaults are automatically protected:
- Under-collateralized vaults become liquidatable.
- Over-collateralized vaults may mint more pSunDAI.

### Interest Accrual

A **stability fee** of 0.5% per year accrues continuously:

fee = (debt * 0.5% * elapsedSeconds) / 31,536,000
debt += fee



Accrual occurs locally, per vault, during the next transaction.

### Liquidation Engine

If collateral ratio < 110%, the vault can be liquidated:

reward = baseCollateral + bonus (2–5%)



The reward dynamically scales based on time since last withdrawal (auction-style bonus curve).

### Emergency Unlock

Vaults can be force-unlocked after 30 days of inactivity **only if debt = 0** —  
ensuring funds cannot be trapped even under oracle downtime.

---

## 5. Economic Model

### Safety Layers

| Parameter | Purpose | Value |
|------------|----------|-------|
| COLLATERAL_RATIO | Base collateral requirement | 150% |
| LIQUIDATION_RATIO | Liquidation trigger | 110% |
| MIN_SYSTEM_HEALTH | System-wide CR floor | 130% |
| STABILITY_FEE_BPS | Annual interest | 0.5% |
| MAX_DEVIATION_BPS | Oracle price change cap | ±5% |

These constants create predictable, bounded economic behavior.

### System Health

System Ratio = (TotalCollateral * Price * 100) / (TotalDebt * 1e18)



If System Ratio < 130%, new minting pauses automatically.

---

## 6. Mathematical Appendix

### Collateral Ratio
ratio = (collateral * price * 100) / (debt * 1e18)



### TWAP Hybrid Update
price_new = median(valid_TWAPs)
if |price_new - lastPrice| > 5%: price_new = lastPrice



### Stability Fee
fee = (debt * STABILITY_FEE_BPS * elapsed) / (SECONDS_PER_YEAR * 10_000)



### Liquidation Reward
reward = baseCollateral + (baseCollateral * bonusBps / 10_000)



---

## 7. Autonomy and Immutability

SunDAI is **fully immutable** — once deployed:

- No admin keys  
- No upgradeability  
- No external upkeep  
- No off-chain oracles  

It is a living protocol, self-sustaining and self-pricing.  
The system continues operating indefinitely so long as the chain itself remains functional.

---

## 8. Cross-Chain Expansion

| Chain | Token | Status |
|--------|--------|--------|
| PulseChain | **pSunDAI** | Active |
| Base | **bSunDAI** | Planned |
| Ethereum | eSunDAI | Future |

Each deployment uses native liquidity pairs to build its own on-chain oracle.  
All remain autonomous and unlinked — no bridge or shared admin.

---

## 9. Historical Context

Autonomous assets mark a new era for decentralized finance.

- **2009–2019:** Custodial and fiat-backed stablecoins.  
- **2020–2022:** Governance-driven stablecoins (MakerDAO, FRAX).  
- **2023+:** Autonomous stable assets — no governance, no oracle dependency, no human inputs.

SunDAI demonstrates that price discovery, collateralization, and risk management can all exist *within* the protocol itself —  
a milestone in the evolution of self-sustaining DeFi systems.

---

## 10. Conclusion

SunDAI merges game theory, mathematics, and automation into a single immutable framework.  
It defines a **new asset class** — the *Autonomous Stable Asset (ASA)* — proving that financial equilibrium can exist entirely on-chain.

As the network expands across chains (pSunDAI → bSunDAI), the principles remain the same:
**autonomy, immutability, and self-sufficiency.**

---

### Dev Team

**ELITE TEAM6**  
Website: [www.sundaitoken.com](https://www.sundaitoken.com)  
Telegram: [https://t.me/eliteteam6](https://t.me/eliteteam6)

---

*MIT Licensed — for educational and research use.*
