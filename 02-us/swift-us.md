# SWIFT in the US Context

## 🧭 What is it
SWIFT (Society for Worldwide Interbank Financial Telecommunication) as used by US financial institutions for cross-border messaging, correspondent banking, and international wire instructions.

---

## 🧱 How US Banks Use SWIFT

- **Correspondent Banking** — US banks as intermediaries for foreign banks
- **SWIFT BIC (Bank Identifier Code)** — 8–11 character address for US banks
  - e.g., `CHASUS33` = JPMorgan Chase, New York
  - e.g., `WFBIUS6S` = Wells Fargo, San Francisco
- **Nostro Accounts** — USD accounts held at US banks by foreign banks
- **CHIPS Integration** — SWIFT messages settle via CHIPS for USD
- **Fed Integration** — SWIFT messages can trigger Fedwire transfers

---

## 🔄 Inbound International Wire to US (Flow)

```
Foreign Bank
  │
  ▼
Sends SWIFT MT103 (or ISO 20022 pacs.008) message
  │
  ▼
US Correspondent Bank (e.g., JPMorgan, Citi)
  │  ← checks SWIFT message, resolves beneficiary bank
  ▼
Routes via CHIPS or Fedwire to beneficiary's bank
  │
  ▼
Beneficiary's US Bank
  │
  ▼
Credits Customer Account
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Network | SWIFT FIN / SWIFT GPI |
| Message Format | MT103 (legacy) / ISO 20022 pacs.008 (migration 2025) |
| Settlement | Via CHIPS (USD clearing) or Fedwire |
| BIC Structure | 4-char bank + 2-char country + 2-char location + 3-char branch |
| GPI Tracker | End-to-end payment tracking (UETR) |
| OFAC Compliance | All US cross-border payments screened |

---

## 🌍 Major US SWIFT Correspondents

| Bank | BIC | Role |
|------|-----|------|
| JPMorgan Chase | CHASUS33 | Top USD correspondent |
| Citibank | CITIUS33 | Major USD clearer |
| Bank of America | BOFAUS3N | Major correspondent |
| Wells Fargo | WFBIUS6S | Regional correspondent |
| The Bank of New York | IRVTUS3N | Custody & clearing |

---

## ⚖️ SWIFT vs FedNow vs CHIPS

| Feature | SWIFT | CHIPS | FedNow |
|---------|-------|-------|--------|
| Purpose | Messaging (not settlement) | USD clearing+settlement | Domestic instant payments |
| Scope | Global cross-border | Domestic USD | US domestic |
| Settlement | Via local RTGS (Fedwire) | Direct + Fedwire | Fed Reserve (real-time) |
| Speed | 1–5 days (traditional) / GPI faster | Same day | < 20 sec |
| Message | MT / ISO 20022 | ISO 20022 | ISO 20022 |

---

## ⚙️ OFAC & Sanctions Screening

```
All US cross-border payments MUST:
  1. Screen sender + receiver against OFAC SDN list
  2. Screen intermediary banks
  3. Block + report any matches
  4. Hold pending transactions for review
  
Regulatory basis: Bank Secrecy Act (BSA), USA PATRIOT Act
Penalty risk: Massive fines (BNP Paribas: $8.9B in 2014)
```

---

## 🧠 Mental Model

```
SWIFT in US = International postal address + tracking system

  BIC = Zip code for the bank
  SWIFT message = The letter/package
  CHIPS/Fedwire = The actual delivery truck (money moves here)
  
  SWIFT doesn't move money — it moves instructions
  The actual USD moves via CHIPS or Fedwire
```

---

## 🔗 Related Topics
- [SWIFT (Global)](../04-cross-border/swift.md)
- [Wire Transfers](wire.md)
- [Correspondent Banking](../04-cross-border/correspondent-banking.md)
- [ISO 20022](../05-infrastructure/iso-20022.md)
- [International Remittance](../06-use-cases/international-remittance.md)
