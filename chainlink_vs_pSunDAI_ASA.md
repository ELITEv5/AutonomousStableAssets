# 🧮 Chainlink Proof-of-Reserve vs. pSunDAI (Autonomous Stable Asset)

### Collateral
- **Chainlink PoR:** Off-chain fiat or BTC held by custodians  
- **pSunDAI:** On-chain PLS locked in immutable vault contracts  

### Verification
- **Chainlink PoR:** External attestors and oracle feeds publish collateral balances  
- **pSunDAI:** Self-verifying on-chain math—every vault action enforces collateralization  

### Trust Model
- **Chainlink:** *Trust but verify* (relies on custodians + oracle operators)  
- **pSunDAI:** *Don’t trust—just read the chain* (purely cryptographic verification)  

### Update Cycle
- **Chainlink:** Periodic oracle updates (minutes or hours)  
- **pSunDAI:** Real-time enforcement at every mint, repay, or liquidation  

### Human Control
- **Chainlink:** Operators can update feeds or custodians  
- **pSunDAI:** No admin keys, immutable code, no upgrades  

### Failure Mode
- **Chainlink:** Feed or custodian failure can hide true reserve state  
- **pSunDAI:** Oracle freeze simply halts new actions—collateral remains safe on-chain  

### Use Case
- **Chainlink:** Centralized stablecoins (USDC, PYUSD, etc.)  
- **pSunDAI:** Autonomous over-collateralized stable assets (ASA class)

---

## Explanation

**Chainlink Proof-of-Reserve (PoR)** adds *transparency* to centralized systems by auditing custodians and publishing on-chain proofs that off-chain reserves exist.

**pSunDAI**, by contrast, achieves *intrinsic transparency*—the reserves *are* the collateral, locked directly in immutable smart contracts.  
No custodian. No operator. No external proof required.

| Model | Core Principle |
|--------|----------------|
| **Chainlink PoR** | “Trust but verify.” |
| **pSunDAI / ASA** | “Don’t trust, verify on-chain.” |

---

> One model builds *auditable trust* into centralized finance.  
> The other builds *trustless stability* directly into code.
