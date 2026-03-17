# Clearing vs Settlement

## 🧭 What is it
Two distinct but sequential stages in every payment:
- **Clearing** = calculating who owes what to whom
- **Settlement** = the actual transfer of funds to discharge those obligations

---

## 🧱 Core Concepts

### Clearing
- Exchange of payment instructions between banks
- Calculation of net positions
- Validation, routing, and confirmation of messages
- Performed by clearinghouses (NPCI, EBA, Nacha, CHIPS)

### Settlement
- Actual transfer of funds between banks
- Performed in central bank money (reserve accounts)
- Operated by central banks (RBI, Fed, ECB)
- Two types: Gross (individual) or Net (batched)

---

## 🔄 Flow

```
PAYMENT INSTRUCTION
  │
  ▼
CLEARING PHASE:
  → Message exchange between banks
  → Validation (format, funds check)
  → Netting (calculating net positions)
  → Settlement obligation created
  │
  ▼
SETTLEMENT PHASE:
  → Central bank debits sender's bank reserve account
  → Central bank credits receiver's bank reserve account
  → Final, irrevocable transfer complete
  │
  ▼
POST-SETTLEMENT:
  → Banks credit/debit customer accounts
  → Reconciliation
  → Reporting
```

---

## ⚙️ Gross vs Net Settlement

### Gross Settlement (RTGS)
```
Transaction 1: Bank A → Bank B: $100M  → SETTLE IMMEDIATELY
Transaction 2: Bank C → Bank A: $80M   → SETTLE IMMEDIATELY  
Transaction 3: Bank B → Bank C: $50M   → SETTLE IMMEDIATELY

Total settled: $230M gross
```

### Net Settlement (ACH/SEPA)
```
End of day netting:
  Bank A owes Bank B: $100M
  Bank B owes Bank A: $60M
  Net: Bank A pays Bank B $40M

Total settled: $40M (vs $160M gross)
Liquidity savings: 75%
```

---

## ⚙️ Technical Comparison

| Feature | Gross Settlement (RTGS) | Net Settlement (DNS) |
|---------|------------------------|---------------------|
| Settlement timing | Real-time (per transaction) | Deferred (batch) |
| Liquidity needed | High (full transaction value) | Low (net amount only) |
| Credit risk | Zero (immediate finality) | Intraday credit exposure |
| Settlement risk | Minimal | Systemic risk if bank fails |
| Cost | Higher | Lower |
| Systems | Fedwire, RTGS, TARGET2, CHAPS | ACH, NEFT, SEPA, BACS |
| Use case | High-value, urgent | Retail, bulk, payroll |

---

## 🌍 Settlement Agents by Region

| Region | Gross Settlement | Net Settlement Clearing |
|--------|-----------------|------------------------|
| India | RBI (RTGS) | NPCI (UPI, IMPS, NACH) |
| USA | Federal Reserve (Fedwire) | Nacha, TCH (ACH, RTP) |
| Eurozone | ECB (TARGET2/T2) | EBA Clearing (STEP2) |
| UK | Bank of England (CHAPS) | Pay.UK (Bacs, FPS) |

---

## ⚖️ Settlement Finality

| Model | Finality | Risk |
|-------|----------|------|
| RTGS | Immediate upon settlement | None (central bank money) |
| DNS | End of settlement cycle | Unwind risk if participant fails |
| CLS (FX) | PVP — simultaneous | Minimal |
| Blockchain | After confirmation blocks | Probabilistic |

---

## 🧠 Mental Model

```
Clearing = Scorekeeping during a game
Settlement = Paying up after the game ends

Gross = Each point scored = immediate cash exchange
Net   = All scores totaled at end = one net payment

RTGS: Each transaction individually settled as it happens
ACH:  All transactions accumulated → settle net difference once
```

---

## 🔗 Related Topics
- [Payment Lifecycle](../00-overview/payment-lifecycle.md)
- [ISO 20022](iso-20022.md)
- [RTGS (India)](../01-india/rtgs.md)
- [TARGET2](../03-europe/target2.md)
- [Wire Transfers (US)](../02-us/wire.md)
