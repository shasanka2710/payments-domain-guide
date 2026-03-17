# Subscriptions — Recurring Payment Patterns

## 🧭 What is it
Automated, recurring payment collection on a predefined schedule — used for SaaS, utilities, media, insurance, loan EMIs, and membership services.

---

## 🧱 Core Components

- **Mandate / Authorization** — Customer's upfront consent for recurring debits
- **Billing Engine** — Calculates amounts, generates payment requests on schedule
- **Payment Schedule** — Fixed or variable frequency and amount
- **Dunning Logic** — Retry strategy for failed payments
- **Proration** — Partial period billing (upgrades, cancellations)
- **Webhook/Notification** — Events: payment.succeeded, payment.failed, mandate.revoked

---

## 🔄 Subscription Lifecycle

```
SETUP:
  1. Customer subscribes → provides payment method
  2. Mandate/authorization captured (card, ACH, UPI, SEPA DD)
  3. Initial charge or trial period starts

RECURRING CYCLE:
  4. Billing engine triggers on schedule
  5. Payment instruction sent to processor/bank
  6. Success → service continues, receipt sent
  7. Failure → dunning logic triggered

CANCELLATION:
  8. Customer cancels → mandate revoked
  9. Billing engine disables future charges
  10. Pro-rated refund (if applicable)
```

---

## 🌍 Recurring Payment Methods by Region

| Region | Method | Type | Notes |
|--------|--------|------|-------|
| India | NACH (e-NACH) | Direct debit mandate | Bank mandate for EMI/SIP |
| India | UPI AutoPay | UPI mandate | Up to ₹15,000/day auto-debit |
| USA | ACH debit | Pull payment | PPD/WEB, up to $1M/day |
| USA | Card-on-file | Card pull | Visa/MC recurring rules |
| Europe | SEPA Direct Debit | Pull payment | Mandate required, 8-week reversal |
| UK | Direct Debit (Bacs) | Pull payment | UK standard for bills |
| Global | Card recurring | Pull payment | CNP recurring transaction |

---

## ⚙️ UPI AutoPay (India)

```
Setup Flow:
  1. Merchant presents UPI AutoPay mandate screen
  2. Customer authorizes via UPI PIN
  3. Mandate registered with NPCI (amount, frequency, start/end)
  
Execution Flow (auto-debit day):
  4. Merchant's system sends debit notification (24h before)
  5. Customer can block if needed
  6. On execution date: auto-debit happens without user action
  7. Confirmation sent to customer
  
Limits: ₹15,000/transaction (for <₹15K, no pre-debit notification needed)
```

---

## ⚙️ SEPA Direct Debit Mandate Flow

```
1. Creditor (biller) sends mandate to debtor (customer)
2. Debtor signs (physically or electronically)
3. Creditor submits to bank (BOU)
4. Pre-notification sent (5 business days before first debit)
5. Creditor sends debit instruction (SDD Core: D-2 days before)
6. STEP2 processes → debtor's bank debits account
7. Customer has:
   → Pre-authorized period: 8 weeks to dispute (CORE)
   → Unauthorized: 13 months to dispute
```

---

## ⚖️ Retry / Dunning Strategies

| Retry | Timing | Notes |
|-------|--------|-------|
| Immediate retry | Same day | Only for soft declines |
| Day 3 retry | 3 days later | Allow bank processing time |
| Day 7 retry | 1 week later | Weekend/holiday avoidance |
| Day 14 final | 2 weeks | Last attempt |
| Dunning email | Each failure | Prompt customer to update payment |
| Service pause | After N failures | Suspend until payment updated |

---

## 🧠 Mental Model

```
Subscriptions = Standing order at a restaurant

  Mandate = You give the restaurant permission to charge you
  Billing engine = Waiter that shows up every month
  Dunning = Follow-up call when your card is declined
  
  Push (card/UPI) = Restaurant charges YOUR card
  Pull (SEPA DD/ACH) = Restaurant debits YOUR account directly
  
  Difference: Pull = more reliable for billers (less card expiry issues)
              Push = more customer control
```

---

## 🔗 Related Topics
- [BBPS](../01-india/bbps.md)
- [UPI](../01-india/upi.md)
- [ACH](../02-us/ach.md)
- [SEPA](../03-europe/sepa.md)
- [Retries](../07-architecture/retries.md)
