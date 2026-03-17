# Forex — Foreign Exchange in Payments

## 🧭 What is it
The conversion of one currency to another as part of cross-border payment processing. FX is embedded in every international payment and affects cost, timing, and settlement.

---

## 🧱 Core Components

- **Spot Rate** — Current exchange rate for immediate delivery (T+2)
- **Forward Rate** — Agreed rate for future delivery
- **FX Spread** — Difference between buy and sell rates (bank profit)
- **CLS (Continuous Linked Settlement)** — Multi-currency FX settlement system
- **PVP (Payment versus Payment)** — Simultaneous exchange to eliminate settlement risk
- **FX Liquidity Providers** — Banks, market makers, ECNs

---

## 🔄 FX in a Cross-Border Payment

```
Scenario: India → USA ($1,000)

1. Sender in India has INR
2. Payer's bank (ICICI) quotes exchange rate (e.g., 1 USD = 83 INR)
3. ICICI debits ₹83,000 from sender
4. ICICI or its FX desk converts INR → USD
5. USD is credited to Nostro account or sent via correspondent
6. Correspondent routes $1,000 to USA beneficiary bank
7. Beneficiary receives $1,000 (minus correspondent fees)

Sender sees: ₹83,000 debited
Receiver sees: ~$985 (after fees)
FX spread + fees = the difference
```

---

## ⚙️ FX Settlement Models

| Model | Description | Risk |
|-------|-------------|------|
| **Free of Payment (FoP)** | FX leg and payment leg settle separately | Settlement risk (Herstatt risk) |
| **PVP (Payment vs Payment)** | Both legs settle simultaneously | No settlement risk |
| **CLS (Continuous Linked Settlement)** | Multilateral PVP via CLS Bank | Minimal — industry gold standard |
| **On-behalf-of** | Bank nets and settles on client's behalf | Depends on bank |

---

## ⚙️ CLS (Continuous Linked Settlement)

```
CLS Bank (owned by 80+ major FIs):

  Settles $6.5T+ in FX daily (PVP model)
  
  Mechanism:
    Bank A sends USD, receives EUR
    Bank B sends EUR, receives USD
    
    CLS: Simultaneously credits/debits both banks
    Both legs settle AT THE SAME TIME
    Eliminates Herstatt risk entirely
  
  Supported: 18 currencies (USD, EUR, GBP, JPY, CHF, AUD, etc.)
```

---

## 🌍 FX Rate Tiers

| Tier | Participant | Spread |
|------|-------------|--------|
| Tier 1 | Central Banks, BIS | Near zero |
| Tier 2 | Large commercial banks | 0.01–0.05% |
| Tier 3 | Smaller banks, FX platforms | 0.1–0.5% |
| Retail (traditional) | Bank customers | 1–3% |
| Retail (fintech) | Wise, Revolut | 0.3–0.7% |
| Remittance (traditional) | WU, MoneyGram | 3–8% |

---

## ⚖️ FX Cost in Remittance

| Provider | Fee | FX Markup | Total Cost on $200 |
|----------|-----|-----------|---------------------|
| Traditional Bank Wire | $20–50 | 2–3% | $24–56 |
| Western Union | $5–10 | 2–4% | $9–18 |
| MoneyGram | $5–8 | 2–3% | $9–14 |
| Wise (TransferWise) | $4–6 | 0.3–0.7% | $5–8 |
| Remitly | $3–5 | 1–2% | $5–9 |
| Revolut | $0 | 0.5% (weekend surcharge) | $1–3 |

---

## 🧠 Mental Model

```
FX = Currency exchange booth at airport — but at global scale

  Tourist buys USD with EUR = you pay the "retail" price
  Banks trade EUR/USD with each other = "wholesale" price
  
  The wider the spread = the more the middleman earns
  Fintechs win by compressing the spread and passing savings to users
  
  PVP/CLS = Making sure both sides of the exchange happen 
             simultaneously (no one runs away with the money)
```

---

## 🔗 Related Topics
- [SWIFT](swift.md)
- [Correspondent Banking](correspondent-banking.md)
- [International Remittance](../06-use-cases/international-remittance.md)
- [Clearing vs Settlement](../05-infrastructure/clearing-vs-settlement.md)
- [Key Players](../00-overview/key-players.md)
