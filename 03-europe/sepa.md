# SEPA — Single Euro Payments Area

## 🧭 What is it
Integrated euro payment market covering 36 European countries. Enables cross-border euro payments to be as easy and cost-effective as domestic payments.

---

## 🧱 Core Components

- **EPC (European Payments Council)** — Scheme owner, sets rules
- **EBA Clearing** — Pan-European clearinghouse (STEP2)
- **TARGET2** — ECB's RTGS for high-value/bank-to-bank settlement
- **SEPA Schemes**
  - SCT (SEPA Credit Transfer) — Push payment
  - SDD (SEPA Direct Debit) — Pull payment
    - Core — Consumer direct debit
    - B2B — Business direct debit
  - SCT Inst (SEPA Instant Credit Transfer) — Real-time push

---

## 🔄 SEPA Credit Transfer Flow

```
1. Payer's bank initiates SCT instruction
2. Payer's bank sends XML (pain.001) to clearinghouse
3. EBA STEP2 (or bilateral exchange) clears the payment
4. Net positions calculated across participating banks
5. ECB TARGET2 settles net obligations
6. Beneficiary bank receives credit notification
7. Beneficiary account credited
Total time: D+1 (next business day)
```

---

## ⚙️ Technical Deep Dive

| Parameter | Detail |
|-----------|--------|
| Message Format | ISO 20022 XML (pain.001, pacs.008, pacs.003) |
| Settlement | DNS via TARGET2 |
| Clearing | EBA STEP2, bilateral, or domestic ACH |
| Credit Transfer | D+1 settlement |
| Direct Debit | D+1 (with 5-day pre-notification) |
| IBAN | International Bank Account Number (routing key) |
| BIC | Bank Identifier Code (required for some transactions) |
| Character Set | Latin alphabet (UTF-8 for data, ASCII for XML) |
| Amount Limit | SCT: No limit; SDD: No limit |

---

## 🌍 SEPA Coverage

| Type | Countries |
|------|-----------|
| Eurozone | 20 EU countries using EUR |
| Non-Euro EU | Denmark, Sweden, Poland, etc. |
| Non-EU EEA | Norway, Iceland, Liechtenstein |
| Other | UK (post-Brexit limited), Switzerland, San Marino, Monaco |
| **Total** | **36 countries** |

---

## ⚖️ SCT vs SDD vs SCT Inst

| Feature | SCT (Credit) | SDD (Debit) | SCT Inst |
|---------|-------------|-------------|----------|
| Direction | Push | Pull | Push |
| Timing | D+1 | D+1 | ≤ 10 sec |
| Authorization | Sender | Mandate from receiver | Sender |
| Use Case | Transfers, salaries | Subscriptions, bills | P2P, urgent |
| Reversal | Limited | Up to 8 weeks (consumer) | Limited |
| Limit | No limit | No limit | €100K |

---

## ⚙️ SEPA Direct Debit Mandate

```
SDD Mandate Flow:
  1. Creditor (biller) obtains signed mandate from debtor (customer)
  2. Mandate contains: creditor ID, debtor IBAN, frequency
  3. Creditor stores mandate + reference number (MRN)
  4. On due date: creditor submits debit instruction
  5. Debtor's bank debits account
  6. Customer has 8 weeks (CORE) to dispute unauthorized debit
```

---

## 🧠 Mental Model

```
SEPA = EU's version of a domestic payment system

  Before SEPA: Paying someone in Germany from France 
               = international wire (expensive, slow)
  After SEPA:  Same as paying a domestic French account
               (same process, same cost, same speed)
               
SEPA = European Union as one single payment market
```

---

## 🔗 Related Topics
- [SEPA Instant](sepa-instant.md)
- [TARGET2](target2.md)
- [ACH (US equivalent)](../02-us/ach.md)
- [ISO 20022](../05-infrastructure/iso-20022.md)
- [Subscriptions Use Case](../06-use-cases/subscriptions.md)
