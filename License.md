# SunDAI - Autonomous Stable Asset Protocol

**Built by:** ELITE TEAM6  
**Version:** v5.6 Immortal Edition  
**License:** MIT (No Copyright Holder)  
**Website:** https://www.sundaitoken.com  
**Contact:** dev@sundaitoken.com (security disclosures only)

---

## License

MIT License (No Copyright Holder)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---

## ⚠️ CRITICAL DISCLAIMERS

### No Issuer, Controller, or Legal Entity

**There is no company, foundation, or legal entity behind SunDAI.**

- The smart contracts are deployed immutably with no admin keys
- The creators (ELITE TEAM6) have no ongoing control, ownership, or liability
- This is open-source software released to the public domain
- The protocol operates autonomously without human intervention
- **No one can pause, upgrade, modify, or control these contracts**

---

### Financial Risk Warning

SunDAI is experimental financial software. By using this protocol, you acknowledge and accept the following risks:

#### Smart Contract Risk
- The contracts are **immutable** and cannot be upgraded or fixed
- Any bugs or vulnerabilities discovered after deployment **cannot be patched**
- The protocol **has not been audited** by third-party security firms
- You may **lose all deposited collateral**

#### Oracle Risk
- Price feeds depend on DEX liquidity and may be manipulated
- Oracle uses 4-hour confirmation on large price drops (intentional delay)
- Price updates require user interactions or manual poke() calls
- Stale oracle data could affect liquidation timing

#### Liquidation Risk
- Your collateral **will be liquidated** if vault health falls below 110%
- Interest accrues continuously and can push vaults into liquidation
- You are **solely responsible** for monitoring your position
- No warnings, no grace period, no customer service

#### Market Risk
- Cryptocurrency prices are extremely volatile
- PLS price can drop 30-50%+ in hours during crashes
- Even healthy vaults can be liquidated in extreme conditions
- Past performance does not indicate future results

#### Total Loss Risk
- You may lose **100% of deposited collateral**
- There is no insurance, no backstop, no recovery mechanism
- Once liquidated, your collateral is gone permanently

---

### Not a Payment Stablecoin

**SunDAI is NOT a reserve-backed stablecoin.**

pSunDAI is an experimental **synthetic stable asset** created through over-collateralized debt positions. Key differences from payment stablecoins (USDC, USDT):

- ❌ **No USD reserves** - Protocol holds no dollars, treasuries, or reserve assets
- ❌ **No redemption rights** - You cannot redeem pSunDAI for $1 from anyone
- ❌ **No issuer** - Users self-mint tokens by locking PLS collateral in smart contracts
- ❌ **No custody** - No entity custodies funds or controls the protocol
- ❌ **No $1 guarantee** - Peg maintained by market arbitrage, not protocol guarantee
- ❌ **No payment system** - Not designed or intended for payments or remittances

#### Legal Classification

pSunDAI is a **synthetic derivative token**, not a payment stablecoin under proposed US regulations. It operates similarly to:
- MakerDAO's DAI (algorithmic, over-collateralized)
- Liquity's LUSD (CDP-based, immutable)
- Reflexer's RAI (floating peg, no governance)

This is **software that creates synthetic assets**, not a financial service.

---

### No Warranties or Guarantees

- The protocol is provided **"AS-IS"** with **ZERO guarantees** of:
  - Uptime or availability
  - Peg stability (may depeg at any time)
  - Functionality or correctness
  - Security or safety
- ELITE TEAM6 provides **no support, no customer service, no assistance**
- **No one is responsible if this breaks, fails, or loses your money**

---

### Not Financial, Investment, Legal, or Tax Advice

- This software is for **informational and experimental purposes only**
- Nothing in this repository constitutes advice of any kind
- **Do not use this as a store of value, payment system, or investment**
- Consult qualified professionals before making financial decisions

---

### Regulatory Compliance & Restricted Jurisdictions

**This protocol is NOT available to:**
- **United States persons** (as defined under US securities regulations)
- Residents of **OFAC-sanctioned countries** (North Korea, Iran, Syria, Cuba, etc.)
- Residents of jurisdictions where DeFi protocols are **prohibited by law**

**By using this protocol, you represent and warrant that:**
- You are **not a US person**
- You are **not accessing from a restricted jurisdiction**
- You **comply with all applicable laws** in your jurisdiction
- You understand this may be **illegal where you live**

**Users are solely responsible for:**
- Determining whether use is legal in their jurisdiction
- Complying with all applicable tax, securities, and financial laws
- Obtaining any required licenses or approvals
- Consequences of violating local laws

---

### Immutability Notice

**The deployed smart contracts are IMMUTABLE:**
- Cannot be paused, upgraded, modified, or controlled by anyone
- Cannot be shut down or stopped under any circumstances
- No emergency shutdown mechanism exists
- No admin recovery function exists
- **Once deployed, the protocol runs forever without human control**

This is a **feature**, not a bug - but it means:
- No one can fix problems
- No one can recover funds
- No one can help you if something goes wrong

---

### No Affiliation or Endorsement

- SunDAI is **not affiliated with** any government, bank, or regulatory body
- **Not endorsed by** PulseChain, Ethereum, or any other blockchain
- **Not connected to** any financial institution or payment network
- References to "stable" describe **intended algorithmic behavior**, not regulatory status

---

### User Responsibility & Acknowledgment

**By interacting with this protocol, you acknowledge and agree that:**

✓ You understand how decentralized finance (DeFi) and CDP protocols work  
✓ You have read and understood all documentation  
✓ You are **solely responsible** for security of your private keys and wallet  
✓ You accept **full responsibility** for any losses incurred  
✓ You will **not hold anyone liable** for damages, losses, or theft  
✓ You understand **no one can help you** if something goes wrong  
✓ You are using this **at your own risk** with **no safety net**  
✓ **There is no customer service, no support, no recourse**

---

### Security & Bug Disclosure

#### Responsible Disclosure
If you discover a security vulnerability, please contact: **dev@sundaitoken.com**

We encourage responsible disclosure but provide **no bug bounty, no rewards, no guarantees** of response.

#### Known Limitations & Design Tradeoffs

These are **intentional features**, not bugs:

- **4-hour confirmation** on large oracle price drops (anti-manipulation)
- **Interest accrues continuously** and can affect liquidation timing
- **5-minute withdrawal cooldown** after deposits (anti-attack feature)
- **Oracle updates require user interactions** or manual poke() calls
- **30-minute cooldown** between manual oracle poke() calls
- **No partial liquidations** (minimum 20% of debt must be liquidated)

---

### Technical Documentation

See [WHITEPAPER.md](./WHITEPAPER.md) for complete technical specifications and economic model details.

---

### Contract Addresses (PulseChain Mainnet)

| Contract | Address | Verified |
|----------|---------|----------|
| pSunDAI Token | `0x5529c1cb179b2c256501031adCDAfC22D9c6d236` | [✓](https://scan.pulsechain.com/address/0x5529c1cb179b2c256501031adCDAfC22D9c6d236) |
| Vault v5.6 | `0x789472Ef7fa74cB8898Ed38cAa5d18f4D49EcC6d` | [✓](https://scan.pulsechain.com/address/0x789472Ef7fa74cB8898Ed38cAa5d18f4D49EcC6d) |
| Oracle v5.1 | `0xC19C8201701585D9087F261eaCd3Ee3345251Da3` | [✓](https://scan.pulsechain.com/address/0xC19C8201701585D9087F261eaCd3Ee3345251Da3) |

⚠️ **Always verify contract addresses before interacting.**  
⚠️ **No one will ever ask for your private keys or seed phrase.**  
⚠️ **If someone claims to be "official support," they are scamming you.**

---

## 🚨 FINAL WARNING

**USE AT YOUR OWN RISK**

This is experimental software deployed immutably with no control or liability. You may lose everything. No one can help you. No one is responsible.

**If you are not comfortable with these risks, DO NOT USE THIS PROTOCOL.**

---

**Built by ELITE TEAM6 | Open Source | Community Owned**  
**No company. No control. No promises.**
