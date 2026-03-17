# IMPS — Immediate Payment Service

## 🧭 What is it
24×7 real-time interbank electronic fund transfer system operated by NPCI (India). The underlying rails on which UPI operates.

---

## 🧱 Core Components

- **NPCI IMPS Switch** — Central routing and clearing hub
- **MMID (Mobile Money Identifier)** — 7-digit identifier linked to mobile + bank account
- **Mobile Number** — Primary identifier for P2P transfers
- **IFSC + Account** — Bank identifier for account-based transfers
- **Member Banks** — All RBI-licensed banks participating in IMPS

---

## 🔄 How it Works (Flow)

```
1. Payer initiates IMPS transfer via mobile banking / net banking
2. Payer's bank validates instruction (account, limits, fraud checks)
3. Payer's bank sends IMPS request to NPCI Switch
4. NPCI resolves beneficiary bank (via MMID or IFSC)
5. NPCI routes request to beneficiary's bank
6. Beneficiary's bank credits account
7. NPCI confirms success to payer's bank
8. Payer's bank sends confirmation to payer
Total time: < 30 seconds
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Message Format | ISO 8583 (card-like messaging) |
| Settlement Type | Deferred Net Settlement (4× daily via RBI) |
| Clearing | NPCI acts as clearinghouse |
| Transaction Limit | ₹5,00,000 per transaction |
| Availability | 24×7×365 |
| Identifiers | Mobile + MMID, IFSC + Account, Aadhaar |
| Channels | Mobile banking, net banking, ATM, SMS |
| Interoperability | Full across all member banks |

---

## 🌍 IMPS Use Cases

| Use Case | Description |
|----------|-------------|
| P2P transfers | Send money using mobile number |
| Account transfers | Send using IFSC + account number |
| UPI backend | UPI layer runs on top of IMPS rails |
| Merchant payments | Real-time merchant credit |
| Recharges | Mobile/DTH recharges via bank |

---

## ⚖️ IMPS vs UPI vs NEFT

| Feature | IMPS | UPI | NEFT |
|---------|------|-----|------|
| Built on | Direct NPCI rails | IMPS rails | RBI rails |
| Identifier | Mobile+MMID / IFSC | VPA | IFSC + Account |
| Initiation | Bank app | Any UPI app | Bank app |
| Speed | < 30 sec | < 30 sec | 30–60 min |
| Limit | ₹5L | ₹1L–5L | No limit |
| Interoperability | Bank-level | App-level (full) | Bank-level |
| API availability | Bank API | Open UPI API | Bank API |

---

## ⚙️ Settlement Mechanism

```
Intraday:
  All IMPS transactions accumulate at NPCI
  Net positions calculated per bank
  
Settlement windows (4× daily):
  8:00 AM → 11:00 AM → 2:00 PM → 5:00 PM
  
  NPCI sends settlement instructions to RBI
  RBI debits/credits banks' current accounts
```

---

## 🧠 Mental Model

```
IMPS = Highway; UPI = GPS navigation on that highway

  IMPS provides the road (rails)
  UPI adds smart routing, VPA resolution, 
  and app-layer interoperability on top

  You can travel on IMPS directly (bank app)
  or via UPI (any UPI app using the same road)
```

---

## 🔗 Related Topics
- [UPI](upi.md)
- [NEFT](neft.md)
- [RTGS](rtgs.md)
- [Clearing vs Settlement](../05-infrastructure/clearing-vs-settlement.md)
- [P2P Use Case](../06-use-cases/p2p.md)
