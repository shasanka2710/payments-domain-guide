# ACH — Automated Clearing House (USA)

## 🧭 What is it
US batch-based electronic fund transfer network operated by Nacha. Handles payroll, direct deposits, bill payments, and B2B transfers.

---

## 🧱 Core Components

- **Nacha** — Rule-setting body and network operator
- **ACH Operators**
  - Federal Reserve's FedACH — processes ~60% of ACH
  - EPN (Electronic Payments Network) by TCH — processes ~40%
- **ODFI (Originating Depository Financial Institution)** — Payer's bank
- **RDFI (Receiving Depository Financial Institution)** — Beneficiary's bank
- **Originator** — Entity that initiates the payment (employer, biller)
- **Receiver** — Entity receiving or authorizing the payment

---

## 🔄 How it Works (Flow)

```
1. Originator submits payment file to ODFI (payer's bank)
2. ODFI validates and transmits to ACH Operator (FedACH or EPN)
3. ACH Operator sorts entries by RDFI
4. ACH Operator transmits to respective RDFIs
5. RDFI credits/debits receiver accounts
6. Net settlement positions calculated
7. Fed Reserve settles net obligations between banks
Total time: Next business day (Standard); Same day available
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| File Format | NACHA file format (fixed-width ASCII) |
| Message Standard | ACH file spec (not ISO 20022 natively) |
| Settlement | Deferred Net Settlement via Fed Reserve |
| Standard Timing | Next Business Day (T+1) |
| Same Day ACH | Available for credits & debits (up to $1M) |
| Batch Submission | Multiple windows per day |
| Transaction Limit | $1M (Same Day); No limit for standard |
| Availability | Business days (Mon–Fri) |

---

## 🌍 ACH Transaction Types (SEC Codes)

| SEC Code | Description | Type |
|----------|-------------|------|
| PPD | Prearranged Payment & Deposit (consumer) | Credit/Debit |
| CCD | Corporate Credit or Debit (B2B) | Credit/Debit |
| WEB | Internet-initiated | Debit |
| TEL | Telephone-initiated | Debit |
| CTX | Corporate Trade Exchange (with addenda) | Credit |
| POP | Point of Purchase | Debit |
| ARC | Accounts Receivable Check | Debit |
| RCK | Re-presented Check | Debit |

---

## ⚖️ ACH vs Wire vs FedNow

| Feature | ACH | Wire (Fedwire) | FedNow |
|---------|-----|----------------|--------|
| Speed | T+1 / Same-day | Minutes | < 20 sec |
| Settlement | Deferred Net | Real-time Gross | Real-time Gross |
| Cost | Low ($0.01–$0.25) | High ($15–$50) | Low |
| Reversibility | Up to 5 days | Irrevocable | Irrevocable |
| Availability | Business hours | Business hours | 24×7×365 |
| Use Case | Payroll, bills | High-value B2B | Instant retail |
| Limit | $1M (same-day) | No limit | $500K |

---

## ⚙️ ACH Return Codes

| Code | Reason |
|------|--------|
| R01 | Insufficient Funds |
| R02 | Account Closed |
| R03 | No Account / Unable to Locate |
| R04 | Invalid Account Number |
| R07 | Authorization Revoked |
| R10 | Customer Advises Not Authorized |
| R29 | Corporate Customer Advises Not Authorized |

---

## 🧠 Mental Model

```
ACH = Overnight mail for money

  Batches collected during the day
  Sorted and shipped overnight
  Delivered next morning (T+1)
  
  Same Day ACH = Express mail (faster but costs more)
  FedNow = Instant courier (real-time)
```

---

## 🔗 Related Topics
- [Wire Transfers](wire.md)
- [FedNow](fednow.md)
- [Clearing vs Settlement](../05-infrastructure/clearing-vs-settlement.md)
- [B2B Use Case](../06-use-cases/b2b.md)
- [Payroll / Subscriptions](../06-use-cases/subscriptions.md)
