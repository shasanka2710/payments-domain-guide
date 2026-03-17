# RTGS — Real-Time Gross Settlement

## 🧭 What is it
High-value, real-time, transaction-by-transaction settlement system operated by RBI (India). Each transaction settled individually in RBI's books.

---

## 🧱 Core Components

- **RBI RTGS System** — Core settlement engine
- **RTGS Service Centre** — Bank's gateway to the system
- **Queue Management** — Manages pending transactions during liquidity shortfall
- **Intraday Liquidity** — RBI provides collateralized credit during day
- **SWIFT Messaging** — ISO 20022 messages used for communication

---

## 🔄 How it Works (Flow)

```
1. Payer initiates high-value transfer (min ₹2L)
2. Payer's bank validates instruction
3. Bank sends RTGS message to RBI RTGS system
4. RBI checks: does payer's bank have sufficient balance in current account?
5a. YES → Debit payer's bank account → Credit beneficiary's bank account → IMMEDIATE
5b. NO  → Queue transaction → Wait for inbound funds or liquidity facility
6. Beneficiary bank credits customer account within 30 min
7. Final settlement confirmed — IRREVOCABLE
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Message Format | ISO 20022 (pacs.008, pacs.009) |
| Settlement Type | Real-Time Gross Settlement (RTGS) |
| Settlement Agent | RBI |
| Min Amount | ₹2,00,000 |
| Max Amount | No upper limit |
| Availability | 24×7×365 (since Dec 2020) |
| Finality | Immediate, irrevocable |
| Intraday Liquidity | Collateralized credit from RBI |
| Queue Mechanism | FIFO with priority override |

---

## 🌍 Global RTGS Comparison

| Country | System | Operator |
|---------|--------|---------|
| India | RTGS | RBI |
| USA | Fedwire | Federal Reserve |
| Europe | TARGET2 | ECB |
| UK | CHAPS | Bank of England |
| Singapore | MEPS+ | MAS |
| Australia | RITS | RBA |

---

## ⚖️ RTGS vs NEFT vs IMPS

| Feature | RTGS | NEFT | IMPS |
|---------|------|------|------|
| Settlement | Gross (per txn) | Net (batch) | Net (deferred) |
| Speed | Immediate | 30–60 min | Immediate |
| Min Amount | ₹2,00,000 | ₹1 | ₹1 |
| Max Amount | No limit | No limit | ₹5,00,000 |
| Risk | Lowest | Medium | Medium |
| Liquidity Needed | High | Low | Low |
| Finality | Immediate | End of batch | Near-real-time |

---

## ⚙️ Liquidity Management

```
Bank A sends ₹10Cr via RTGS:
  → RBI checks Bank A's current account balance
  → If balance ≥ ₹10Cr: SETTLE IMMEDIATELY
  → If balance < ₹10Cr: 
      Option 1: Queue until inbound funds arrive
      Option 2: Use Intraday Liquidity (collateral-backed)
      Option 3: Use Marginal Standing Facility (end of day)
```

---

## 🧠 Mental Model

```
RTGS = Wire transfer one suitcase at a time

  Each transaction = One suitcase of cash
  Physically moved from Bank A's vault (RBI account)
  to Bank B's vault (RBI account)
  Immediately, one by one, no batching
```

---

## 🔗 Related Topics
- [NEFT](neft.md)
- [IMPS](imps.md)
- [TARGET2](../03-europe/target2.md)
- [Clearing vs Settlement](../05-infrastructure/clearing-vs-settlement.md)
- [Wire Transfers (US)](../02-us/wire.md)
