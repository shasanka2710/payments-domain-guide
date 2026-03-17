# SEPA Instant Credit Transfer (SCT Inst)

## 🧭 What is it
Real-time, 24×7×365 euro credit transfer scheme under SEPA. Transactions completed in ≤ 10 seconds, available across the SEPA zone.

---

## 🧱 Core Components

- **EPC SCT Inst Rulebook** — Governing scheme rules
- **RT1 (EBA Clearing)** — Pan-European instant clearing infrastructure
- **TIPS (ECB)** — TARGET Instant Payment Settlement — 24×7 central bank settlement
- **Bilateral CSMs** — National or bilateral clearing & settlement mechanisms
- **PSPs** — Payment Service Providers offering instant payments to customers

---

## 🔄 How it Works (Flow)

```
1. Payer initiates instant transfer via banking app
2. Payer's PSP validates: IBAN, BIC, fraud checks
3. PSP sends pacs.008 message to clearing layer (RT1 or TIPS)
4. Clearing layer forwards to beneficiary PSP
5. Beneficiary PSP confirms availability (≤ 5 sec timeout)
6. Clearing settles the transaction
   → TIPS: immediate central bank settlement
   → RT1: deferred settlement via TARGET2
7. Beneficiary PSP credits customer account
8. Confirmation sent back to payer's PSP
9. Both parties notified
Total time: ≤ 10 seconds
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Message Format | ISO 20022 (pacs.008, pacs.002) |
| Clearing | RT1 (EBA) or TIPS (ECB) |
| Settlement | Central bank money (TIPS) or deferred (RT1) |
| Max Amount | €100,000 per transaction |
| Availability | 24×7×365 |
| Response Timeout | 20 seconds (10s to PSP + processing) |
| Finality | Immediate, irrevocable |
| IBAN required | Yes |

---

## 🌍 Adoption Status (2025)

| Country | Status |
|---------|--------|
| Netherlands | High adoption (iDEAL integration) |
| Germany | Moderate (growing) |
| Italy | Mandatory for PSPs (EU regulation) |
| France | Growing |
| Spain | Growing |
| Non-Eurozone | Limited (currency conversion required) |

> **EU Regulation (2024)**: All PSPs in EU must offer SCT Inst at no extra cost vs regular SCT

---

## ⚖️ RT1 vs TIPS

| Feature | RT1 (EBA Clearing) | TIPS (ECB) |
|---------|-------------------|------------|
| Operator | EBA Clearing | European Central Bank |
| Settlement | Prefunded positions | Central bank money (reserves) |
| Settlement risk | Slight | Zero (central bank) |
| Reach | ~2,500 PSPs | All TARGET2 participants |
| Model | Private | Public infrastructure |

---

## ⚖️ SCT Inst vs SCT vs FedNow vs UPI

| Feature | SCT Inst | SCT | FedNow (US) | UPI (India) |
|---------|---------|-----|-------------|-------------|
| Speed | ≤ 10 sec | D+1 | ≤ 20 sec | ≤ 30 sec |
| Limit | €100K | No limit | $500K | ₹1L–5L |
| Settlement | Central bank | DNS | RTGS | Deferred net |
| Availability | 24×7 | Business days | 24×7 | 24×7 |
| Coverage | 36 SEPA countries | 36 SEPA countries | US | India |

---

## 🧠 Mental Model

```
SCT Inst = Eurozone's answer to UPI / FedNow

  Regular SEPA (SCT) = Overnight courier (arrives tomorrow)
  SEPA Instant (SCT Inst) = Same-city instant delivery (< 10 min)
  
  The ≤10 second rule = strict SLA enforced by regulation
```

---

## 🔗 Related Topics
- [SEPA](sepa.md)
- [TARGET2](target2.md)
- [FedNow](../02-us/fednow.md)
- [UPI](../01-india/upi.md)
- [ISO 20022](../05-infrastructure/iso-20022.md)
