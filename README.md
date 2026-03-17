# 💳 Payments Domain Guide

> A visual-thinking-first knowledge base for the global payments ecosystem — designed for engineers, architects, and product managers.

---

## 🧭 What is this?

A structured, hierarchical reference covering:
- **India** payment systems (UPI, NEFT, RTGS, IMPS, RuPay, BBPS)
- **US** payment systems (ACH, Wire, FedNow, SWIFT)
- **European** payment systems (SEPA, SEPA Instant, TARGET2)
- **Cross-border** payments (SWIFT, Correspondent Banking, Forex)
- **Infrastructure** (Clearing, Settlement, Gateways, ISO 20022)
- **Use cases** (P2P, B2B, Subscriptions, Remittance)
- **Architecture** patterns (Reconciliation, Idempotency, Retries)

---

## 🗂️ Repository Structure

```
payments-domain-guide/
│
├── 00-overview/
│   ├── payments-landscape.md      ← Global map of payment systems
│   ├── payment-lifecycle.md       ← Initiation → Processing → Clearing → Settlement
│   └── key-players.md             ← Banks, PSPs, Networks, Regulators
│
├── 01-india/
│   ├── upi.md                     ← Real-time P2P & P2M
│   ├── neft.md                    ← Batch, net settlement
│   ├── rtgs.md                    ← High-value, real-time gross
│   ├── imps.md                    ← 24×7 instant interbank
│   ├── rupay.md                   ← Domestic card network
│   └── bbps.md                    ← Bill payment system
│
├── 02-us/
│   ├── ach.md                     ← Batch ACH network
│   ├── wire.md                    ← Fedwire & CHIPS
│   ├── fednow.md                  ← Real-time instant payments
│   └── swift-us.md                ← SWIFT in US context
│
├── 03-europe/
│   ├── sepa.md                    ← Single Euro Payments Area
│   ├── sepa-instant.md            ← SEPA Instant Credit Transfer
│   └── target2.md                 ← ECB's RTGS system
│
├── 04-cross-border/
│   ├── swift.md                   ← Global messaging network
│   ├── correspondent-banking.md   ← Nostro/Vostro model
│   └── forex.md                   ← FX rates, conversion
│
├── 05-infrastructure/
│   ├── clearing-vs-settlement.md  ← Core concepts
│   ├── payment-gateways.md        ← Gateway architecture
│   ├── payment-processors.md      ← Processing pipeline
│   ├── iso-20022.md               ← Modern messaging standard
│   └── messaging-formats.md       ← MT, MX, ISO 8583
│
├── 06-use-cases/
│   ├── p2p.md                     ← Person-to-person flows
│   ├── b2b.md                     ← Business-to-business flows
│   ├── subscriptions.md           ← Recurring payment patterns
│   └── international-remittance.md ← Cross-border money transfer
│
└── 07-architecture/
    ├── high-level-architecture.md ← System design overview
    ├── reconciliation.md          ← Matching & reconciliation
    ├── idempotency.md             ← Duplicate prevention
    └── retries.md                 ← Retry strategies & patterns
```

---

## 🚀 Quick Navigation

| I want to learn about... | Go to |
|--------------------------|-------|
| How payments work end-to-end | [Payment Lifecycle](00-overview/payment-lifecycle.md) |
| India's UPI system | [UPI](01-india/upi.md) |
| US ACH transfers | [ACH](02-us/ach.md) |
| SEPA in Europe | [SEPA](03-europe/sepa.md) |
| International wire transfers | [SWIFT](04-cross-border/swift.md) |
| Clearing vs Settlement | [Clearing vs Settlement](05-infrastructure/clearing-vs-settlement.md) |
| Building payment systems | [Architecture](07-architecture/high-level-architecture.md) |

---

## 🧠 Mental Model

```
PAYMENT = INITIATION → ROUTING → CLEARING → SETTLEMENT
            (who pays)  (which rails?)  (netting)  (actual
                                                    funds move)
```

---

## 🔗 Start Here

→ [Global Payments Landscape](00-overview/payments-landscape.md)  
→ [Payment Lifecycle](00-overview/payment-lifecycle.md)  
→ [Key Players](00-overview/key-players.md)
