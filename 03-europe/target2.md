# TARGET2 — Trans-European Automated Real-time Gross Settlement Express Transfer

## 🧭 What is it
The Eurosystem's RTGS system operated by the ECB. Processes high-value euro payments between banks in real-time, using central bank money.

---

## 🧱 Core Components

- **ECB + 4 Central Banks** — Co-operate and operate the system (Deutsche Bundesbank, Banca d'Italia, Banque de France, Banco de España)
- **SSP (Single Shared Platform)** — Core technical infrastructure
- **PM (Payments Module)** — Core payment processing
- **HAM (Home Accounting Module)** — For banks not in SSP
- **RM (Reserve Management Module)** — Minimum reserve tracking
- **Information & Control Module** — Liquidity management tools

---

## 🔄 How it Works (Flow)

```
1. Bank A submits euro payment instruction to TARGET2
2. TARGET2 checks: Does Bank A have sufficient balance in its PM account?
3a. YES → Immediately debit Bank A's account
          → Immediately credit Bank B's account
          → Send confirmation to both banks
          → SETTLEMENT IS FINAL AND IRREVOCABLE
3b. NO  → Enter queue (FIFO or priority-based)
          → Await incoming funds or intraday credit
4. End of day: remaining queued transactions cancelled or settled via marginal lending
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Message Format | ISO 20022 (migrated from SWIFT MT in 2023) |
| Settlement | Real-time Gross Settlement (RTGS) |
| Currency | EUR only |
| Operating Hours | 7:00–18:00 CET (Mon–Fri) |
| RTGS Finality | Immediate and irrevocable |
| Intraday Liquidity | Auto-collateralized repo (via ECB) |
| Minimum Balance | Banks must hold min reserves |
| Volume | ~350,000 transactions/day, ~€1.7T/day |

---

## 🌍 TARGET2 in the European Ecosystem

```
ECB/Eurosystem Architecture:

  TARGET2 (RTGS — high value, bank-to-bank)
      ↑
      │ settlement
      ▼
  STEP2 / RT1 (EBA retail clearing) ←→ National ACH systems
      ↑
      │ settlement instructions
      ▼
  Commercial Banks ←→ Customers
```

---

## ⚖️ TARGET2 vs TIPS vs STEP2

| Feature | TARGET2 | TIPS | STEP2 |
|---------|---------|------|-------|
| Type | RTGS (high-value) | Instant retail settlement | Retail batch clearing |
| Operator | ECB | ECB | EBA Clearing |
| Settlement | Real-time gross | Real-time (24×7) | Net (deferred) |
| Amount | No limit | ≤ €100K | ≤ standard retail |
| Availability | Business hours | 24×7×365 | Business days |
| Currency | EUR | EUR | EUR |

---

## ⚖️ Global RTGS Comparison

| System | Region | Operator | Settlement |
|--------|--------|---------|------------|
| TARGET2 | Eurozone | ECB | RTGS |
| Fedwire | USA | Fed Reserve | RTGS |
| RTGS | India | RBI | RTGS |
| CHAPS | UK | Bank of England | RTGS |
| MEPS+ | Singapore | MAS | RTGS |

---

## ⚙️ TARGET2 → T2 Migration (2023)

```
Old: TARGET2 (separate RTGS)
New: T2 (consolidated platform)
  → RTGS component (replaces TARGET2)
  → CLM (Central Liquidity Management) — unified liquidity
  → ISO 20022 messaging throughout
  → Better real-time liquidity overview
```

---

## 🧠 Mental Model

```
TARGET2 = ECB's central vault where banks' euro reserves sit

  Each bank in the Eurozone has an account at ECB/NCB
  TARGET2 moves balances between these accounts
  Like RTGS in India (RBI) or Fedwire in US (Federal Reserve)
  
  All retail payments ultimately settle here
  (SEPA → STEP2 → nets → TARGET2 for final settlement)
```

---

## 🔗 Related Topics
- [SEPA](sepa.md)
- [SEPA Instant](sepa-instant.md)
- [RTGS (India)](../01-india/rtgs.md)
- [Wire Transfers (US)](../02-us/wire.md)
- [Clearing vs Settlement](../05-infrastructure/clearing-vs-settlement.md)
