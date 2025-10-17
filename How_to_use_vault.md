# ☀️ How to Use the pSunDAI Vault on PulseChain  
*The complete guide to minting and managing your own autonomous stable asset.*

---

## 🧠 Overview

The **pSunDAI Vault** lets you lock PLS as collateral and mint **pSunDAI**,  
a decentralized, immutable stable asset on PulseChain — no admin keys, no upgrades, no middlemen.

You interact directly with the smart contract through the official explorer:
👉 [https://scan.pulsechain.com](https://scan.pulsechain.com)

---

### 🔹 Key Contract Addresses

| Component | Address | Description |
|------------|----------|-------------|
| **PegVault** | `0x52d27c5F3c0a5A733E7f2d5c21Da96b283EF7086` | Main pSunDAI Vault |
| **Oracle** | (auto-used by vault) | Price feed via WPLS/DAI pairs |
| **pSunDAI Token** | (add to wallet manually) | Stable asset you mint |

---

## 🧩 Step-by-Step Guide

### **Step 1. Open the Contract**
1. Go to [https://scan.pulsechain.com](https://scan.pulsechain.com)  
2. Paste the PegVault address:  
0x52d27c5F3c0a5A733E7f2d5c21Da96b283EF7086


3. Click **Contract** → then **Connect Wallet** (MetaMask, Rabby, etc.)

---

### **Step 2. Deposit PLS Collateral**
You must first lock PLS into the Vault.

1. Under **Write Contract**, find `depositPLS()`.  
2. Enter the amount in **wei** (18 decimals).  (Don't be a PAXOS)
- Example:  
  `10,000 PLS = 10000000000000000000000`
3. Click **Write**, confirm in your wallet.  
4. Wait for the transaction to confirm.

Your Vault is now created and holds your PLS.

---

### **Step 3. Wake Up the Oracle (Important for First-Time Users)**
If the network has been quiet or it’s your first deposit,  
the Oracle may not have a fresh price yet.

Follow these steps to safely “wake” it:

1. In **Write Contract**, find `mint()`.  
2. Enter a **tiny test value**, e.g.  
1000000000000


(≈ 0.000001 pSunDAI)
3. Click **Write** and confirm.
4. Once confirmed, immediately call `repay(1000000000000)` to burn that tiny amount.

✅ This updates the Oracle and ensures your price data is current.  
(You’ll only need to do this once per session or after long idle periods.)

---

### **Step 4. Check How Much You Can Mint**
Now that your Oracle is awake and your vault is funded:

1. Click **Read Contract**.  
2. Find `maxMintable(address)` and paste your wallet address.  
3. Click **Read**.  

You’ll see a large number in **wei** — that’s your **maximum mintable amount**  
based on your collateral and the live PLS/USD price.

> 💡 Tip: To stay safe, plan to mint about **95%** of that number.

---

### **Step 5. Mint pSunDAI**
1. Go back to **Write Contract**.  
2. Select the `mint()` function.  
3. Paste your safe mint amount (from `maxMintable * 0.95`).  
4. Click **Write** and confirm the transaction.

✅ You’ve now minted your own pSunDAI — fully backed by your PLS collateral.

> Add the pSunDAI token to your wallet to see it appear.

---

### **Step 6. Check Your Vault Health**
At any time, use `getVaultInfo(address)` under **Read Contract**.

It shows:
- **collateral:** total PLS locked  
- **debt:** pSunDAI minted  
- **ratio:** collateral ratio (target ≥ 150%)  
- **isSafe:** true = healthy, false = unsafe  
- **liquidationPrice:** price of PLS that would trigger liquidation  

Keep your ratio above **150%** to avoid liquidation.

---

## 💰 Managing Your Vault

### **Repay Debt**
To repay pSunDAI and unlock PLS:

1. Make sure you have pSunDAI in your wallet.  
2. In **Write Contract**, click `repay()`.  
3. Enter the amount you want to burn (in wei).  
4. Click **Write** and confirm.

This lowers your debt and improves your safety ratio.

---

### **Withdraw Collateral**
Once your debt is reduced (or zero), you can withdraw some or all PLS.

1. In **Write Contract**, click `withdrawPLS()`.  
2. Enter the amount (in wei).  
3. Wait for any cooldowns to expire (≈3 hours).  
4. Click **Write** and confirm.

> ⚠️ The vault will automatically revert any withdrawal  
> that makes your ratio fall below 150%.

---

### **Combined Actions**
The vault includes combo calls for convenience:

| Function | Description |
|-----------|-------------|
| `depositAndMint(uint256 mintAmount)` | Deposit PLS and mint in one transaction |
| `repayAndWithdraw(uint256 repayAmount, uint256 withdrawAmount)` | Burn pSunDAI and reclaim PLS together |

---

## ⚔️ Liquidations (Advanced)

If a user’s collateral ratio falls below **150%**, their vault becomes *unsafe*.  
Anyone can liquidate it to keep the system stable.

liquidate(address vaultOwner, uint256 repayAmount)



- You repay part of their debt in pSunDAI.  
- You receive a proportional amount of their PLS + a small liquidation reward.  

Liquidations also trigger an Oracle refresh automatically.

---

## 🧮 Oracle & Safety

- The Oracle uses two large WPLS/DAI pairs for price data.  
- Updates occur automatically during mint, repay, or liquidation calls.  
- Health check:  
isOracleHealthy()


returns **true** if data < 5 minutes old.

If prices are stale, vault functions that depend on them will **revert safely** until the next valid update.

---

## 🧾 Summary of Core Functions

| Purpose | Function | Type | Notes |
|----------|-----------|------|-------|
| Deposit PLS | `depositPLS()` | Write | Locks PLS collateral |
| Check max mint | `maxMintable(address)` | Read | Safe mint capacity |
| Mint stablecoin | `mint(uint256)` | Write | Issues pSunDAI |
| Repay | `repay(uint256)` | Write | Burns pSunDAI debt |
| Withdraw | `withdrawPLS(uint256)` | Write | Unlocks PLS |
| Vault info | `getVaultInfo(address)` | Read | Shows ratio, liq price |
| Oracle status | `isOracleHealthy()` | Read | Confirms TWAP freshness |
| Liquidate unsafe vault | `liquidate(address, amount)` | Write | Optional for experts |

---

## ⚙️ Tips for Success

- Keep your ratio above **150%** for safety.  
- If `maxMintable()` returns `0`, the Oracle may be stale — run the **wake-up sequence** (tiny mint + repay).  
- Wait **30+ minutes** between Oracle refreshes for new TWAP data.  
- Always leave a **5–10% buffer** below your max mint value.  

---

## 🎉 Congratulations!

You’ve successfully interacted with the immutable pSunDAI Vault directly on-chain.  
You now control your own decentralized stablecoin — backed by your PLS, governed by math, not people.

> **Immutable. Autonomous. Free.**  
> That’s the pSunDAI way.
