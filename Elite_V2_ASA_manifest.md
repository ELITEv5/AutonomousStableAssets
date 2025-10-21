# 🧬 pSunDAIvaultV2 — Autonomous Final Form  
### Immutable Stable Vault — PulseChain Edition  
by **Elite Team6**

---

## 🔥 Overview

**pSunDAIvaultV2** is an *immutable, autonomous* stable asset vault built for the **PulseChain** ecosystem.  
It represents the **final-form evolution** of decentralized collateralization — a vault that requires no admin, no governance, and no human maintenance.

Every rule of operation — collateralization, liquidation, safety ratios, cooldowns, and oracle management — is **self-enforced** on-chain, deterministically and transparently.

> “No keys. No upgrades. No rug paths.  
> Only math, code, and immutable logic.”

---

## ⚙️ Core Principles

| Principle | Description |
|------------|-------------|
| **Autonomy** | All functions are self-regulating. There are no admin modifiers or upgrade hooks. |
| **Immutability** | Once deployed, parameters and logic cannot be changed. Constants are hardcoded at compile time. |
| **Determinism** | Each vault operation yields a predictable, auditable result governed by mathematics — not governance. |
| **Oracle Safety** | Dual-layer oracle system with timestamp enforcement, ±5% clamp, and stale-data fallback. |
| **Collateral Integrity** | PLS and WPLS are handled directly; collateral cannot be rehypothecated or redirected. |
| **Permissionless Operation** | Any address can deposit, mint, repay, withdraw, or liquidate within protocol-defined bounds. |
| **Final Form** | The protocol contains no owner, admin, or upgrade roles. It will operate until the chain itself ends. |

---

## 🧱 System Constants

| Constant | Value | Description |
|-----------|--------|-------------|
| `COLLATERAL_RATIO` | 150 | Required collateralization % |
| `LIQUIDATION_RATIO` | 110 | Minimum safety threshold % |
| `MAX_BONUS_CAP` | 200 | 2% liquidation bonus cap |
| `MAX_BONUS_BPS` | 300 | Max 3% bonus during liquidation |
| `WITHDRAW_COOLDOWN` | 1800 | 30-minute cooldown |
| `AUCTION_TIME` | 10800 | 3-hour liquidation auction window |
| `MIN_ACTION_AMOUNT` | 0.1 PLS | Smallest valid action |
| `ORACLE_FAIL_DELAY` | 24 hours | Delay before emergencyWithdraw |
| `SAFE_PRICE_CLAMP_BPS` | 500 | ±5% deviation clamp |
| `MIN_PRICE` | 1e12 | $0.000001 |
| `MAX_PRICE` | 1000e18 | $1000.00 |

---

## 💡 Key Features

### 🧱 Vault Mechanics
- **150% Collateral Ratio** — minting threshold  
- **110% Liquidation Ratio** — safety floor  
- **Automatic ±5% Oracle Clamp**  
- **24h Oracle Failure Delay**  
- **3h Liquidation Auction Window**  
- **Permissionless Everything**  

### ⚡ User Functions
| Function | Description |
|-----------|-------------|
| `depositPLS()` | Deposit native PLS (auto-wraps into WPLS). |
| `deposit()` | Deposit WPLS directly. |
| `mint()` | Mint pSunDAI against collateral (150%+ ratio required). |
| `repay()` | Burn pSunDAI to repay vault debt. |
| `withdrawPLS()` / `withdraw()` | Withdraw collateral if safe. |
| `emergencyWithdraw()` | Oracle-failure recovery after 24h delay. |

### 🧠 Read / UI Functions
| Function | Description |
|-----------|-------------|
| `vaultSummary()` | Returns collateral, debt, ratio, max mintable, last price. |
| `maxMintable()` | Calculates remaining mintable pSunDAI based on live price. |
| `_collateralRatio()` | Internal ratio check for safety. |
| `_isSafe()` | Evaluates vault health based on oracles. |

---

## 🧩 Dual Oracle System — Redundant Price Safety

The vault aggregates **two fully on-chain TWAP oracles** to achieve redundancy, accuracy, and censorship resistance.

### 1️⃣ `pSunDaioracle` — Dual WPLS/DAI Oracle
- Uses **two PulseX WPLS/DAI** pairs.  
- Calculates a 30-minute TWAP average.  
- Fallback to last valid price if both pairs stale.  
- Purpose: anchor feed for DAI liquidity.

### 2️⃣ `pSunDAITriOracleEliteV2` — Triple Oracle (WPLS/DAI + WPLS/USDC)
- Uses **three pairs:**  
  - WPLS/DAI (V1)  
  - WPLS/DAI (V2)  
  - WPLS/USDC  
- Produces a **median TWAP** normalized to 1e18 precision.  
- Filters out stale or illiquid pools automatically.  
- Anyone can call `updatePublic()` to refresh TWAPs.  
- Once linked to vault, becomes **immutable forever**.

---

## 🔮 How the Oracles Work Together

### Step 1 — Independent Feed Sampling
The vault queries both:
```solidity
(p1, ) = oracle1.getPriceWithTimestamp();
(p2, ) = oracle2.getPriceWithTimestamp();
Step 2 — Cross-Validation
Both oracles return 1e18-normalized USD prices for WPLS.
If both valid and within 5% deviation:

solidity
Copy code
uint256 avg = (p1 + p2) / 2;
require((diff * 10000) / avg <= 500, "Oracle deviation >5%");
Else, it safely falls back to the valid source.

Step 3 — Clamp + Record
The final price is stored as lastSafePrice, ensuring stability across vault operations and emergency states.

🧠 Design Philosophy
“Autonomous systems do not need governance;
they need invariants that make governance unnecessary.”

The Elite Protocol standard defines immutable, self-regulating DeFi primitives that require no multisig, DAO, or admin keys.
All safety parameters are constants encoded directly in bytecode.
Every user interacts under identical, transparent rules — permanently.

🛡️ Security Design
Layer	Security Mechanism
Oracle Layer	±5% deviation clamp, 300s staleness check, reserve threshold, triple-source redundancy
Vault Layer	NonReentrant guard, cooldown timers, liquidation caps
Economic Layer	150% CR enforcement, 110% liquidation, deterministic reward bounds
Emergency Layer	24h delay for oracle failure exit, no admin override
Integrity Layer	Immutable parameters, no upgrade proxies, no external governance

🧬 Autonomous Final Declaration
╔══════════════════════════════════════════════════════════════════╗
║ ELITE PROTOCOL STANDARD
║ pSunDAIvaultV2 — Immutable Stable Vault
║ Devs: Elite Team6
║ License: MIT | No Admin Keys | Autonomous | Final Form
║
║ - No Owner
║ - No Upgrade Proxy
║ - No Governance Variables
║ - Fully Deterministic Logic
║
║ "Autonomy is the highest form of trust."
╚══════════════════════════════════════════════════════════════════╝

🪙 Token Ecosystem
Component	Contract	Description
Collateral Asset	WPLS	Base-layer collateral
Stable Asset	pSunDAI	Autonomous Stable Asset
Oracle #1	pSunDaioracle	Dual DAI TWAP
Oracle #2	pSunDAITriOracleEliteV2	Triple (DAI + USDC) TWAP
Vault	pSunDAIvaultV2	Mint/redeem + safety enforcement
Developer	Elite Team6	Architect of the ASA protocol

🔗 Links
🌐 Website

📘 Docs

💬 Community

🧑‍💻 License: MIT

🕊️ Elite Team6 — Building Autonomous DeFi Primitives for PulseChain and Beyond
yaml
Copy code

---

✅ **Summary of changes made in this final merged version:**
- Added your original **Elite Protocol / Final Form** tone.  
- Integrated the **new oracle mechanics** (Tri + Dual) from your latest code.  
- Fixed outdated names (`TriOracleEliteV2`, not `Elite`).  
- Added clear technical structure for devs + auditors.  
- Updated safety constants and clamp logic explanations.  
- Retained your **philosophical declaration** section — unchanged.  
- Expanded token ecosystem section to match new architecture.
