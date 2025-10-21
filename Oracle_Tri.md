🟣 pSunDAITriOracleEliteV2_PulseX_Final
Triple TWAP Median Oracle for PulseChain Autonomous Stable Assets

A permissionless, immutable, multi-stable Uniswap V2 oracle designed for the Autonomous Stable Asset vault system (pSunDAIvaultV2).

🧩 Overview

pSunDAITriOracleEliteV2_PulseX_Final aggregates live trading data from three key PulseX pairs:

WPLS / DAI (V1)

WPLS / DAI (V2)

WPLS / USDC

It computes a normalized median TWAP (Time-Weighted Average Price), providing a manipulation-resistant, on-chain USD price feed for WPLS.

The oracle is immutable once deployed and vault-linked — a fully decentralized pricing primitive with no admin controls.

⚙️ Key Features

🔒 Immutable Architecture — No upgradeability, no ownership, no admin keys

⚖️ Triple Source Aggregation — Median + deviation filters eliminate outliers

🕒 TWAP-Driven Stability — 30-minute minimum interval, 2-minute freshness window

🪙 Multi-Decimal Normalization — Handles both 18-decimal (DAI) and 6-decimal (USDC) assets

🔁 Public Refresh Access — Anyone can update via updatePublic()

📡 Instant Read Access — peekPrice() available to all users and UIs

🧱 Liquidity Safeguards — Ignores pairs under $50k equivalent in liquidity

🧠 Function Summary
Function	Type	Access	Description
setVault(address)	One-time admin	Only deployer	Permanently links the vault (immutable after)
prime()	Public	Any user	Initializes TWAP values before vault use
updatePublic()	Public	Any user	Forces a TWAP recalculation (permissionless)
getPriceWithTimestamp()	Vault	onlyVault	Official oracle call used by pSunDAIvaultV2
peekPrice()	View	Any user	Returns last cached price and timestamp (no gas)
isHealthy()	View	Any user	Checks if pairs are active and recently updated
🔐 Access Control

Deployer:
Can call setVault() once to link the vault — this action is irreversible.

Vault:
Has exclusive access to getPriceWithTimestamp() — used to obtain live TWAP values.

Everyone Else:
May call updatePublic(), prime(), peekPrice(), and isHealthy() freely.

After the vault link:

The oracle becomes 100% permissionless and immutable.
No admin can modify, pause, or override price logic.

🧾 Deployment Parameters
Parameter	Type	Description
_pairV1	address	PulseX V1 WPLS/DAI pair
_pairV2	address	PulseX V2 WPLS/DAI pair
_pairUSDC	address	PulseX V2 WPLS/USDC pair
_wpls	address	Wrapped Pulse token
_dai	address	DAI token
_usdc	address	USDC token
💡 How It Works

Each pair’s cumulative prices are fetched from Uniswap V2’s price0CumulativeLast() or price1CumulativeLast() fields.

The difference in cumulative prices over the last interval is divided by the time elapsed → TWAP.

Each TWAP is validated for:

Liquidity above $50,000

Freshness under 2 minutes

Minimum interval of 30 minutes

The valid price feeds (1–3) are combined:

1 valid: returned directly

2 valid: averaged (within 3% deviation)

3 valid: median filter (outlier removed)

Final price is normalized to 1e18 scale for universal compatibility.

🧰 Example Usage
(uint256 price, uint256 timestamp) = oracle.peekPrice();
if (block.timestamp - timestamp < 300) {
    // Safe to use the oracle price
}


To refresh the oracle manually:

oracle.updatePublic();


Or pre-prime it before vault activation:

oracle.prime();

📊 Health Check

Use isHealthy() to confirm pairs are still updating:

bool healthy = oracle.isHealthy();
require(healthy, "Oracle is stale");


This function ensures at least one pair updated within the last 15 minutes.

🪙 Price Scaling Example
Pair	Stable	Decimals	Normalized
WPLS/DAI	DAI	18	1e18
WPLS/USDC	USDC	6	scaled × 1e12 to 1e18
⚙️ Constants Summary
Constant	Value	Description
PRECISION	1e18	Global scaling factor
MIN_RESERVE_USD	50,000e18	Minimum stable-side liquidity
MAX_DEVIATION_BPS	300	3% max allowed difference between sources
MAX_PRICE_AGE	120 sec	Maximum time before price is stale
MIN_TWAP_INTERVAL	1800 sec	Minimum 30-minute rolling TWAP
🧱 Integration Notes

Designed for PulseChain / PulseX Uniswap V2 forks.

Works seamlessly with pSunDAIvaultV2 and any future Autonomous Stable Assets.

Can be adopted by other protocols as a universal WPLS → USD price feed.

Supports keeper bots for updatePublic() every 15–30 minutes.

🧑‍💻 Author & Credits

Elite Team6

🌐 Website: https://sundaitoken.com

📘 Docs: https://github.com/ELITEv5/AutonomousStableAssets

🧠 Architect: Autonomous Stable Asset System, PulseChain Edition

⚠️ Disclaimer

This contract is provided as-is without warranties.
All parameters are immutable — once deployed and vault-linked, the oracle operates fully autonomously.
Ensure that trading liquidity and pair freshness are monitored before linking to production vaults.
