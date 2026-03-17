# SWIFT — Society for Worldwide Interbank Financial Telecommunication

## 🧭 What is it
Global financial messaging network connecting 11,000+ institutions in 200+ countries. SWIFT moves instructions (not money) — the actual settlement happens via local RTGS systems.

---

## 🧱 Core Components

- **SWIFT Network** — Secure, standardized financial messaging infrastructure
- **BIC (Bank Identifier Code)** — Unique address for each financial institution
- **FIN (Financial Application)** — Core messaging service (MT messages)
- **SWIFT GPI** — Global Payments Innovation (tracking + speed improvements)
- **UETR** — Unique End-to-End Transaction Reference (GPI tracker ID)
- **SWIFTRef** — BIC directory, IBAN validation data
- **SWIFT for Corporates** — Direct corporate access to SWIFT network

---

## 🔄 How a Cross-Border Payment Works via SWIFT

```
Scenario: Person in India sends USD to USA

1. Sender's Indian Bank (ICICI) → SWIFT MT103 →
2. Correspondent Bank 1 (if no direct relationship) →
3. USD Correspondent in USA (JPMorgan BIC: CHASUS33) →
4. Routes via CHIPS/Fedwire to Beneficiary's US Bank →
5. Beneficiary's bank credits account

SWIFT carries the MESSAGE
CHIPS/Fedwire carries the MONEY (USD)
```

---

## ⚙️ Message Types (MT — Legacy)

| Message | Category | Description |
|---------|----------|-------------|
| MT103 | Customer Payments | Single customer credit transfer |
| MT202 | Financial Institution | Bank-to-bank payment |
| MT202 COV | Cover payment | Bank-to-bank covering an MT103 |
| MT700 | Documentary Credits | Letter of credit |
| MT300 | Treasury | FX confirmation |
| MT940/942 | Account Reporting | Statement messages |

---

## ⚙️ ISO 20022 Migration (2025)

```
Old: MT messages (fixed-length, limited data)
New: ISO 20022 MX messages (rich XML data)

Key MX messages:
  pacs.008 → replaces MT103 (customer credit transfer)
  pacs.009 → replaces MT202 (financial institution transfer)
  camt.053 → replaces MT940 (account statement)
  
Coexistence period: Nov 2022 → Nov 2025
Full cutover: November 2025
```

---

## 🌍 SWIFT GPI Features

| Feature | Description |
|---------|-------------|
| Tracking | Real-time status via UETR |
| Speed | >50% of payments credited in 30 min |
| Transparency | Full fee deduction visibility |
| Stop & Recall | Ability to recall pending payments |
| CLS (FX) | Continuous Linked Settlement integration |
| Pre-validation | IBAN/BIC validation before sending |

---

## ⚖️ SWIFT vs Alternatives

| Feature | SWIFT | Ripple/XRP | SEPA (EU) | FedNow (US) |
|---------|-------|-----------|-----------|-------------|
| Scope | Global (200+ countries) | Global | Europe only | US only |
| Speed | 1–5 days (GPI: min) | Seconds | D+1 / instant | Seconds |
| Settlement | Via local RTGS | On-chain | Via TARGET2 | Fed Reserve |
| Participants | 11,000+ banks | Growing | 36 countries | US FIs |
| Asset | Fiat (via banks) | XRP / USD | EUR | USD |
| Regulation | Established | Evolving | EU regulated | Fed regulated |

---

## ⚙️ SWIFT Infrastructure

```
SWIFT operates 3 data centers (USA, Netherlands, Switzerland):
  
  Member FI → Secure SWIFT Alliance Gateway → 
  SWIFT Network → 
  Recipient FI's SWIFT Gateway → Message Delivered
  
  Messages: Encrypted, authenticated (PKI)
  SLA: 99.999% availability
  Regulatory: SWIFT owned by member banks (cooperative)
```

---

## 🧠 Mental Model

```
SWIFT = Global postal service for bank instructions

  BIC = Zip code / Address
  MT103/pacs.008 = The letter (payment instruction)
  SWIFT network = Post office routing system
  RTGS/CHIPS = Actual delivery truck (money movement)
  
  SWIFT says "please transfer $1M to Bank B"
  Fedwire/CHIPS/TARGET2 actually moves the $1M
```

---

## 🔗 Related Topics
- [Correspondent Banking](correspondent-banking.md)
- [Forex](forex.md)
- [ISO 20022](../05-infrastructure/iso-20022.md)
- [Messaging Formats](../05-infrastructure/messaging-formats.md)
- [International Remittance](../06-use-cases/international-remittance.md)
