# ☀️ How to Use the pSunDAI Vault on PulseChain

This guide explains how to interact directly with the **pSunDAI PegVault** using the [PulseChain block explorer](https://scan.pulsechain.com).  
You’ll learn how to:
- Deposit PLS as collateral  
- Wake up (refresh) the Oracle  
- Check how much you can safely mint  
- Mint your own pSunDAI stablecoins  
- Repay and withdraw collateral  
- Understand liquidation safety  

---

## 🧠 Overview

**Vault Contract Address:**
0x52d27c5F3c0a5A733E7f2d5c21Da96b283EF7086


**Oracle Contract:** automatically used by the Vault  
**Stablecoin Token:** pSunDAI (`pSUNDAI`)

Each vault is *isolated* — your position is yours alone.  
There are no admin keys, no upgrades, and no pooled debt.

---

## 🪙 Step-by-Step Guide

### **Step 1. Open the PulseChain Scanner**
Go to 👉 [https://scan.pulsechain.com](https://scan.pulsechain.com)

---

### **Step 2. Load the PegVault Contract**
Paste this address into the search bar:

0x52d27c5F3c0a5A733E7f2d5c21Da96b283EF7086


Press **Enter** → Click **“Contract”** → then **“Connect Wallet.”**

---

### **Step 3. Wake Up the Oracle (Optional but Recommended)**
If the network has been quiet, the Oracle might be stale.  
Refreshing it ensures your `maxMintable` calculation is accurate.

**To refresh the Oracle:**
1. In **Write Contract**, find `mint`.
2. Enter a tiny amount such as `1000000000000` (that’s 0.000001 pSunDAI).
3. Click **“Write”** → confirm → wait for it to complete.
4. Then immediately call `repay(1000000000000)` to clear the tiny mint.

✅ This triggers the Oracle update without changing your position.

---

### **Step 4. Deposit PLS Collateral**
1. In **Write Contract**, select `depositPLS`.  
2. Enter your deposit amount in **wei (18 decimals)**.  
   - Example: `10,000 PLS = 10000000000000000000000`
3. Click **“Write”** and confirm in your wallet.

Once confirmed, your PLS is locked as collateral in your vault.

---

### **Step 5. Check Your Max Mintable Amount**
1. Switch to **Read Contract**.
2. Find `maxMintable(address)`.
3. Paste your wallet address.
4. Click **“Read.”**

You’ll get a large integer result — this is the maximum pSunDAI you can mint, in wei.

---

### **Step 6. Mint pSunDAI**
1. Go back to **Write Contract**.  
2. Find the `mint` function.  
3. Paste the value you copied from `maxMintable` (or use slightly less for safety, e.g., 95% of it).  
4. Click **“Write”** and confirm in your wallet.

When the transaction confirms, your **pSunDAI** balance will appear in your wallet.

> 💡 **Tip:** Import the pSunDAI token address manually if you don’t see it right away.

---

## 💰 Managing Your Vault

### **Check Vault Health**
In **Read Contract**, use:
- `getVaultInfo(address)` → shows your collateral, debt, ratio, and liquidation price.  
- If your ratio drops below **150%**, your vault becomes unsafe and can be liquidated.  

---

### **Repay Debt**
When you want to reduce or close your position:

1. Make sure you hold enough pSunDAI in your wallet.  
2. In **Write Contract**, select `repay`.  
3. Enter the amount (in wei).  
4. Click **“Write.”**

This burns pSunDAI and lowers your vault’s debt.  
If your ratio is now safe, the vault automatically resets its “unsafe time.”

---

### **Withdraw Collateral**
After repaying (or if you’re over-collateralized):

1. In **Write Contract**, select `withdrawPLS`.  
2. Enter the amount of PLS (in wei).  
3. Confirm you’re outside the withdrawal cooldown (≈3 hours).  
4. Click **“Write.”**

Your PLS will be unwrapped from WPLS and sent back to your wallet.

> ⚠️ If your withdrawal would drop your ratio below 150%,  
> the transaction will revert for safety.

---

### **Combined Actions**
The Vault supports combo calls:

| Function | Description |
|-----------|--------------|
| `depositAndMint(uint256 mintAmount)` | Deposit PLS and mint in one transaction |
| `repayAndWithdraw(uint256 repayAmount, uint256 withdrawAmount)` | Repay debt and withdraw collateral in one go |

---

## ⚔️ Liquidations (for Experts)

If a vault falls below **150% collateral ratio**, anyone can liquidate it using:

liquidate(address vaultOwner, uint256 repayAmount)


- The liquidator burns pSunDAI to repay that debt.
- In return, they receive a proportional amount of PLS plus a liquidation reward.  
- The protocol uses the Oracle price at that moment to calculate fairness.

---

## 🧮 Oracle Health Check

- The Oracle averages prices from two WPLS/DAI pairs.  
- Updates occur automatically during mint, repay, or liquidation calls.  
- You can check freshness using:

isOracleHealthy()


If it returns **true**, the Oracle data is <5 minutes old.

---

## ✅ Summary of Functions

| Action | Function | Type | Notes |
|--------|-----------|------|-------|
| Deposit PLS | `depositPLS()` | Write | Locks collateral |
| Check max mint | `maxMintable(address)` | Read | Returns safe mint limit |
| Mint pSunDAI | `mint(amount)` | Write | Issues pSunDAI |
| Repay debt | `repay(amount)` | Write | Burns pSunDAI |
| Withdraw PLS | `withdrawPLS(amount)` | Write | Unlocks collateral |
| Check vault info | `getVaultInfo(address)` | Read | Shows ratio and liquidation price |
| Liquidate unsafe vault | `liquidate(address, amount)` | Write | Burns pSunDAI for collateral |
| Oracle status | `isOracleHealthy()` | Read | Confirms TWAP freshness |

---

## 🧭 Safety Notes

- Keep your **collateral ratio >150%** at all times.  
- The system liquidates under-collateralized vaults automatically for stability.  
- Wait at least **30 minutes** between Oracle refreshes for new TWAP data.  
- If the Oracle fails or is stale >5 minutes, mint/repay will revert until refreshed.  

---

## 🎉 You Did It!

You now understand how to use the pSunDAI PegVault directly from the blockchain explorer —  
no UI, no admin keys, just smart contracts.

> **Immutable • Permissionless • Autonomous**  
> The way DeFi was meant to be.
