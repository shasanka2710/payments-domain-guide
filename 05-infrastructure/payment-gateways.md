# Payment Gateways

## 🧭 What is it
A payment gateway is the technology layer that connects a merchant's system to payment networks — handling authorization, routing, encryption, and response for online/in-person transactions.

---

## 🧱 Core Components

- **Merchant Integration** — API, SDK, hosted page, or plugin
- **Payment Page / SDK** — Secure data capture (PCI DSS scope management)
- **Tokenization Engine** — Replaces PAN with token to reduce PCI scope
- **Authorization Module** — Routes to correct payment network for approval
- **Fraud Detection** — Risk scoring, velocity checks, 3DS, device fingerprint
- **3D Secure (3DS)** — Cardholder authentication protocol (Visa: VBV, MC: SecureCode)
- **Settlement Module** — Batches and forwards settlement files to acquirer

---

## 🔄 Online Card Payment Flow

```
1. Customer enters card details on merchant checkout
2. Gateway tokenizes card data (PAN → token)
3. Gateway sends authorization request to acquirer
4. Acquirer routes to card network (Visa/MC/RuPay)
5. Card network routes to issuing bank
6. Issuer: checks balance/fraud → Approve/Decline
7. Response routed back: Issuer → Network → Acquirer → Gateway → Merchant
8. Merchant shows success/failure to customer
9. End of day: Gateway sends settlement batch to acquirer
10. Acquirer settles with merchant (T+1 or T+2)
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Protocol | HTTPS (TLS 1.2+) for merchant comms |
| Card Data | ISO 8583 (auth messages) |
| Tokenization | Network tokenization (Visa/MC) or gateway tokenization |
| 3DS Version | 3DS2 (frictionless for low-risk, challenge for high-risk) |
| PCI DSS | Gateway is PCI DSS Level 1 certified |
| Encryption | End-to-end encryption (E2EE) or P2PE |
| Webhook | Event-driven notifications (payment.succeeded, payment.failed) |

---

## 🌍 Major Gateway Players

| Region | Gateways | Features |
|--------|---------|---------|
| Global | Stripe, Adyen, Braintree | Multi-currency, orchestration |
| India | Razorpay, PayU, CCAvenue | UPI, cards, netbanking, wallets |
| USA | Stripe, Square, Authorize.Net | ACH, cards, BNPL |
| Europe | Adyen, Mollie, Worldpay | SEPA, local methods |
| APAC | 2C2P, Omise, PayMaya | Local rails |

---

## ⚖️ Gateway vs Processor vs PSP

| Feature | Gateway | Processor | PSP |
|---------|---------|-----------|-----|
| Merchant-facing | ✅ Yes | ❌ No | ✅ Yes |
| Routing/auth | ✅ Routes | ✅ Processes | ✅ Both |
| Settlement | ❌ No | Via acquirer | ✅ Yes |
| Acquiring bank | Needs one | IS the acquirer | Aggregated |
| Risk management | Partial | Partial | Full |
| Examples | Authorize.Net | FIS, TSYS | Stripe, Razorpay |

---

## ⚙️ Payment Orchestration

```
Modern Architecture:

  Merchant System
      ↓
  Orchestration Layer (e.g., Spreedly, Primer)
      ↓
  ┌──────────────────────────────────┐
  │  Gateway A  │  Gateway B  │  PSP │
  │  (primary)  │  (fallback) │      │
  └──────────────────────────────────┘
      ↓
  Networks (Visa / MC / UPI / ACH)

Benefits: Fallback routing, best authorization rates, 
          cost optimization, single integration
```

---

## 🧠 Mental Model

```
Payment Gateway = Airport terminal

  Merchant = Airline
  Customer payment = Passenger
  Gateway = Terminal (check-in, security, routing)
  Payment network = The actual runway + aircraft
  
  Terminal doesn't fly the plane (no settlement)
  Terminal routes passengers to correct gate (routing)
  Terminal handles security checks (fraud/3DS)
```

---

## 🔗 Related Topics
- [Payment Processors](payment-processors.md)
- [Key Players](../00-overview/key-players.md)
- [ISO 20022](iso-20022.md)
- [Messaging Formats](messaging-formats.md)
- [B2B Use Case](../06-use-cases/b2b.md)
