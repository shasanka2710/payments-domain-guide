# Retry Strategies in Payment Systems

## 🧭 What is it
Patterns and strategies for safely retrying failed payment operations — balancing reliability (eventual success) with safety (no duplicate payments).

---

## 🧱 Core Concepts

- **Transient failure** — Temporary error that may succeed on retry (network timeout, rate limit)
- **Permanent failure** — Error that will never succeed (invalid account, blocked card)
- **Retry storm** — Thundering herd problem when all clients retry simultaneously
- **Exponential backoff** — Doubling wait time between retries
- **Jitter** — Random delay added to prevent synchronized retries
- **Dead Letter Queue (DLQ)** — Queue for permanently failed messages
- **Circuit Breaker** — Pattern to stop retrying when downstream is unhealthy

---

## 🔄 Retry Decision Tree

```
Payment fails:

  Error type?
    │
    ├── NETWORK TIMEOUT → Retry (check idempotency first)
    ├── RATE LIMIT (429) → Retry with backoff
    ├── SERVER ERROR (5xx) → Retry with backoff + circuit breaker
    ├── INSUFFICIENT FUNDS → DO NOT retry (notify user)
    ├── INVALID ACCOUNT → DO NOT retry (notify user)
    ├── FRAUD DECLINE → DO NOT retry (escalate)
    ├── DUPLICATE REQUEST → Return cached response
    └── SYSTEM UNAVAILABLE → Queue for later + circuit breaker
```

---

## ⚙️ Retry Strategies

### 1. Immediate Retry
```
Attempt 1 → fail → Attempt 2 immediately
Use for: Very transient errors (network blip)
Risk: Can amplify problems if system is overloaded
```

### 2. Fixed Delay
```
Attempt 1 → fail → wait 5s → Attempt 2 → fail → wait 5s → Attempt 3
Use for: Simple retry with predictable wait
Risk: Synchronization of retries (retry storm)
```

### 3. Exponential Backoff
```
Attempt 1 → fail → wait 1s
Attempt 2 → fail → wait 2s
Attempt 3 → fail → wait 4s
Attempt 4 → fail → wait 8s
...
Use for: Most distributed systems
Risk: Long wait times for high retry counts
```

### 4. Exponential Backoff with Jitter
```
wait_time = min(cap, base * 2^attempt) + random(0, max_jitter)

Example (cap=30s, base=1s, jitter=0–1s):
  Attempt 1: wait = 1s + 0.3s = 1.3s
  Attempt 2: wait = 2s + 0.7s = 2.7s
  Attempt 3: wait = 4s + 0.2s = 4.2s
  Attempt 4: wait = 8s + 0.9s = 8.9s

Best practice: ✅ Prevents retry storms
```

---

## ⚙️ Circuit Breaker Pattern

```
States:
  CLOSED → Normal operation, requests pass through
  OPEN   → Too many failures, reject all requests immediately
  HALF-OPEN → Allow limited requests to test recovery

Thresholds:
  Error rate > 50% in 30s → OPEN (trip the circuit)
  After 60s in OPEN → HALF-OPEN (test with 10% traffic)
  Success in HALF-OPEN → CLOSED (restore normal operation)

Benefit: Prevents cascade failures + gives downstream time to recover
```

---

## ⚙️ Payment-Specific Retry Rules

| Error Code | Retryable | Strategy |
|-----------|-----------|---------|
| Network timeout | ✅ Yes | Exponential backoff + idempotency |
| 429 Too Many Requests | ✅ Yes | Respect Retry-After header |
| 500/503 Server Error | ✅ Yes | Exponential backoff + circuit breaker |
| 51 Insufficient Funds | ❌ No | Dunning logic (subscription context) |
| 54 Expired Card | ❌ No | Request card update |
| 57 Transaction not permitted | ❌ No | Do not retry |
| 91 Issuer unavailable | ✅ Yes | Retry after delay |
| Duplicate transaction | N/A | Return idempotent cached response |

---

## ⚙️ Async Retry with Queues

```
Kafka-based retry pattern:

Payment fails → Publish to retry-queue (delay: 5min)
  → Consumer retries after delay
  → Success: done
  → Fail again: requeue with increased delay (30min)
  → After N attempts: move to DLQ (Dead Letter Queue)
  → DLQ: manual review / alert / compensation

Benefits:
  Decoupled from main flow
  Durable (survives restarts)
  Observable (monitor DLQ depth)
  Safe (idempotency keys prevent duplicates)
```

---

## 🧠 Mental Model

```
Retry = Redialing a phone number

  Network timeout = Phone rang, no answer → try again in 5 min
  Declined = Number disconnected → stop trying, find another way
  
  Exponential backoff = Wait longer each time (1min, 2min, 4min...)
  Jitter = Don't all call at exactly the same time
  Circuit breaker = If 10 people all got busy signal, 
                    wait before even trying
  Idempotency = Make sure same payment doesn't go through twice
                even if you called 3 times
```

---

## 🔗 Related Topics
- [Idempotency](idempotency.md)
- [Reconciliation](reconciliation.md)
- [High-Level Architecture](high-level-architecture.md)
- [Subscriptions](../06-use-cases/subscriptions.md)
- [Payment Lifecycle](../00-overview/payment-lifecycle.md)
