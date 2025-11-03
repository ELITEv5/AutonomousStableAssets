# 🌞 SunDAI ASA — Autonomous Stable Asset

> **The World’s First Fully Autonomous Stable Asset Vault.**  
> Built on PulseChain. Designed for every chain.  
> Developed by **ELITE TEAM6**.

---

## 🧠 Overview

**SunDAI ASA** is an **Autonomous Stable Asset (ASA)** — a fully on-chain, immutable vault system that enables users to mint a decentralized stable asset (**pSunDAI**) by locking native collateral such as **PLS**, **wETH**, **HEX**, or other on-chain assets.

Unlike fiat-backed stablecoins, **SunDAI is algorithmic, collateralized, and self-governing** — no keys, no banks, no off-chain dependency.

SunDAI runs on math, collateral, and immutable code.

---

## ⚙️ Key Features

| Feature | Description |
|----------|--------------|
| 🧱 **Immutable Vaults** | Each user has a unique, keyless vault. No admin intervention required. |
| 🧮 **Autonomous Oracle System** | Self-refreshing oracle with ±10% clamp protection and stale-price fallback. |
| 💎 **Full Autonomy** | No governance keys. No pausable contracts. No upgrades. 100% autonomous. |
| 💰 **0.5% Annual Stability Fee** | Accrued automatically per vault — no interest rates, no custodians. |
| ⚖️ **Safe Collateralization (150%)** | Over-collateralized design protects against volatility and depegging. |
| 🔥 **Liquidation Auctions** | Fair, time-based liquidation rewards keep vaults balanced without admin action. |
| ⚡ **One-Click UX** | Deposit+Mint and Repay+Withdraw in a single transaction. |
| 🌍 **Chain-Agnostic Architecture** | Built to support native assets across EVM-compatible chains (PLS, ETH, BNB, etc.). |

---

## 🧩 Core Contracts

| Contract | Description |
|-----------|-------------|
| `pSunDAI_ASA_Token.sol` | ERC-20 stable asset token (Autonomous Stable Asset). |
| `pSunDAI_Stable_Vaultv3.sol` | Core vault logic — handles deposits, minting, repayment, withdrawals, and liquidations. |
| `pSunDAIoraclePLSX3.sol` | Oracle contract that aggregates stable pair data and clamps volatility. |

All contracts are immutable and deployed without admin ownership.  

---

## 🔒 Security & Design

SunDAI ASA is engineered for **complete autonomy and transparency**:
- No upgradeable proxies.
- No admin or owner functions.
- No centralized minting.
- No emergency control.
- Immutable after deployment.

If the oracle stops updating, users can still:
- Repay debt.  
- Withdraw collateral (if debt = 0).  
- Liquidate unsafe vaults.

This ensures **liveness, solvency, and permissionless safety** under all conditions.

---

## 🧠 Economic Model

- **Collateral Ratio:** 150% (minting), 110% (liquidation threshold).  
- **Stability Fee:** 0.5% annualized, automatically accrued.  
- **Liquidation Bonus:** 2%–5% dynamic, time-weighted.  
- **System Pause:** Automatic minting halt if global ratio < 130%.  

All parameters are **hardcoded and immutable** — no DAO votes or admin adjustments.

---

## 💬 Example Workflow

1. Deposit **WPLS** (or native wrapped token).  
2. Mint **pSunDAI** up to 66% of your collateral value.  
3. Repay any amount of pSunDAI at any time.  
4. Withdraw collateral once debt is cleared.  
5. Vault auto-rebalances and accrues minimal stability fees.

---

## 🌐 Official Links

- 🌞 **Website:** [https://www.sundaitoken.com](https://www.sundaitoken.com)  
- 📜 **Docs:** [https://github.com/ELITEv5/SunDAI](https://github.com/ELITEv5/SunDAI)  
- 🧑‍💻 **Developers:** dev@sundaitoken.com  
- 🧠 **Whitepaper: https://github.com/ELITEv5/SunDAI/blob/main/SunDAI_Whitepaper_2025.md

---

## 🪙 License

```text
MIT License

Copyright (c) 2025 ELITE TEAM6  
SunDAI Autonomous Stable Asset (ASA)  
Website: https://www.sundaitoken.com  
Contact: dev@sundaitoken.com

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
🏁 “Built for Freedom.”
No banks. No custodians. No permission.
Only math, code, and collateral.

— SunDAI ASA by ELITE TEAM6
