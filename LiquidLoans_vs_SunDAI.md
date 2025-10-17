# ⚖️ Comparison: pSunDAI vs. Liquid Loans (USDL)

This document compares the **pSunDAI Autonomous Stable Asset (ASA)** protocol with **Liquid Loans (USDL)**,  
both native to PulseChain — highlighting key similarities, design choices, and philosophical differences.

---

## 🧠 Overview

Both systems allow users to lock **PLS** as collateral and mint a **stablecoin** without intermediaries.  
However, their approaches to stability, liquidation, and system design differ significantly.

| Feature | **pSunDAI (ASA)** | **Liquid Loans (USDL)** |
|----------|--------------------|--------------------------|
| **Core Asset** | pSunDAI – native autonomous stable asset | USDL – USD-pegged stablecoin |
| **Collateral** | 100% backed by PLS | 100% backed by PLS |
| **Collateral Ratio** | 150% minimum (safety-focused) | 110% minimum (efficiency-focused) |
| **Interest / Fees** | 0% interest, 0% ongoing fees | 0% interest, one-time borrowing fee |
| **Governance** | None (immutable by design) | None (governance-free, but multi-token) |
| **Admin Keys** | None | None |
| **Oracle Type** | Dual TWAP from Uniswap V1 + V2 | Chainlink-style oracle feed |
| **Liquidation System** | Public, direct vault liquidations | Stability Pool mechanism |
| **Reward Tokens** | None | LOAN token for rewards & incentives |
| **Redemption Mechanism** | None (organic equilibrium) | $1 USDL redeemable for $1 PLS |
| **Architecture** | Single immutable contract | Multi-contract DApp ecosystem |
| **Peg Type** | Autonomous Stable Asset (ASA) | Fiat-peg mimic via algorithm |
| **Target Audience** | Code-first DeFi users | Yield-focused borrowers & stakers |

---

## ⚙️ Core Design Philosophy

### 🧩 **Liquid Loans (USDL)**
- A **decentralized lending protocol** offering 0% interest loans against PLS collateral.  
- Introduces two tokens:
  - **USDL**: stablecoin pegged to $1.  
  - **LOAN**: secondary token capturing fees and rewards.  
- Uses a **Stability Pool** to auto-liquidate undercollateralized vaults.  
- Enables **redemption**: 1 USDL = $1 worth of PLS.  
- Focused on yield participation (staking, rewards, redemptions).  

### ☀️ **pSunDAI (ASA)**
- A **purely autonomous vault system** — no secondary token, no team, no treasury.  
- 150% collateral ratio ensures mathematical solvency at all times.  
- Dual on-chain oracles (TWAP) guarantee independence from off-chain feeds.  
- Simplicity-first design: one contract controls all mint, repay, and liquidation logic.  
- Peg stability emerges from collateral physics, not governance or incentives.  

---

## 🧮 Liquidation Model

| Mechanism | **pSunDAI** | **Liquid Loans** |
|------------|--------------|------------------|
| **Trigger** | Ratio <150% | Ratio <110% |
| **Who Liquidates** | Anyone (public) | Stability Pool participants |
| **Reward** | PLS + time-based bonus (up to 5%) | PLS + LOAN rewards |
| **Flow** | Vault-to-liquidator directly | Vault → Stability Pool |
| **Complexity** | Minimal | Multi-layered |
| **Dependency** | None | Requires active pool deposits |

> ✅ *pSunDAI’s liquidation system is simpler, fully autonomous, and doesn’t depend on reward farming.*

---

## 🧮 Oracle Architecture

| Aspect | **pSunDAI Oracle** | **Liquid Loans Oracle** |
|--------|--------------------|--------------------------|
| **Source** | Two largest WPLS/DAI pairs (TWAP) | Chainlink-style PLS/USD feed |
| **Update** | On-chain, during mint/repay/liquidate | Off-chain aggregation |
| **Dependency** | None | External providers |
| **Staleness Guard** | Built-in (300s window) | External freshness guarantee |
| **Philosophy** | Self-contained ecosystem | External reliability layer |

> ✅ *pSunDAI runs without any external price oracle dependency.*

---

## 💎 Token Economy Comparison

| Feature | **pSunDAI** | **Liquid Loans** |
|----------|--------------|------------------|
| Stablecoin | pSunDAI | USDL |
| Reward Token | None | LOAN |
| Fee Capture | None (fee-free system) | Borrowing & redemption fees |
| Value Flow | Direct user self-interest | LOAN staking & stability pool rewards |
| Monetary Policy | Code-defined | Algorithmic + staking-based |

> ✅ *pSunDAI is the minimal viable stablecoin model — no inflation, no yield layer, no governance token.*

---

## 🏗️ System Complexity

| Category | **pSunDAI** | **Liquid Loans** |
|-----------|--------------|------------------|
| Codebase | Single immutable vault + oracle | Multi-contract ecosystem |
| Maintenance | None (immutable) | Requires oracle updates |
| Front-End | Optional (scan-based) | Dedicated DApp UI |
| User Actions | Deposit → Mint → Repay | Borrow → Stake → Redeem |
| Launch Model | 90% community / 10% Destiny Vault | Controlled, DApp-led rollout |

> ✅ *pSunDAI’s simplicity = stronger long-term immutability and easier auditability.*

---

## 🧩 Stability Mechanism

| Concept | **pSunDAI (ASA)** | **Liquid Loans (USDL)** |
|----------|--------------------|--------------------------|
| **Peg Source** | Collateral math & arbitrage | Redemption-based floor |
| **Failsafe** | Overcollateralization | Stability Pool |
| **Liquidation Type** | Autonomous, direct | Delegated, incentivized |
| **Oracle Link** | On-chain pairs only | Chainlink feed |
| **Monetary Identity** | Autonomous Stable Asset | Dollar-Pegged Stablecoin |

---

## 🔮 Philosophical Summary

| Aspect | **pSunDAI / ASA** | **Liquid Loans / USDL** |
|--------|--------------------|--------------------------|
| Goal | Autonomous stable asset | Decentralized borrowing protocol |
| Model | Pure algorithmic collateral physics | Incentive-based monetary system |
| Reliance on Activity | None | Needs Stability Pool + Stakers |
| Upgrade Path | None (immutable) | Upgrade via frontend community |
| Design Ethos | *“Code is law.”* | *“DeFi lending reimagined.”* |

---

## 🧭 Conclusion

Both projects contribute vital infrastructure to PulseChain DeFi:

- **Liquid Loans** offers a *yield-generating lending ecosystem*, combining borrowing, staking, and redemptions under a managed community DApp.  
- **pSunDAI** is the *bare-metal stable asset layer* — a single immutable contract, fully autonomous, and governed only by math.

> **Liquid Loans** = DeFi Bank.  
> **pSunDAI** = Monetary Physics.

---

### 🔗 Related Docs
- [How to Use the pSunDAI Vault](https://github.com/ELITEv5/AutonomousStableAssets/blob/main/How_to_use_vault.md)
- [How Liquidation Works](https://github.com/ELITEv5/AutonomousStableAssets/blob/main/how_liquidation_works.md)
- [Autonomous Stable Asset (ASA) Concept](https://github.com/ELITEv5/AutonomousStableAssets/blob/main/asa-standard.md)

---

> **Immutable. Autonomous. Fair.**  
> pSunDAI represents the evolution from “stablecoin” to **Autonomous Stable Asset (ASA)** —  
> stability without control, trust without governance.
