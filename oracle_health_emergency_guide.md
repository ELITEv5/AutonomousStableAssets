# 🛰️ Oracle Health & Emergency Guide

This guide explains how the **pSunDAI Oracle** works,  
how to verify its health, and what to do if it stalls or market liquidity drops.

---

## 🧠 Overview

The **pSunDAI Oracle** powers all vault functions — deposit, mint, repay, and liquidation.  
It determines the price of **PLS in USD**, using two independent on-chain liquidity sources.

### ✅ Design Goals
- 100% **on-chain** (no Chainlink or off-chain feeds)
- Dual-source redundancy (Uniswap V1 + V2)
- Built-in **time-weighted average price (TWAP)**
- **Freshness guard** (max 5 minutes old)
- Immutable — no updates, no admins, no replacements

---

## ⚙️ How the Oracle Works

### 🧩 Structure

| Variable | Description |
|-----------|--------------|
| `pairV1` | Primary WPLS/DAI liquidity pair |
| `pairV2` | Secondary WPLS/DAI liquidity pair |
| `lastPrice` | Latest recorded TWAP price |
| `MAX_PRICE_AGE` | 300 seconds (5 minutes) freshness limit |
| `AUCTION_TIME` | 86,400 seconds (24 hours) — used in liquidation reward calc |

When the vault needs a price, it calls:

```solidity
_getPricePLSUSD()
That in turn requests a fresh update from the oracle’s getPriceWithTimestamp() function.

🔁 Oracle “Wake-Up” Events
The oracle updates automatically during these on-chain actions:

mint() – when a user mints new pSunDAI

repay() – when a user repays debt

liquidate() – when liquidation occurs

depositAndMint() – during combined deposit/mint

Each of these calls triggers the oracle to recalculate the TWAP price
and update the internal timestamp.

⚙️ Oracle Health Check
You can manually verify oracle freshness anytime via PulseChain Scan:

Visit https://scan.pulsechain.com

Paste the Oracle Contract Address


0x<your_oracle_address_here>
Go to Read Contract

Click peekPrice()

You’ll see two values:


price (uint256):  30425980603125
timestamp (uint256): 1760658475
If the timestamp is within 300 seconds of the current block time,
the oracle is healthy.

🧭 Oracle Not Updating? (Common Cause)
If you’re testing minting or checking maxMintable() and it returns 0,
it usually means the oracle needs a fresh update.

🧰 Fix:
Deposit first:


depositPLS()
Mint a small “dust” amount to trigger an update:


mint(1000000000000) // 0.000001 pSunDAI
Wait for the transaction to confirm.

Now re-check:


maxMintable(yourAddress)
✅ The value will now show the correct maximum mintable amount.

⚠️ Low Liquidity or Pair Failure
The oracle reads from two pairs:

Pair	Example	Weight
V1	0xE560...DE0aE	Primary
V2	0x146E...0ae32	Secondary

If one pair becomes illiquid:

The oracle automatically falls back to the other pair.

If both fail, it uses the last known valid lastPrice.

In this fallback state:
Minting and liquidation still function,
but may revert if the price is older than 5 minutes.

Repay and Withdraw will still succeed.

🚨 Emergency Scenarios
1. Both Oracle Pairs Go Offline
If both pairs lose liquidity:

The oracle will refuse to return a new price (stale >300s).

Mint and liquidation will temporarily pause (revert on stale price).

No collateral is lost — funds remain safely locked.

🛡️ Once new liquidity forms on either pair, a single mint or repay will automatically refresh the system.

2. Oracle Timestamp Too Far Ahead (Future Bug)
Occasionally (on testnets or forked time chains), timestamps may appear years ahead.
This is harmless as long as the time difference between updates is realistic.
Vault safety logic only cares about the difference between block times, not the calendar year.

✅ No user action required.

3. Oracle Stuck & Vault Frozen
If somehow both pairs are broken permanently:

A new vault + oracle pair can be deployed in parallel.

The old vault’s collateral can be withdrawn by repaying all pSunDAI,
even with stale price fallback, if authorized in future migration tools.

🧩 Failsafe: lastPrice Fallback
If both TWAP pairs are invalid, the oracle reverts to its last valid recorded price:


require(lastPrice > 0, "No historical price");
return (lastPrice, block.timestamp);
This ensures:

No blackouts in view functions.

Vault ratio calculations can still display approximate data.

🔍 Function Summary
Function	Purpose	Oracle Interaction
peekPrice()	Returns cached price + timestamp	None (read-only)
getPriceWithTimestamp()	Returns and updates live TWAP price	Full update
_getPricePLSUSD()	Internal call by Vault	Live price with freshness check
_getPriceView()	Internal view (no update)	Uses last known data

🧠 Best Practices
Scenario	Action
maxMintable() returns 0	Mint dust amount to refresh oracle
Long oracle timestamp	Ignore – check delta instead
Low liquidity on one pair	Oracle switches to backup
No updates >5 mins	Wait or trigger mint/repay
Total liquidity collapse	Oracle halts (failsafe protects funds)

🧭 Summary
Property	Status
Source	Dual TWAP (on-chain)
Freshness	≤5 minutes
Backup	Secondary pair + lastPrice fallback
Trigger Events	Mint, Repay, Liquidate, DepositAndMint
Immutability	Yes
External Dependencies	None
Safety in Failures	Fully protected

Immutable. Autonomous. Self-Healing.
The pSunDAI Oracle is not a data feed — it’s a heartbeat.
As long as PulseChain trades, your stable asset lives.
