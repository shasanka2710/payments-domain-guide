# RuPay — India's Domestic Card Network

## 🧭 What is it
India's domestic card payment network operated by NPCI. Alternative to Visa/Mastercard, designed for Indian market with lower transaction costs.

---

## 🧱 Core Components

- **NPCI** — Network operator and scheme owner
- **Issuing Banks** — Banks that issue RuPay cards to customers
- **Acquiring Banks** — Banks that accept RuPay at POS/online
- **RuPay Switch** — Central transaction routing and authorization
- **Card Variants** — Debit, Credit, Prepaid, Contactless
- **Co-branded Programs** — Jan Dhan (PMJDY), Kisan, Corporate cards

---

## 🔄 How it Works (Card Transaction Flow)

```
1. Cardholder presents RuPay card at POS / enters online
2. Acquirer sends authorization request to RuPay Switch
3. RuPay Switch routes to Issuing Bank
4. Issuer: checks balance / credit limit → Approve / Decline
5. Response sent back via RuPay Switch → Acquirer → Merchant
6. Transaction completed
7. Clearing: NPCI nets obligations between issuers and acquirers
8. Settlement: Net funds transferred via RBI
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Protocol | ISO 8583 (authorization messages) |
| Clearing | NPCI CAS (Card Authorization Switch) |
| Settlement | Deferred Net via RBI |
| Security | EMV chip, OTP, tokenization |
| Contactless | NFC (RuPay Contactless) |
| UPI Linkage | RuPay card linked to UPI (RuPay on UPI) |
| International | Accepted via JCB, Discover, DinaCard networks |

---

## 🌍 RuPay Card Variants

| Variant | Target | Key Feature |
|---------|--------|-------------|
| RuPay Classic | Mass market | Basic debit |
| RuPay Platinum | Premium | Rewards, insurance |
| RuPay Select | Super premium | Airport lounge, high limits |
| RuPay PMJDY | Financial inclusion | Zero-balance accounts |
| RuPay Credit | Credit segment | UPI-linked credit card |
| RuPay Prepaid | Gift/travel | Prepaid wallet card |

---

## ⚖️ RuPay vs Visa vs Mastercard

| Feature | RuPay | Visa | Mastercard |
|---------|-------|------|------------|
| Origin | India (NPCI) | USA | USA |
| Domestic fee | Lower | Higher | Higher |
| International acceptance | Limited (growing) | Global | Global |
| Data residency | India (compliant) | Offshore | Offshore |
| UPI integration | Native | No | No |
| Govt programs | PMJDY, etc. | No | No |
| Market share (India) | ~60% debit cards | ~25% | ~15% |

---

## ⚙️ RuPay on UPI

```
Innovation: Credit card on UPI rails

  RuPay Credit Card → Linked to UPI app
  Merchant scans UPI QR code
  Customer pays via RuPay Credit (not debit)
  Issuer extends credit → settles via UPI rails
  MDR charged to merchant (new revenue model)
```

---

## 🧠 Mental Model

```
RuPay = India's homegrown Visa/Mastercard

  NPCI owns the rails (like Visa owns its network)
  But data stays in India (sovereignty)
  Much lower transaction fees (India-focused pricing)
  Deeply integrated with govt financial inclusion programs
```

---

## 🔗 Related Topics
- [UPI](upi.md)
- [IMPS](imps.md)
- [Key Players](../00-overview/key-players.md)
- [Payment Processors](../05-infrastructure/payment-processors.md)
- [P2P Use Case](../06-use-cases/p2p.md)
