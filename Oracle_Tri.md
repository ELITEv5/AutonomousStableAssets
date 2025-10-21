# pSunDAITriOracleEliteV2_PulseX_Final

**Immutable Triple-Pair TWAP Oracle for PulseChain Autonomous Stable Assets**

---

## Overview

The `pSunDAITriOracleEliteV2_PulseX_Final` contract aggregates price data from three PulseX trading pairs:

- WPLS / DAI (V1)
- WPLS / DAI (V2)
- WPLS / USDC

It computes a median time-weighted average price (TWAP), normalized to 18 decimals, to provide a secure, manipulation-resistant on-chain USD price feed.

This oracle is immutable once deployed and linked to a vault. It is designed for the `pSunDAIvaultV2` but can be used publicly as a decentralized price reference.

---

## Features

- **Immutable and Autonomous** — No owner, no upgradability, no admin functions  
- **Triple-Source Aggregation** — Combines three pairs using median and deviation filtering  
- **TWAP-Based Pricing** — 30-minute minimum interval with a 2-minute freshness limit  
- **Multi-Stable Support** — Supports both 18-decimal (DAI) and 6-decimal (USDC) pairs  
- **Liquidity Safeguard** — Ignores pairs with less than $50,000 equivalent stable liquidity  
- **Permissionless Updates** — Anyone can call `updatePublic()` or `prime()`  
- **Vault Integration** — The linked vault has exclusive access to `getPriceWithTimestamp()`  

---

## Function Summary

| Function | Access | Description |
|-----------|---------|-------------|
| `setVault(address)` | Deployer only (once) | Permanently links the vault |
| `prime()` | Public | Initializes the TWAP before vault operation |
| `updatePublic()` | Public | Recalculates the TWAP; can be called by anyone |
| `getPriceWithTimestamp()` | onlyVault | Primary price fetch function for the vault |
| `peekPrice()` | Public (view) | Returns the last cached price and timestamp |
| `isHealthy()` | Public (view) | Confirms that underlying pairs are updating regularly |

---

## Access Control

| Role | Permission |
|------|-------------|
| **Deployer** | May call `setVault()` once |
| **Vault** | May call `getPriceWithTimestamp()` |
| **Public** | May call all other functions freely |

After the vault is set, the oracle becomes fully immutable and permissionless.

---

## Deployment Parameters

| Parameter | Description |
|------------|-------------|
| `_pairV1` | Address of WPLS/DAI V1 pair |
| `_pairV2` | Address of WPLS/DAI V2 pair |
| `_pairUSDC` | Address of WPLS/USDC pair |
| `_wpls` | Wrapped Pulse token address |
| `_dai` | DAI token address |
| `_usdc` | USDC token address |

---

## Operation

1. Each pair’s cumulative price is fetched from UniswapV2-style pairs.  
2. Time-weighted averages are computed using cumulative deltas and elapsed time.  
3. Each TWAP is validated for:
   - Minimum reserve liquidity (`> $50,000`)
   - Freshness under 2 minutes
   - 30-minute minimum interval  
4. Valid prices are combined:
   - One valid → used directly  
   - Two valid → averaged (within 3% deviation)
   - Three valid → median used (outlier removed)  
5. Final price normalized to `1e18` for consistent scaling.

---

## Public Usage

The oracle is open to public integrations. Example:

```solidity
(uint256 price, uint256 ts) = oracle.peekPrice();
require(block.timestamp - ts < 300, "Stale oracle");
Public users can also update the oracle:

solidity
Copy code
oracle.updatePublic();
Or prime it manually:

solidity
Copy code
oracle.prime();
Health Monitoring
solidity
Copy code
bool ok = oracle.isHealthy();
require(ok, "Oracle is stale");
Ensures at least one pair has updated within the last 15 minutes.

Constants
Constant	Value	Description
PRECISION	1e18	Scaling factor
MIN_RESERVE_USD	50,000 × 1e18	Minimum stable-side liquidity
MAX_DEVIATION_BPS	300	Maximum deviation between pair prices (3%)
MAX_PRICE_AGE	120 sec	Maximum allowed staleness
MIN_TWAP_INTERVAL	1800 sec	Minimum 30-minute interval between updates

Integration Notes
Designed for PulseChain / PulseX (UniswapV2) infrastructure.

Compatible with any Autonomous Stable Asset vault.

May be used by third-party protocols as a public price oracle.

Supports automated keepers for periodic updates via updatePublic().

Author
Elite Team6

Website: https://sundaitoken.com

Documentation: https://github.com/ELITEv5/AutonomousStableAssets

License: MIT

Chain: PulseChain

Version: pSunDAITriOracleEliteV2_PulseX_Final

Disclaimer
This contract is immutable and operates fully autonomously once deployed and linked.
Ensure sufficient trading activity and liquidity before relying on its output in production systems.
