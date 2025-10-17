# ⚔️ How Liquidation Works in the pSunDAI Vault

Learn how liquidation keeps the **pSunDAI** stablecoin secure,  
how to perform one, and how to protect your own vault from being liquidated.

---

## 🧠 What Is Liquidation?

Liquidation occurs when a vault’s **collateral ratio** falls below **150%**,  
meaning its PLS collateral no longer safely covers the amount of pSunDAI minted.

When this happens, the vault becomes **unsafe**, and anyone on-chain can:

- Repay part of its pSunDAI debt.
- Receive a proportional share of its PLS collateral (plus a reward).

> 🧩 In short: you repay risky debt and earn PLS in return.

---

## ⚖️ The Safety Rule

A vault is safe if:

collateral * price * 100 >= debt * COLLATERAL_RATIO * 1e18

yaml
Copy code

If this condition fails, liquidation becomes available.

---

## 🧾 The Liquidation Function

liquidate(address vaultOwner, uint256 repayAmount)

markdown
Copy code

### Parameters:
- `vaultOwner` → Address of the unsafe vault.  
- `repayAmount` → How much pSunDAI you want to repay.

### What Happens:
- Your pSunDAI is **burned**.
- You receive **PLS** from the vault’s collateral as a reward.
- The vault’s **debt** and **collateral** are reduced.

---

## 💥 Example

| Field | Value |
|--------|--------|
| Collateral | 10,000 PLS |
| Debt | 60 pSunDAI |
| Oracle Price | $0.000008 |
| Collateral Value | $80 |
| Ratio | 133% (unsafe) |

If you call:

liquidate(0xAliceAddress, 20e18)

yaml
Copy code

You repay 20 pSunDAI of Alice’s debt and receive a reward of ~2,700 PLS,  
based on the oracle price and time-based bonus.

---

## 🧮 Reward Formula

baseCollateral = (repayAmount * 1e18) / price
bonus = (baseCollateral * MAX_BONUS_BPS * timeElapsed) / (AUCTION_TIME * 10000)
reward = baseCollateral + bonus

yaml
Copy code

### Explanation:
- **baseCollateral** → The PLS equivalent of the debt you repaid.  
- **bonus** → Grows over time (up to 5% max).  
- **reward** → What you receive in total.

---

## ⏳ Bonus Timeline

| Time Unsafe | Bonus | Total Reward |
|--------------|--------|---------------|
| 0 minutes | 0% | Base collateral |
| 30 minutes | 1% | 1.01x |
| 2 hours | 3% | 1.03x |
| 24 hours | 5% | 1.05x (cap) |

The longer a vault stays unsafe, the higher the liquidation reward (within limits).

---

## 🧩 How to Perform a Liquidation

1. Go to [https://scan.pulsechain.com](https://scan.pulsechain.com)  
2. Paste the Vault address:  
0x52d27c5F3c0a5A733E7f2d5c21Da96b283EF7086


3. Click **Contract** → **Connect Wallet**
4. Click **Write Contract**
5. Find `liquidate(address vaultOwner, uint256 repayAmount)`
6. Enter:
- Vault address of the unsafe user.
- Amount of pSunDAI to repay (≥20% of their debt).
7. Click **Write** and confirm the transaction.

You’ll automatically receive your PLS reward.

---

## 🧱 Vault After Liquidation

- Vault debt is reduced.  
- Collateral is reduced by the reward amount.  
- If still unsafe, more liquidations can occur.  
- If restored above 150%, vault returns to safe status.

---

## 🔍 Checking Unsafe Vaults

Use these read functions:

1. `getVaultInfo(address)`  
- Shows ratio and safety status.  
2. `liquidationInfo(address)`  
- Returns:  
  - `debt` → total vault debt  
  - `minRepay` → minimum repayable amount  
  - `rewardNow` → current liquidation reward  

If `isSafe = false`, the vault can be liquidated.

---

## 🧠 Avoiding Liquidation

For vault owners:

- Maintain your ratio above **150%** (ideally 170–200%).  
- Use `getVaultInfo(address)` often to check safety.  
- If unsafe:
- `repay(amount)` → burns pSunDAI to restore health.  
- `depositPLS()` → adds more collateral.

Once your vault ratio is >150%, liquidation risk is gone.

---

## ⚙️ Liquidation Parameters

| Parameter | Description | Value |
|------------|--------------|--------|
| `COLLATERAL_RATIO` | Minimum safety level | 150% |
| `LIQUIDATION_RATIO` | Liquidation trigger | 110% |
| `MAX_BONUS_BPS` | Max liquidator bonus | 5% |
| `AUCTION_TIME` | Max bonus time window | 24 hours |
| `MIN_LIQUIDATION_BPS` | Minimum liquidation portion | 20% |
| `MIN_LIQUIDATION_REWARD` | Minimum reward size | 0.001 PLS |

---

## 🛡️ Safety Mechanisms

- **Oracle freshness:** must be <5 minutes old.  
- **Cooldown:** 10-minute delay between liquidations on the same vault.  
- **TWAP safeguard:** prevents manipulation of short-term prices.

---

## 🧭 Recovery Strategy (for Owners)

If your vault is unsafe:
1. Call `repay(amount)` to burn pSunDAI.  
2. Or `depositPLS()` to add collateral.  
3. Check `getVaultInfo()` again.  
4. Once `isSafe = true`, you’re protected.

---

## 📘 Summary

| Role | Action | Benefit |
|------|---------|----------|
| Vault Owner | Keep ratio >150% | Safety from liquidation |
| Liquidator | Repay unsafe debt | Earn PLS reward |
| Protocol | Enforces overcollateralization | Maintains pSunDAI peg |

---

> **Immutable. Autonomous. Fair.**  
> Liquidation in pSunDAI isn’t punishment — it’s protection.  
> Every liquidation keeps the system solvent and the stablecoin honest.
