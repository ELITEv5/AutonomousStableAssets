# 🌞 pSunDAIVaultASA_Autonomous_Stable_Asset 
### Immutable Autonomous Stable Asset (ASA) Vault — PulseChain Edition  
**Version:** 1.0 Final  
**Developer:** [Elite Team 6](https://x.com/elite_team6)  
**Docs:** [https://github.com/ELITEv5/AutonomousStableAssets](https://github.com/ELITEv5/AutonomousStableAssets)  
**License:** MIT | Immutable | Autonomous  

---

## 🧠 Overview  

The **pSunDAIVaultASA_Autonomous_Stable_Asset** contract represents the **final evolution** of the pSunDAI ecosystem — a completely immutable, self-governing stablecoin vault that operates without any admins, governance, or maintenance.  

It integrates a **self-refreshing oracle**, **time-based stability fees**, **system-wide collateral checks**, and **autonomous UX flows** for seamless, one-click interaction.

> 💬 *“The code is the keeper.”*

---

## 🧩 Architecture Summary

| Layer | Contract | Role | Immutable |
|--------|-----------|------|-----------|
| Base Token | `pSunDAIV8` | ERC-20 stable asset, mint/burn controlled by vault | ✅ Yes |
| Vault | `pSunDAIVault_ASA_Autonomous_Stable_Asset` | Collateral, debt, minting, liquidation | ✅ Yes |
| Oracle | `pSunDAIoraclePLSX` | Median-filtered, tri-pair TWAP hybrid | ✅ Yes |
| Interface | `IWPLS` | WPLS wrapper for native PulseChain PLS | ✅ Standard |

---

## 🔧 Key Features Added in Final Version  

| Category | New Capability | Description |
|-----------|----------------|--------------|
| 🧭 **Oracle Autonomy** | Self-refreshing, median TWAP | Oracle refreshes automatically via user actions — no keepers, no updates needed. |
| 🧮 **Stability Fee System** | Time-based 0.5% annualized | Minimal annual stability fee accrues mathematically per vault. |
| 🛡️ **System-Wide Health Check** | 130% minimum global ratio | Blocks minting if total system collateral drops below 130%. |
| ⚙️ **Oracle Staleness Protection** | 24-hour cutoff | Prevents minting or liquidation if oracle data is stale. |
| 💸 **One-Click UX** | `depositAndAutoMintPLS()` / `repayAndAutoWithdraw()` | Enables intuitive, one-transaction flows for front-end users. |
| 🧰 **Dust Forgiveness** | Auto-clears residual debt | Any remaining dust <1e12 wei is forgiven to avoid rounding errors. |
| 🔥 **Dynamic Liquidation Rewards** | 2%–5% time-based | Liquidation rewards increase over time since last vault activity. |
| 🔓 **Emergency Unlocks** | 30-day inactivity unlock | Fully repaid vaults can withdraw collateral after 30 days even if oracle fails. |
| 🧾 **System Transparency** | `vaultInfo()` and `systemStatus()` | Single-call data for frontend dashboards and explorers. |

---

## 🧮 Mathematical Integrity  

### Stability Fee  
```solidity
fee = (debt * 0.5% * elapsed_seconds) / seconds_per_year;
Applies only if a vault has outstanding debt.

Accrues smoothly based on elapsed time.

Keeps long-term vaults in balance with system risk.

Collateralization Ratios
Minimum Mint: 150%

Liquidation Trigger: 110%

Global System Minimum: 130%

⚖️ Vault Lifecycle
Action	Function	Description
Deposit PLS	depositPLS()	Wraps and stores PLS as WPLS collateral.
Deposit WPLS	deposit()	Adds WPLS collateral directly.
One-Click Mint	depositAndAutoMintPLS()	Deposits and mints at safe 155% ratio.
Mint Manually	mint(amount)	Mints exact pSunDAI amount (subject to ratio).
Repay	repay(amount)	Burns pSunDAI and reduces vault debt.
One-Click Repay + Withdraw	repayAndAutoWithdraw()	Repays debt and returns collateral in one step.
Withdraw	withdrawPLS() / withdrawWPLS()	Redeems collateral while maintaining ratio.
Liquidate	liquidate(victim, repayAmount)	Repays unsafe vaults and receives bonus reward.
Emergency Unlock	emergencyUnlock()	Fully repaid vaults can self-withdraw after 30 days.

🧭 Oracle — pSunDAIoraclePLSX_AutonomousUXFinal
Data Sources
V1 Pair: 0xE56043671df55dE5CDf8459710433C10324DE0aE

V2 Pair: 0x146E1f1e060e5b5016Db0D118D2C5a11A240ae32

USDC Pair: PulseChain USDC liquidity pool

Key Mechanics
Median-filtered across all pairs for anti-manipulation.

TWAP + Spot hybrid ensures both responsiveness and safety.

Refreshes automatically when user interactions occur.

Enforces ±10% change clamp per update to prevent flash deviations.

Never returns 0 or stale data — always uses lastSafePrice.

🧠 System Self-Protection
Risk	Mitigation
Oracle failure	Auto-freeze minting/liquidation; still allows repayments & withdrawals
Rapid price crash	Collateral ratio enforced per vault + global system check
Vault neglect	Stability fee accrual + auto-repay to health
Network inactivity	No keepers required; resumes from lastSafePrice
Oracle death	Emergency unlock allows user recovery after 30 days

💎 Economic Summary
Parameter	Value	Purpose
Collateral Ratio	150%	Vault safety threshold
Liquidation Ratio	110%	Liquidation trigger
Liquidation Bonus	2–5%	Dynamic liquidator reward
Stability Fee	0.5% annually	Time-based debt cost
System Health	≥130%	Global solvency check
Withdraw Cooldown	300 seconds	Anti-flash-withdraw rule
Oracle Refresh	60 seconds	TWAP self-update interval

⚙️ Frontend-Ready Methods
Function	Purpose
vaultInfo(address)	Returns full vault + system data
systemStatus(address)	Returns oracle, ratio, mintable data
maxMint(address)	Shows maximum mintable pSunDAI
repayToHealth(address)	Shows repay amount needed to restore safety
liquidationInfo(address)	Returns liquidatable user data + rewards

🔐 Fail-Safe Behavior
If oracle halts → system enters safe-mode (no new minting or liquidations).

If all oracles vanish → vaults retain PLS, users can reclaim via emergency unlock.

If total system debt hits 0 → vaults become dormant, collateral untouched.

💬 “When humans disappear, it still works.”

🧠 Design Philosophy
The pSunDAIVaultASA_AutonomousUXFullFinal isn’t a DeFi product —
it’s a mathematical institution.

It defines the rules of solvency, balance, and redemption without requiring any trust in people, servers, or multisigs.

“This isn’t governance — it’s physics.”

📜 Attribution
© 2025 Elite Team 6
SunDAI™, pSunDAI™, and Destiny Vault™ are independent decentralized protocols.
Not affiliated with MakerDAO, Aave, or any other stablecoin issuer.

License: MIT | Autonomous | Immutable
Website: https://www.sundaitoken.com
Docs: https://github.com/ELITEv5/AutonomousStableAssets
