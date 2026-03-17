# FedNow — US Instant Payment System

## 🧭 What is it
Real-time, 24×7×365 instant payment service operated by the Federal Reserve (launched July 2023). Enables immediate fund transfers for individuals and businesses across the US.

---

## 🧱 Core Components

- **Federal Reserve Banks** — Operator and settlement agent
- **Participating FIs** — Banks and credit unions connected to FedNow
- **FedNow Service** — The switching and settlement infrastructure
- **Liquidity Management Tool** — Inter-participant liquidity transfers
- **Send/Receive Capability** — Banks can implement send-only, receive-only, or both
- **Request for Payment (RFP)** — Pull payment request functionality

---

## 🔄 How it Works (Flow)

```
1. Payer initiates payment via bank app
2. Payer's bank validates request
3. Bank sends credit transfer message to FedNow Service
4. FedNow validates message and checks liquidity
5. FedNow debits sending bank's Fed account
6. FedNow credits receiving bank's Fed account
7. FedNow sends confirmation to receiving bank
8. Receiving bank credits beneficiary account
9. Both parties notified of completion
Total time: < 20 seconds, 24×7×365
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Message Format | ISO 20022 (pacs.008, pacs.002, pain.013) |
| Settlement | Real-time Gross Settlement |
| Settlement Agent | Federal Reserve |
| Transaction Limit | $500,000 per transaction |
| Availability | 24×7×365 |
| Finality | Immediate, irrevocable |
| API | REST-based API for participating FIs |
| Routing | ABA routing number + account number |

---

## 🌍 US Instant Payment Landscape

| System | Operator | Launch | Limit | Participants |
|--------|---------|--------|-------|-------------|
| FedNow | Federal Reserve | 2023 | $500K | 900+ FIs (growing) |
| RTP (Real-Time Payments) | The Clearing House | 2017 | $1M | ~300 large FIs |
| Zelle (consumer layer) | Early Warning Services | 2017 | Bank-set | ~2,200 FIs |

---

## ⚖️ FedNow vs RTP vs ACH

| Feature | FedNow | RTP | Same-Day ACH |
|---------|--------|-----|-------------|
| Speed | < 20 sec | < 20 sec | Same day |
| Settlement | RTGS | RTGS | DNS |
| Availability | 24×7×365 | 24×7×365 | Business hours |
| Limit | $500K | $1M | $1M |
| Operator | Fed Reserve | The Clearing House | FedACH/EPN |
| Participant coverage | Growing | Large FIs | All FIs |
| Message format | ISO 20022 | ISO 20022 | NACHA format |

---

## ⚙️ Request for Payment (RFP)

```
B2B / Invoice Use Case:

  Biller → Sends RFP to Payer's bank (via FedNow)
  Payer's bank → Presents to payer for approval
  Payer approves → Triggers instant payment
  Biller receives funds immediately
  
Use cases: Invoice payment, bill collection, A/R automation
```

---

## 🧠 Mental Model

```
FedNow = Fed-operated UPI for the US

  UPI (India) = NPCI-operated instant rails
  FedNow (US) = Fed-operated instant rails
  
  Both: 24×7, real-time, account-to-account
  Difference: FedNow = direct Fed rails (no overlay)
              UPI = overlay on IMPS + VPA layer
```

---

## 🔗 Related Topics
- [ACH](ach.md)
- [Wire Transfers](wire.md)
- [UPI (India equivalent)](../01-india/upi.md)
- [SEPA Instant (EU equivalent)](../03-europe/sepa-instant.md)
- [ISO 20022](../05-infrastructure/iso-20022.md)
