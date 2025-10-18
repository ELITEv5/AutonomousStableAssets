# 🪙 Algorithmic vs Collateralized Stables  
### Understanding Why pSunDAI is Built Differently

---

## ⚖️ Overview

In the world of decentralized finance, “stablecoins” generally fall into two families:

| Type | Definition |
|------|-------------|
| **Algorithmic Stablecoin** | Uses mint/burn logic and market incentives to target $1 without hard collateral. |
| **Collateralized Stablecoin** | Every token is backed by on-chain collateral, enforcing solvency through code. |

---

## 🧠 The Core Difference

| Concept | Algorithmic Stable | Collateralized Stable (pSunDAI) |
|----------|--------------------|----------------------------------|
| **Backing** | None or partially backed by volatile tokens | Fully backed by on-chain PLS collateral |
| **Peg Mechanism** | Market incentives and supply expansion/contraction | Vault ratios and liquidation math |
| **Value Floor** | Zero — faith-based peg | Collateral value × liquidation ratio |
| **Primary Risk** | Death spiral during panic | Temporary liquidation of unsafe vaults |
| **Governance** | Often centralized or adjustable | Immutable smart contracts |
| **Transparency** | Complex balance logic | Fully auditable vault collateral |
| **Legal Posture** | May be seen as synthetic / unregistered | Commodity-like, provable asset backing |

---

## 💥 How Algorithmic Stables Work (and Break)

Algorithmic systems (e.g. UST, FRAX, AMPL) use **reflexive supply mechanics**:

1. Demand for stablecoin ↑ → Mint more
2. Demand ↓ → Burn or devalue paired token
3. System relies on traders restoring the peg

🧨 When confidence fails → minting hyperinflates the paired asset → peg collapses → value evaporates.

---

## 🧱 How pSunDAI Works

pSunDAI uses **mathematical overcollateralization** instead of belief:

1. Deposit **PLS** as collateral into a vault.
2. Mint up to **66%** of its USD value in pSunDAI (150% collateral ratio).
3. If value drops below 110%, vaults can be **liquidated** by anyone.
4. Collateral is always ≥ debt — guaranteed by code.

No central mint, no discretionary controls, no human intervention.

---

## 📊 Real-World Comparison

| Feature | Algorithmic (UST) | Collateralized (pSunDAI) |
|----------|------------------|---------------------------|
| **Backed By** | LUNA (speculative) | PLS (hard collateral) |
| **Collateral Ratio** | <100% | ≥150% |
| **Peg Enforcement** | Arbitrage incentive | Vault liquidation |
| **Supply Control** | Elastic algorithm | User deposits only |
| **Failure Mode** | Hyperinflation & collapse | Collateral liquidation |
| **Transparency** | Low | 100% on-chain |
| **Outcome** | Unstable | Stable by math |

---

## 🧮 Example Scenarios

### UST (Algorithmic)
> UST falls to $0.95 → protocol mints LUNA → LUNA price falls → peg fails → UST collapses.

### pSunDAI (Collateralized)
> PLS price drops 20% → unsafe vault liquidated → collateral sold → peg remains secure.

One depends on **human confidence**, the other depends on **arithmetic**.

---

## 💎 Why This Matters

Algorithmic stables chase price stability through **belief**.  
pSunDAI achieves stability through **solvency**.

That distinction makes it:
- **Safer** for holders  
- **Simpler** to audit  
- **Harder** to exploit  
- **Easier** to trust

---

## 🧾 Summary Table

| Feature | Algorithmic Stablecoin | pSunDAI (Collateralized) |
|----------|------------------------|---------------------------|
| Collateralized | ❌ No | ✅ Yes |
| Immutable | ❌ Often adjustable | ✅ Yes |
| Value Floor | ❌ None | ✅ ≥150% collateral |
| Peg Basis | Market faith | On-chain math |
| Failure Mode | Death spiral | Graceful liquidation |
| Legal Clarity | Risky synthetic | Commodity-backed asset |

---

### ✅ In One Line

> **pSunDAI isn’t an algorithmic stablecoin — it’s an autonomous, over-collateralized asset defined by math, not belief.**

---

Built for transparency.  
Powered by PulseChain.  
No team. No keys. No trust.  
Only code.

