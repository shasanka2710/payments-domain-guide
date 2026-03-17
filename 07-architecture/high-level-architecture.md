# High-Level Payment System Architecture

## 🧭 What is it
A system design overview of a production-grade payment platform — covering components, data flows, scalability patterns, and integration points.

---

## 🧱 Core Architectural Components

```
┌─────────────────────────────────────────────────────────┐
│                    CLIENT LAYER                          │
│  Mobile App │ Web App │ POS Terminal │ Merchant API      │
└──────────────────────┬──────────────────────────────────┘
                       │ HTTPS / REST / WebSocket
┌──────────────────────▼──────────────────────────────────┐
│                  API GATEWAY / BFF                       │
│  Auth │ Rate Limiting │ Routing │ SSL Termination        │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│              PAYMENT ORCHESTRATION LAYER                 │
│  Payment Router │ Rule Engine │ Method Selector          │
│  Idempotency │ Retry Logic │ Timeout Handling            │
└──┬──────────────────────────────────────────┬───────────┘
   │                                          │
┌──▼──────────────┐                ┌──────────▼───────────┐
│  PAYMENT ENGINE  │                │   FRAUD ENGINE        │
│  Authorization   │                │   Risk Scoring        │
│  Capture         │                │   Velocity Checks     │
│  Refunds         │                │   ML Models           │
│  Reversals       │                │   Rules Engine        │
└──┬──────────────┘                └──────────────────────┘
   │
┌──▼──────────────────────────────────────────────────────┐
│              RAILS INTEGRATION LAYER                     │
│  UPI  │  ACH  │  SWIFT  │  SEPA  │  Card Networks       │
│  NEFT │  RTGS │  Faster Payments │  RTP / FedNow        │
└──┬──────────────────────────────────────────────────────┘
   │
┌──▼──────────────────────────────────────────────────────┐
│              DATA & PERSISTENCE LAYER                    │
│  Transaction DB │ Ledger DB │ Cache (Redis)              │
│  Message Queue (Kafka) │ Event Store                     │
└─────────────────────────────────────────────────────────┘
```

---

## 🔄 Transaction Processing Flow

```
1. Client sends payment request (amount, method, beneficiary)
2. API Gateway authenticates + rate limits
3. Orchestration Layer:
   a. Generate transaction ID + idempotency key
   b. Check idempotency store (duplicate?)
   c. Call Fraud Engine → risk score
   d. Route to correct rail
4. Rail Adapter calls external payment network
5. Network returns response (sync or async)
6. Update transaction state in DB
7. Publish event to Kafka (payment.completed / payment.failed)
8. Notification service sends webhook + push/SMS
9. Reconciliation service processes end-of-day settlements
```

---

## ⚙️ State Machine (Transaction States)

```
                    ┌─────────┐
                    │ CREATED  │
                    └────┬────┘
                         │ submit to network
                    ┌────▼────┐
                    │ PENDING  │
                    └────┬────┘
              ┌──────────┴──────────┐
         ┌────▼────┐           ┌────▼────┐
         │ SUCCESS  │           │ FAILED  │
         └────┬────┘           └────┬────┘
              │                     │
    ┌─────────▼──────┐    ┌────────▼───────┐
    │ SETTLED/CLEARED │    │ RETRY / REFUND │
    └────────────────┘    └────────────────┘
```

---

## ⚙️ Key Design Principles

| Principle | Implementation |
|-----------|---------------|
| Idempotency | Unique idempotency key per request; dedupe on DB |
| Exactly-once | Idempotency + distributed locks + state machine |
| Retry safety | Exponential backoff with jitter, dead letter queue |
| Consistency | Ledger as source of truth; event sourcing |
| Scalability | Horizontal scaling of payment engines; partitioned Kafka |
| Observability | Distributed tracing (OpenTelemetry), structured logs |
| Availability | Multi-AZ, circuit breakers, failover rails |
| Security | TLS, tokenization, HSM for key management |

---

## ⚙️ Technology Stack (Reference)

| Component | Technology |
|-----------|----------|
| API Gateway | Kong / AWS API GW / Nginx |
| Payment Service | Java/Go microservices |
| Message Queue | Apache Kafka |
| Cache | Redis Cluster |
| Transaction DB | PostgreSQL (ACID) |
| Ledger | PostgreSQL / Ledger-specific DB |
| Fraud Engine | ML platform (Python) + Rules (Drools) |
| Monitoring | Prometheus + Grafana + Jaeger |
| Secret management | HashiCorp Vault / AWS Secrets Manager |

---

## 🧠 Mental Model

```
Payment System = Air traffic control

  Each payment = A flight
  API Gateway = Airport check-in
  Orchestration = Air traffic controller (routing, sequencing)
  Rail adapters = Different runways (UPI, ACH, SWIFT)
  Fraud engine = Security scanner
  Ledger = Flight log (immutable record)
  Kafka = Radio communication (event broadcasting)
  
  Guarantee: Every flight (payment) lands exactly once
```

---

## 🔗 Related Topics
- [Idempotency](idempotency.md)
- [Retries](retries.md)
- [Reconciliation](reconciliation.md)
- [Payment Lifecycle](../00-overview/payment-lifecycle.md)
- [Clearing vs Settlement](../05-infrastructure/clearing-vs-settlement.md)
