# BBPS — Bharat Bill Payment System

## 🧭 What is it
Interoperable, centralized, bill payment platform operated by NPCI (India) for recurring utility and biller payments.

---

## 🧱 Core Components

- **NPCI Bharat BillPay Ltd (NBBL)** — System operator
- **Bharat BillPay Operating Units (BBPOUs)** — Banks and non-banks that connect customers and billers
  - Customer Operating Units (COUs) — Consumer-facing agents
  - Biller Operating Units (BOUs) — Biller-facing agents
- **Central Unit (CU)** — NBBL's switching and routing hub
- **Billers** — Registered utility/service providers (electricity, water, telecom, etc.)
- **Agent Institutions** — Banks, telecom operators, business correspondents

---

## 🔄 How it Works (Flow)

```
1. Customer initiates bill payment via BBPS-enabled app/bank/agent
2. Customer Operating Unit (COU) receives request
3. COU sends bill fetch request to NBBL Central Unit
4. Central Unit routes to Biller Operating Unit (BOU)
5. BOU forwards to biller → biller returns bill details
6. Customer confirms payment amount
7. COU debits customer account (via UPI/NEFT/card/cash)
8. NBBL processes payment → routes to BOU
9. BOU confirms payment to biller system
10. Customer receives payment confirmation + receipt
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Message Format | ISO 20022-aligned / proprietary BBPS API |
| Settlement | T+1 net settlement via RBI |
| Clearing | NBBL acts as central clearinghouse |
| Availability | 24×7×365 |
| Channels | Banks, apps, agents, kiosks, ATMs |
| Bill Categories | Electricity, water, gas, telecom, DTH, insurance, loans, FASTag, etc. |
| Payment Modes | UPI, NEFT, debit card, credit card, prepaid, cash |

---

## 🌍 Biller Categories

| Category | Examples |
|----------|---------|
| Electricity | BESCOM, MSEB, TNEB |
| Water | Municipal corporations |
| Gas | IGL, MGL, Mahanagar Gas |
| Telecom | Airtel, Jio, BSNL |
| DTH | Tata Sky, Dish TV |
| Insurance | LIC, HDFC Life |
| Loan EMI | Banks, NBFCs |
| FASTag | NHAI, all tag issuers |
| Education | Schools, colleges |
| Housing | Society maintenance |

---

## ⚖️ BBPS vs Direct Biller Payment

| Feature | BBPS | Direct Biller Portal |
|---------|------|---------------------|
| Interoperability | ✅ Single interface | ❌ Biller-specific |
| Receipt | Standardized | Varies |
| Dispute resolution | BBPS framework | Biller-dependent |
| Channels | 10,000+ agent touchpoints | Online only |
| Coverage | All registered billers | Single biller |
| Reconciliation | Centralized | Manual |

---

## 🧠 Mental Model

```
BBPS = Universal TV Remote for bill payments

  Old way: Different remote for every TV (each biller had own portal)
  BBPS way: One remote (interface) controls all TVs (billers)
  
  Customer uses any BBPS app → pays any registered biller
  Like UPI for P2P, but BBPS for bill payments
```

---

## 🔗 Related Topics
- [UPI](upi.md)
- [NEFT](neft.md)
- [Subscriptions Use Case](../06-use-cases/subscriptions.md)
- [Payment Gateways](../05-infrastructure/payment-gateways.md)
- [Key Players](../00-overview/key-players.md)
