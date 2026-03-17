# NEFT — National Electronic Funds Transfer

## 🧭 What is it
Batch-based, deferred net settlement interbank fund transfer system operated by RBI (India). Available 24×7×365 since Dec 2019.

---

## 🧱 Core Components

- **RBI NEFT Clearing Centre** — Central processor for all NEFT transactions
- **NEFT Service Centre** — Bank's connection point to RBI
- **IFSC Code** — 11-character bank branch identifier (routing key)
- **Batch Processing Engine** — Groups transactions into hourly batches
- **Net Settlement** — Calculates net positions across all banks per batch

---

## 🔄 How it Works (Flow)

```
1. Payer initiates transfer via net banking / mobile app
2. Payer's bank receives instruction
3. Bank queues transaction → aggregates with others
4. At batch cut-off: bank sends batch to RBI NEFT centre
5. RBI NEFT centre processes all batches
6. Net settlement positions calculated per bank
7. RBI debits/credits banks' current accounts (settlement)
8. Beneficiary bank credits customer account
9. Credit confirmation sent to originating bank
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Message Format | ISO 20022 (migrated from proprietary) |
| Settlement Type | Deferred Net Settlement (DNS) |
| Batch Frequency | 48 half-hourly batches (24×7) |
| Transaction Limit | No upper limit (min ₹1) |
| Availability | 24×7×365 |
| Identifier | IFSC Code + Account Number |
| Settlement Agent | RBI (current accounts of banks) |
| Return Time | Within 2 hours of next batch |

---

## 🌍 Participant Types

| Participant | Role |
|------------|------|
| Direct Members | Large banks with direct RBI connection |
| Sub-Members | Smaller banks routing through direct members |
| RBI | Operator + Settlement Agent |

---

## ⚖️ NEFT vs RTGS vs IMPS

| Feature | NEFT | RTGS | IMPS |
|---------|------|------|------|
| Speed | 30–60 min (batch) | Immediate | Immediate |
| Settlement | Deferred Net | Real-Time Gross | Deferred Net |
| Min Amount | ₹1 | ₹2,00,000 | ₹1 |
| Max Amount | No limit | No limit | ₹5,00,000 |
| Availability | 24×7 | 24×7 | 24×7 |
| Use Case | General transfers | High-value | Urgent retail |
| Charges | Regulated (free for retail) | Higher fees | Moderate |

---

## ⚙️ NEFT Batch Timeline

```
Each half-hour window:
  :00 → Banks submit transactions to RBI
  :10 → RBI processes batch
  :15 → Net settlement in RBI books
  :20 → Banks credit beneficiary accounts
  :30 → Next batch begins
```

---

## 🧠 Mental Model

```
NEFT = Bus service for money

  Each bus (batch) leaves every 30 minutes
  All passengers (transactions) on the same bus settle together
  Net fares calculated at destination (net settlement)
  Vs RTGS = Private taxi (instant, one at a time, expensive)
```

---

## 🔗 Related Topics
- [RTGS](rtgs.md)
- [IMPS](imps.md)
- [UPI](upi.md)
- [Clearing vs Settlement](../05-infrastructure/clearing-vs-settlement.md)
- [Payment Lifecycle](../00-overview/payment-lifecycle.md)
