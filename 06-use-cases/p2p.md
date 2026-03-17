# P2P — Person-to-Person Payments

## 🧭 What is it
Direct fund transfer between two individuals — the most common consumer payment use case, enabled by mobile apps and instant payment rails.

---

## 🧱 Core Components

- **Sender** — Individual initiating the transfer
- **Receiver** — Individual receiving the transfer
- **Mobile/Web App** — Initiation channel (PhonePe, Venmo, Zelle, Wise)
- **Identifier** — Phone number, VPA, email, username
- **Payment Rail** — UPI, RTP, Faster Payments, SEPA Instant
- **Notification** — Real-time SMS/push notification to both parties

---

## 🔄 P2P Flow (Universal Pattern)

```
1. Sender opens app → enters receiver identifier + amount
2. App resolves identifier → maps to bank account
3. Sender authenticates (PIN/biometric)
4. App sends payment instruction to backend
5. Backend routes via payment rail (UPI/RTP/FPS)
6. Rail routes to receiver's bank
7. Receiver's bank credits account
8. Both parties receive push notification
Total: < 30 seconds (real-time rails)
```

---

## 🌍 P2P Systems by Region

| Region | System | Rail | Identifier | Limit |
|--------|--------|------|-----------|-------|
| India | UPI (PhonePe, GPay) | IMPS | VPA / Mobile | ₹1–5L |
| USA | Zelle | RTP / FedNow | Mobile / Email | Bank-set |
| USA | Venmo / CashApp | ACH / RTP | Username | $5K/week |
| Europe | SEPA Instant apps | SCT Inst | IBAN | €100K |
| UK | Faster Payments | FPS | Mobile / Sort+Acc | £250K |
| Singapore | PayNow | FAST | Mobile / NRIC | SGD 200K |
| Australia | PayID / Osko | NPP | Mobile / Email / ABN | AUD 1M+ |

---

## ⚖️ App-Layer vs Rail-Layer

| Layer | Examples | Role |
|-------|---------|------|
| App/UX Layer | PhonePe, Venmo, Zelle, PayPay | User experience, onboarding |
| Overlay/API | UPI scheme, Zelle network | Directory, resolution |
| Rail Layer | IMPS, RTP, FPS, NPP | Actual money movement |
| Settlement | RBI, Fed, BoE, RBA | Final settlement |

---

## ⚙️ P2P Technical Considerations

| Concern | Solution |
|---------|---------|
| Duplicate payments | Idempotency keys |
| Wrong beneficiary | Confirmation name check (UK CoP, India VPA) |
| Fraud | Device binding, transaction limits, velocity checks |
| Failed credits | Return flow, refund within SLA |
| Reconciliation | UETR / UPI transaction ID tracking |
| Chargebacks | P2P typically not chargeable (push payments) |

---

## ⚙️ Confirmation of Payee (CoP)

```
UK's CoP / India's name matching:

  Sender enters: "John Smith" + account details
  System checks: does the name match the account?
  
  ✅ Match → Proceed
  ⚠️ Partial match → Warn sender
  ❌ No match → Block or warn strongly
  
  Prevents APP fraud (Authorized Push Payment scams)
```

---

## 🧠 Mental Model

```
P2P = Digital cash between friends

  App = Your digital wallet app (Venmo, PhonePe)
  Identifier = Friend's "digital address" (VPA, phone, email)
  Rail = The underground pipe money travels through
  Settlement = When the balance actually transfers between banks
  
  User sees: "Sent ✅" (even if settlement is deferred)
  Bank sees: Net settlement at scheduled windows
```

---

## 🔗 Related Topics
- [UPI](../01-india/upi.md)
- [FedNow](../02-us/fednow.md)
- [SEPA Instant](../03-europe/sepa-instant.md)
- [Idempotency](../07-architecture/idempotency.md)
- [Reconciliation](../07-architecture/reconciliation.md)
