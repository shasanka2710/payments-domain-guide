# Idempotency in Payment Systems

## 🧭 What is it
The property that ensures a payment operation produces the same result regardless of how many times it is executed with the same input. Critical for preventing duplicate payments in distributed systems.

---

## 🧱 Core Concepts

- **Idempotency Key** — Unique client-generated identifier for a payment request
- **Deduplication Store** — Cache/DB that tracks processed idempotency keys
- **Idempotent Response** — Returning the same result for duplicate requests
- **Exactly-once semantics** — Each payment executes exactly once, regardless of retries
- **At-least-once delivery** — Message queues may redeliver; idempotency handles this

---

## 🔄 Idempotency Flow

```
REQUEST 1 (original):
  Client → POST /payments {idempotency_key: "key-abc-123", amount: 100}
  Server: check key → not found → PROCESS PAYMENT → store result
  Response: {status: "success", transaction_id: "txn-001"}

REQUEST 2 (retry — same key):
  Client → POST /payments {idempotency_key: "key-abc-123", amount: 100}
  Server: check key → FOUND → return CACHED RESPONSE
  Response: {status: "success", transaction_id: "txn-001"}  ← SAME RESULT

No duplicate payment created ✅
```

---

## ⚙️ Implementation Pattern

```
// Pseudocode
function processPayment(request):
  key = request.idempotency_key
  
  // Step 1: Check idempotency store
  cached = idempotencyStore.get(key)
  if cached:
    return cached.response  // Return previous result
  
  // Step 2: Acquire lock (prevent concurrent duplicates)
  lock = distributedLock.acquire(key, ttl=30s)
  
  // Step 3: Double-check after lock
  cached = idempotencyStore.get(key)
  if cached:
    lock.release()
    return cached.response
  
  // Step 4: Process payment
  result = paymentEngine.execute(request)
  
  // Step 5: Store result
  idempotencyStore.set(key, result, ttl=24h)
  lock.release()
  
  return result
```

---

## ⚙️ Idempotency Key Design

| Principle | Implementation |
|-----------|---------------|
| Client-generated | UUID v4 / ULID on client side |
| Unique per request | Include: payer + payee + amount + timestamp + nonce |
| Stable on retry | Same key must be sent on every retry attempt |
| TTL | 24 hours (after which, new key = new request) |
| Scope | Per API endpoint (same key can be used on different endpoints) |

---

## ⚙️ Network-Level Idempotency

```
Banking rails have their own idempotency:
  
  UPI: Transaction Reference Number (TRN) — unique per transaction
  IMPS: NPCI Reference + Bank Reference
  SWIFT: UETR (Unique End-to-End Transaction Reference) in GPI
  ACH: Trace Number — unique per entry
  SEPA: Instruction ID + End-to-End ID
  
  If your system generates a duplicate with the SAME network ID:
    → Network rejects as duplicate
  
  If your system sends the SAME payment TWICE with different IDs:
    → Network processes both = DUPLICATE PAYMENT
  
  Lesson: Idempotency at your layer prevents the second scenario
```

---

## ⚖️ Idempotency vs Exactly-Once

| Concept | Description |
|---------|-------------|
| At-most-once | Message sent once, may be lost | Not suitable for payments |
| At-least-once | Message retried until confirmed | May duplicate; needs idempotency |
| Exactly-once | Guaranteed single execution | Achieved via idempotency + transactions |
| Idempotency | Makes at-least-once behave like exactly-once | ✅ Standard approach |

---

## 🧠 Mental Model

```
Idempotency = Stamped "PAID" on an invoice

  When you mark an invoice PAID:
    First time: Process payment + stamp PAID
    Second time: See PAID stamp → stop, don't pay again
  
  Idempotency key = The PAID stamp
  Deduplication store = The filing cabinet of paid invoices
  
  Without it: Double payment on network retry
  With it: "Already processed, here's your receipt"
```

---

## 🔗 Related Topics
- [Retries](retries.md)
- [Reconciliation](reconciliation.md)
- [High-Level Architecture](high-level-architecture.md)
- [Payment Lifecycle](../00-overview/payment-lifecycle.md)
- [P2P Use Case](../06-use-cases/p2p.md)
