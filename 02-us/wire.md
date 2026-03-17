# Wire Transfers — US (Fedwire & CHIPS)

## 🧭 What is it
Real-time, high-value, irrevocable fund transfers between US banks via Fedwire (Federal Reserve) or CHIPS (The Clearing House). Used for large institutional and B2B payments.

---

## 🧱 Core Components

### Fedwire Funds Service
- **Operator** — Federal Reserve Banks
- **Participants** — Depository institutions with Fed accounts
- **Settlement** — Real-time gross in Fed Reserve books
- **SWIFT Integration** — International wire routing via SWIFT

### CHIPS (Clearing House Interbank Payments System)
- **Operator** — The Clearing House (TCH)
- **Participants** — ~50 large financial institutions
- **Settlement** — Multilateral netting + final settlement via Fedwire
- **Volume** — Processes ~95% of cross-border USD transactions

---

## 🔄 How it Works (Fedwire Flow)

```
1. Sending bank initiates wire instruction
2. Bank submits message to Fedwire system
3. Fed verifies sending bank has sufficient reserves
4. Fed immediately debits sender's reserve account
5. Fed immediately credits receiver's reserve account
6. Receiver bank is notified → credits customer account
7. Transaction is FINAL and IRREVOCABLE
Total time: Minutes (during business hours)
```

---

## 🔄 CHIPS Flow (Netting Model)

```
1. Banks submit payment instructions to CHIPS queue
2. CHIPS algorithm continuously attempts to net multilaterally
3. Matched/netted transactions settled simultaneously
4. End of day: remaining queue settled via Fedwire
5. Net settlement reduces liquidity needs by ~95%
```

---

## ⚙️ Technical Deep Dive

| Parameter | Fedwire | CHIPS |
|-----------|---------|-------|
| Message Format | Fedwire proprietary / ISO 20022 (2023+) | ISO 20022 |
| Settlement | Real-time Gross | Multilateral Net + Fedwire |
| Availability | 21+ hours/day (Mon–Fri) | Business hours |
| Min Amount | No minimum | No minimum |
| Max Amount | No limit | No limit |
| Finality | Immediate | End of cycle |
| Cost | $0.83–$1.00 (Fed rate) | Varies |
| Participants | ~10,000 institutions | ~50 large banks |

---

## 🌍 Wire in Global Context

| System | Country | Operator | Type |
|--------|---------|---------|------|
| Fedwire | USA | Federal Reserve | RTGS |
| CHIPS | USA | The Clearing House | DNS + Fedwire |
| CHAPS | UK | Bank of England | RTGS |
| TARGET2 | Eurozone | ECB | RTGS |
| RTGS | India | RBI | RTGS |

---

## ⚖️ Fedwire vs CHIPS

| Feature | Fedwire | CHIPS |
|---------|---------|-------|
| Settlement | Gross (immediate) | Net (end of day) |
| Liquidity | Higher need | Lower need (~5%) |
| Participants | ~10,000 | ~50 |
| Coverage | Domestic focus | Cross-border USD |
| Cost | Lower volume fees | Netting saves costs |
| Finality | Immediate | End of cycle |

---

## 🧠 Mental Model

```
Fedwire = Federal Express (each package delivered individually, instantly)

CHIPS = Carpooling system (group similar destinations, 
        deliver together, sharing costs and liquidity)
        
Both ultimately use Fed's reserve accounts as the 
"vault" where actual money sits.
```

---

## 🔗 Related Topics
- [ACH](ach.md)
- [FedNow](fednow.md)
- [SWIFT (Cross-border)](../04-cross-border/swift.md)
- [RTGS India](../01-india/rtgs.md)
- [TARGET2](../03-europe/target2.md)
