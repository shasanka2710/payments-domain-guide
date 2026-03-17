# Global Payments Landscape

## 🧭 What is it
A macro-level map of the world's payment systems — who operates them, what rails they run on, and how money moves across geographies.

---

## 🧱 Core Components

- **Payment Rails** — The underlying network/infrastructure
  - Real-Time Gross Settlement (RTGS)
  - Automated Clearing House (ACH / Batch)
  - Card Networks (Visa, Mastercard, RuPay, UnionPay)
  - SWIFT (Messaging layer for cross-border)
- **Payment Layers**
  - Initiation layer (apps, POS, APIs)
  - Processing layer (authorization, routing)
  - Clearing layer (netting obligations)
  - Settlement layer (actual fund transfer)
- **Key Operators**
  - Central Banks (RBI, Fed, ECB)
  - Network Operators (NPCI, Nacha, EBA Clearing)
  - Commercial Banks
  - Payment Service Providers (PSPs)

---

## 🌍 Regional Systems Map

| Region | Retail (Fast) | Retail (Batch) | High-Value RTGS | Card Network | Cross-Border |
|--------|--------------|----------------|-----------------|--------------|--------------|
| India | UPI, IMPS | NEFT | RTGS | RuPay | SWIFT |
| USA | FedNow, RTP | ACH (Nacha) | Fedwire, CHIPS | Visa/MC | SWIFT |
| Europe | SEPA Instant | SEPA CT/DD | TARGET2 | Visa/MC | SWIFT/TARGET2 |
| UK | Faster Payments | Bacs | CHAPS | Visa/MC | SWIFT |
| Singapore | PayNow | GIRO | MEPS+ | Visa/MC | SWIFT |
| Australia | NPP/Osko | BECS | RITS | Visa/MC | SWIFT |

---

## 🔄 How Money Flows (High Level)

```
Payer
  │
  ▼
Payer's Bank (Debit)
  │
  ▼
Payment Rail (UPI / ACH / SWIFT / SEPA)
  │
  ▼
Clearinghouse / Switch
  │
  ▼
Beneficiary's Bank (Credit)
  │
  ▼
Beneficiary
```

---

## ⚙️ Technical Dimensions

| Dimension | Options |
|-----------|---------|
| Speed | Real-time / Near-real-time / Batch / Next-day / T+2 |
| Direction | Push (sender initiates) / Pull (receiver requests) |
| Scope | Domestic / Cross-border |
| Settlement | Gross (RTGS) / Net (ACH, SEPA) |
| Finality | Immediate / Deferred |
| Message Format | ISO 8583 / ISO 20022 / MT (SWIFT) / Proprietary |

---

## ⚖️ Key Comparisons

| Feature | UPI (India) | FedNow (US) | SEPA Instant (EU) |
|---------|-------------|-------------|-------------------|
| Speed | < 30 sec | < 20 sec | < 10 sec |
| Availability | 24×7×365 | 24×7×365 | 24×7×365 |
| Settlement | NPCI → RBI | Fed Reserve | ECB / EBA |
| Limit | ₹1–5L | $500K | €100K |
| Model | Overlay on IMPS | New rails | Overlay on SEPA |

---

## 🧠 Mental Model

```
Think of payments like POSTAL MAIL:

  INITIATION  = Writing a letter
  ROUTING     = Post office sorting
  CLEARING    = Counting who owes whom across routes
  SETTLEMENT  = Final delivery + account books updated
```

---

## 🔗 Related Topics
- [Payment Lifecycle](payment-lifecycle.md)
- [Key Players](key-players.md)
- [SWIFT](../04-cross-border/swift.md)
- [ISO 20022](../05-infrastructure/iso-20022.md)
