# UPI — Unified Payments Interface

## 🧭 What is it
Real-time, account-to-account push & pull payment system built on IMPS rails, operated by NPCI (India).

---

## 🧱 Core Components

- **NPCI Switch** — Central routing hub for all UPI transactions
- **PSP (Payment Service Provider)** — Banks/apps that onboard users (PhonePe, GPay, Paytm, BHIM)
- **VPA (Virtual Payment Address)** — User's payment handle (e.g., `name@upi`)
- **UPI PIN** — 4/6 digit authentication credential
- **Mandate** — Pre-authorized recurring debit instruction
- **Collect Request** — Pull payment initiated by payee

---

## 🔄 How it Works (P2P Push Flow)

```
1. Payer opens UPI app → enters VPA + amount
2. PSP App → sends PAY request to NPCI UPI Switch
3. NPCI → resolves VPA → identifies beneficiary bank
4. NPCI → routes to payer's issuing bank
5. Payer's bank: verify PIN → debit account
6. NPCI → routes credit to beneficiary's bank
7. Beneficiary's bank: credits account
8. NPCI → sends success response to both PSPs
9. Both parties notified (< 30 seconds end-to-end)
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Protocol | HTTPS/REST (PSP ↔ NPCI), ISO 8583-like internally |
| Message Format | XML over UPI API spec |
| Settlement | Deferred Net Settlement via RBI (4× daily) |
| Clearing | NPCI acts as clearinghouse |
| Transaction Limit | ₹1L default; ₹2L–5L for select categories |
| Availability | 24×7×365 |
| Authentication | UPI PIN (device-bound) |
| Interoperability | Full — any PSP ↔ any bank |

---

## 🌍 UPI Ecosystem

| Component | Examples |
|-----------|----------|
| PSP Apps | PhonePe, Google Pay, Paytm, BHIM, WhatsApp Pay |
| Issuing Banks | All major Indian banks (400+) |
| Operator | NPCI |
| Regulator | RBI |

---

## ⚙️ UPI Transaction Types

| Type | Description | Initiated By |
|------|-------------|-------------|
| P2P | Person to Person transfer | Payer (push) |
| P2M | Person to Merchant | Payer (push) or Merchant (collect) |
| Collect | Pull request from payee | Payee |
| UPI Mandate | Recurring debit | Payer pre-authorizes |
| UPI Lite | Offline small value | On-device wallet |
| UPI 123Pay | Feature phone UPI | IVR / missed call |
| UPI One World | For foreign visitors | Pre-funded wallet |

---

## ⚖️ UPI vs IMPS vs NEFT

| Feature | UPI | IMPS | NEFT |
|---------|-----|------|------|
| Speed | < 30s | < 30s | 30 min batches |
| Availability | 24×7 | 24×7 | 24×7 |
| Limit | ₹1L–5L | ₹5L | ₹50L+ |
| Auth | UPI PIN | Net banking / PIN | Net banking |
| Identifier | VPA | Mobile + MMID | IFSC + Acct No |
| Settlement | Deferred Net | Deferred Net | Deferred Net |

---

## 🧠 Mental Model

```
UPI = Email for Money

  VPA = Email Address (rahul@okicici)
  NPCI = Email Server (routes messages)
  UPI PIN = Password
  Payment = Sending/Receiving an email
  Collect = "Request money" = receiving an invoice
```

---

## 🔗 Related Topics
- [IMPS](imps.md)
- [NEFT](neft.md)
- [RTGS](rtgs.md)
- [P2P Use Case](../06-use-cases/p2p.md)
- [Payment Lifecycle](../00-overview/payment-lifecycle.md)
