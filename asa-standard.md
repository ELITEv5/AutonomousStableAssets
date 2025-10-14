# ASA Standard v1.0  
**Autonomous Stable Asset (ASA)**  

**Author:** +ELITE Team6  
**Status:** Updated 
**Created:** 2025-10-13  

## Summary
Defines the Autonomous Stable Asset model — a decentralized, immutable system for creating over-collateralized, market-pegged assets without custodians or governance.

## Abstract
An ASA is an on-chain contract that mints and redeems a stable-value token backed by crypto collateral.  
Stability is achieved through collateral ratio enforcement, liquidation incentives, and autonomous price oracles.  
There is no issuer; the protocol itself performs all accounting.

## Specification
- Collateral ratio ≥ 150 %  
- Liquidation ratio = 110 %  
- Max bonus = 5 % over 24 h  
- Oracle = dual-TWAP on-chain feed  
- Governance = none (immutable)  
- Redemption = repay → unlock collateral  

## Rationale
Traditional “stablecoins” depend on custodians and regulatory permission.  
An ASA replaces human discretion with deterministic math, providing a censorship-resistant unit of account native to blockchains.

## Reference Implementation
pSunDAI – first ASA deployed on PulseChain.  
https://github.com/ELITEv5/AutonomousStableAssets
