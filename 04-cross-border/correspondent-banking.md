# Correspondent Banking

## 🧭 What is it
A system where one bank (the correspondent) holds accounts and provides services for another bank (the respondent) in a different country/jurisdiction. The backbone of cross-border payments.

---

## 🧱 Core Concepts

- **Correspondent Bank** — Larger bank providing services (USD clearing, SWIFT access) to smaller banks
- **Respondent Bank** — Smaller/regional bank using correspondent's services
- **Nostro Account** — "Our money at your bank" — Account held by Bank A in foreign currency at Bank B
- **Vostro Account** — "Your money at our bank" — Bank B's view of the same account
- **Loro Account** — "Their account" — Third-party reference to a nostro/vostro relationship
- **Cover Payment** — Separate bank-to-bank payment (MT202) covering a customer payment (MT103)

---

## 🔄 How it Works (Cross-Border Flow)

```
Scenario: India → USA transfer

Sender (Mumbai)
  │ sends INR, wants USD delivered in USA
  ▼
ICICI Bank (India)
  │ has Nostro USD account at JPMorgan NY
  │ sends SWIFT MT103 (customer instruction)
  │ sends SWIFT MT202 COV (cover payment)
  ▼
JPMorgan Chase (USA — Correspondent)
  │ verifies SWIFT message
  │ debits ICICI's Nostro account
  │ routes via CHIPS/Fedwire
  ▼
Wells Fargo (USA — Beneficiary Bank)
  │ receives funds
  ▼
Beneficiary receives USD
```

---

## ⚙️ Nostro / Vostro Accounting

```
ICICI Bank's perspective:
  "Our USD account at JPMorgan" = NOSTRO account
  Balance represents pre-funded USD liquidity

JPMorgan's perspective:
  "ICICI's account held with us" = VOSTRO account
  JPMorgan manages this account for ICICI

Third-bank perspective:
  "ICICI's account at JPMorgan" = LORO account
```

---

## 🌍 Global Correspondent Landscape

| Corridor | Key Correspondents | Notes |
|----------|-------------------|-------|
| USD clearing | JPMorgan, Citi, BofA, BONY | CHIPS participants |
| EUR clearing | Deutsche Bank, BNP Paribas, Société Générale | TARGET2 access |
| GBP clearing | HSBC, Barclays, Lloyds | CHAPS access |
| JPY clearing | MUFG, Sumitomo, Mizuho | BOJ-NET access |
| INR (offshore) | SBI, ICICI, Axis (international branches) | RBI regulated |

---

## ⚖️ Correspondent Banking vs Alternatives

| Feature | Correspondent | Fintech (Wise/Remitly) | CBDC Networks |
|---------|--------------|----------------------|---------------|
| Infrastructure | Existing banking | Internal matching | New rails |
| Cost | High (multiple fees) | Low | Low (theoretical) |
| Speed | 1–5 days | 1–2 days | Seconds (future) |
| Transparency | Low | High | High |
| Regulation | Heavily regulated | Regulated (lighter) | Evolving |
| Reliability | High | Medium-High | Unproven at scale |

---

## ⚙️ De-risking Trend

```
Problem: Many large banks closing correspondent relationships

Reasons:
  → AML/KYC compliance costs too high for small corridors
  → FATF blacklisting pressure
  → Low profitability in some corridors

Impact:
  → Smaller/frontier markets lose USD access
  → Longer payment chains → higher costs → slower
  
Solutions being explored:
  → Multilateral netting platforms
  → CBDC corridors (mBridge, Project Dunbar)
  → Crypto rails
```

---

## 🧠 Mental Model

```
Correspondent Banking = Banking's franchise model

  Small regional bank = franchise owner
  Large correspondent bank = franchisor
  
  Franchisee uses franchisor's brand (SWIFT network access),
  infrastructure (Nostro account), and services
  to serve customers beyond their own capabilities
  
  Nostro = Franchise's cash register (pre-funded)
```

---

## 🔗 Related Topics
- [SWIFT](swift.md)
- [Forex](forex.md)
- [SWIFT in US Context](../02-us/swift-us.md)
- [International Remittance](../06-use-cases/international-remittance.md)
- [ISO 20022](../05-infrastructure/iso-20022.md)
