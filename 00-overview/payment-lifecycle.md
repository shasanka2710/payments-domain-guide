# Payment Lifecycle

## 🧭 What is it
The end-to-end journey of a payment — from initiation by payer to final credit at beneficiary — across four universal stages.

---

## 🧱 Four Universal Stages

```
INITIATION → AUTHORIZATION → CLEARING → SETTLEMENT
```

| Stage | What Happens | Who Acts |
|-------|-------------|----------|
| **Initiation** | Payment instruction created | Payer / App / Merchant |
| **Authorization** | Funds verified, transaction approved | Issuing Bank / Switch |
| **Clearing** | Obligations calculated, messages exchanged | Clearinghouse / Network |
| **Settlement** | Actual money movement between banks | Central Bank / RTGS |

---

## 🔄 Detailed Flow

```
1. INITIATION
   Payer enters amount + beneficiary → Payment instruction created
   ↓
2. AUTHENTICATION
   PIN / Biometric / OTP verified → Transaction authenticated
   ↓
3. AUTHORIZATION
   Issuing bank checks: funds? limits? fraud? → Approve / Decline
   ↓
4. ROUTING
   Instruction routed via correct rail (UPI/ACH/SWIFT/SEPA)
   ↓
5. CLEARING
   Obligations netted (or gross settled) → Settlement obligation created
   ↓
6. SETTLEMENT
   Central bank / custodian moves funds between bank accounts
   ↓
7. CONFIRMATION
   Payer & beneficiary notified → Transaction complete
```

---

## ⚙️ Real-Time vs Batch

| Aspect | Real-Time (UPI, FedNow) | Batch (NEFT, ACH) |
|--------|------------------------|-------------------|
| Authorization | Instant | Queued |
| Clearing | Per transaction | End-of-batch |
| Settlement | Near-real-time or deferred | Scheduled windows |
| Notification | Immediate | After batch runs |
| Use case | P2P, retail | Payroll, bulk payments |

---

## ⚙️ Push vs Pull

| Model | Description | Examples |
|-------|-------------|----------|
| **Push** | Sender initiates → credits receiver | UPI, IMPS, Wire, SEPA CT |
| **Pull** | Receiver requests → debits sender | ACH Debit, NACH, SEPA DD, Card |

---

## ⚙️ Gross vs Net Settlement

```
GROSS (RTGS):
  Bank A → ₹1M → Bank B    (settled individually, immediately)
  Bank C → ₹2M → Bank A    (settled individually, immediately)

NET (ACH/NEFT):
  Bank A owes Bank B: ₹1M
  Bank B owes Bank A: ₹0.6M
  Net: Bank A pays Bank B ₹0.4M (settled at end of cycle)
```

| Feature | Gross (RTGS) | Net (ACH) |
|---------|-------------|-----------|
| Settlement | Per transaction | Batched |
| Liquidity needed | High (full amount) | Low (net amount) |
| Risk | Low (immediate finality) | Higher (intraday exposure) |
| Speed | Real-time | Deferred |

---

## 🧠 Mental Model

```
Lifecycle = Supply chain for money:

  Factory (Payer) 
    → Logistics (Routing/Rails) 
      → Warehouse (Clearing) 
        → Delivery (Settlement) 
          → Customer (Beneficiary)
```

---

## 🔗 Related Topics
- [Payments Landscape](payments-landscape.md)
- [Clearing vs Settlement](../05-infrastructure/clearing-vs-settlement.md)
- [High-Level Architecture](../07-architecture/high-level-architecture.md)
- [Reconciliation](../07-architecture/reconciliation.md)
