# Case Study: When Code Outperforms Custodians  
### The 300-Trillion Mint Incident vs. Autonomous Stability

---

## 🧩 The Event

In October 2025, a well-known regulated stablecoin accidentally minted **300 trillion tokens**—roughly one million times its intended supply.  
The cause was a simple but costly **decimal mismatch**: the token used 6 decimals, while the issuer’s minting script assumed 18.  
Within minutes, the token’s circulating supply spiked by twelve orders of magnitude before the operator noticed and manually burned the excess 20 minutes later.

This was not a hack or exploit; it was a **human input error** inside a centralized, upgradeable contract controlled by a trusted entity.

---

## ⚙️ The Structural Flaw

Centralized stablecoins depend on:
- off-chain custodians,  
- admin keys with mint/burn authority, and  
- operational scripts that must handle decimal precision, accounting, and limits correctly.

When humans sit in the loop, they can make mistakes—even inside billion-dollar institutions.  
The architecture allows them to do so.

---

## ☀️ The Autonomous Alternative — pSunDAI

**pSunDAI**, built as an **Autonomous Stable Asset (ASA)**, eliminates that human layer entirely.

* **Minting is algorithmic:**  
  Only the vault contract can mint, and only against verifiable PLS collateral at the required collateral ratio.

* **Decimals are fixed and baked into code:**  
  No external scripts or admin functions exist that can over-mint.

* **Immutable logic:**  
  The contracts are deployed once, with no upgrade keys or privileged roles.

The result is a system that *cannot* mis-mint—even by accident.  
There is no “operator console” to type the wrong number into.

---

## 🧠 The Lesson

> Centralized systems rely on *trust and procedure*.  
> Autonomous systems rely on *math and code*.

The former can be audited, supervised, and still fail due to human error.  
The latter simply executes deterministic logic and halts if inputs are invalid.

---

## ⚖️ Summary

| Aspect | Centralized Stablecoin | pSunDAI (ASA) |
|---------|-----------------------|----------------|
| Mint Authority | Human operators | Vault contract only |
| Error Type | Human decimal / script error | Impossible — hard-coded logic |
| Recovery | Manual burn | Automatic prevention |
| Control | Upgradeable / pausable | Immutable |
| Trust Model | “Trust but monitor” | “Don’t trust—verify on-chain” |

---

### 🧭 Takeaway

A billion-dollar company can still mint 300 trillion by mistake.  
An **Autonomous Stable Asset** can’t—because it doesn’t have the ability to make mistakes in the first place.

> Stability isn’t about who runs the system.  
> It’s about whether the system needs to be run at all.
