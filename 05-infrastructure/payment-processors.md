# Payment Processors

## 🧭 What is it
A payment processor handles the technical and operational processing of a transaction — connecting acquiring banks, card networks, and issuing banks to execute authorization, clearing, and settlement.

---

## 🧱 Core Components

- **Transaction Routing Engine** — Routes authorization requests to correct networks
- **Authorization Gateway** — Interfaces with card networks and issuers
- **Risk Engine** — Fraud detection, velocity checks, rules engine
- **Clearing Engine** — Aggregates transactions for settlement batch
- **Settlement Engine** — Processes interchange, net settlement to merchant accounts
- **Reporting & Reconciliation** — Transaction data, chargeback management
- **Acquiring Bank Interface** — Connection to sponsor bank for card acquiring

---

## 🔄 Authorization → Clearing → Settlement Pipeline

```
AUTHORIZATION (Real-time):
  Merchant → Processor → Network → Issuer → Approve/Decline
  Time: < 2 seconds

CLEARING (Daily):
  Processor aggregates transactions → Prepares clearing files
  → Sends to card networks (Visa, MC)
  → Networks route to issuers for clearing

SETTLEMENT (T+1 or T+2):
  Networks calculate interchange and net positions
  → Processor receives net settlement
  → Processor remits funds to merchant (minus fees)
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Auth protocol | ISO 8583 (card), REST APIs (modern), ISO 20022 |
| Clearing format | Visa/MC clearing file formats |
| Settlement | T+1 (debit/prepaid), T+2 (credit standard) |
| Uptime requirement | 99.999% (five nines) |
| TPS capacity | Large processors: 10,000–50,000+ TPS |
| Interchange | Processor passes through network interchange to issuers |
| Chargeback | Managed per card scheme rules (Visa/MC dispute procedures) |

---

## 🌍 Major Processor Landscape

| Processor | Revenue | Specialty |
|-----------|---------|-----------|
| Worldpay (FIS) | Global, large merchants | Omnichannel, enterprise |
| TSYS (Global Payments) | Issuer processing, US | Card issuing focus |
| Fiserv / First Data | US community banks | SMB, community FI |
| Adyen | Global, enterprise | Unified commerce, high-value |
| Stripe | Global, tech merchants | Developer-first, platform |
| NPCI | India | UPI, RuPay, IMPS, NACH |
| Worldline | Europe | SEPA, European focused |

---

## ⚖️ Front-End vs Back-End Processing

| Feature | Front-End Processor | Back-End Processor |
|---------|--------------------|--------------------|
| Role | Authorization routing | Clearing & settlement |
| Connects to | Card networks (Visa/MC) | Issuing banks |
| Real-time | Yes | No (batch) |
| Also called | Acquirer processor | Issuer processor |
| Example | Chase Merchant Services | TSYS (issuing), FIS |

---

## ⚙️ Interchange Economics

```
$100 Card Transaction:

  Consumer pays:          $100.00
  Interchange (to issuer): -$1.80  (e.g., 1.8%)
  Network fee (Visa/MC):  -$0.13  (assessment)
  Processor margin:       -$0.25  
  
  Merchant receives:      $97.82

Key: Interchange varies by:
  → Card type (credit > debit > prepaid)
  → Merchant category (MCC)
  → Transaction type (card-present < card-not-present)
  → Issuer country
```

---

## 🧠 Mental Model

```
Payment Processor = Logistics company for money

  Gateway = Accepts the package (merchant-facing)
  Processor = Sorts and routes the package (bank-facing)
  Network = Highway system (Visa/MC rails)
  Settlement = Delivery confirmation + payment to sender
  
  Like FedEx/UPS: accepts → sorts → routes → delivers
```

---

## 🔗 Related Topics
- [Payment Gateways](payment-gateways.md)
- [Key Players](../00-overview/key-players.md)
- [Clearing vs Settlement](clearing-vs-settlement.md)
- [ISO 20022](iso-20022.md)
- [Reconciliation](../07-architecture/reconciliation.md)
