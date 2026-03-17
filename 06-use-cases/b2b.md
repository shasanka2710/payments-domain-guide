# B2B — Business-to-Business Payments

## 🧭 What is it
Fund transfers between businesses — typically higher value, more complex, with rich remittance data requirements for reconciliation and accounting.

---

## 🧱 Core Components

- **ERP Integration** — SAP, Oracle, NetSuite initiate payment runs
- **Treasury Management System (TMS)** — Cash position, payment approval, netting
- **Payment Hub** — Centralized payment routing across rails and entities
- **Remittance Information** — Invoice references, PO numbers, payment purpose
- **Bank Connectivity** — SWIFT, Host-to-Host (H2H), EBICS, open banking APIs
- **Approval Workflow** — Multi-level authorization for large payments
- **Virtual Account Numbers** — For automated reconciliation of receivables

---

## 🔄 B2B Payment Flow

```
1. Supplier sends invoice to buyer (PDF/EDI/API)
2. Buyer's AP team approves invoice in ERP
3. ERP generates payment instruction
4. Payment Hub applies rules → selects rail (ACH/Wire/SEPA)
5. Payment file sent to bank (SWIFT/H2H/API)
6. Bank processes → routes via payment rail
7. Supplier's bank receives funds
8. Supplier's ERP matches payment to invoice (auto-reconcile)
9. Invoice marked "paid"
```

---

## 🌍 B2B Payment Rails by Type

| Use Case | Preferred Rail | Why |
|----------|---------------|-----|
| Domestic high-value | Wire (Fedwire/RTGS/CHAPS) | Immediate finality |
| Domestic payables | ACH (CCD/CTX) / SEPA CT | Low cost, bulk |
| International | SWIFT (MT103/pacs.008) | Global reach |
| USD cross-border | CHIPS | Netting, efficiency |
| Real-time B2B | FedNow / SEPA Inst / UPI | Urgent payments |
| Trade finance | LC, BG, documentary collections | Complex transactions |

---

## ⚙️ Remittance & Reconciliation

```
B2B problem: How does supplier know which invoices are paid?

Solutions:
  1. Structured remittance (ISO 20022 remittance block)
     → pacs.008 carries up to 9,999 invoice references
  
  2. Virtual Account Numbers (VAN)
     → Each payer gets unique account number
     → Bank auto-routes to correct AR
  
  3. EBICS (Germany/Europe)
     → Corporate-to-bank protocol for bulk files
  
  4. EDI/820 (US)
     → Separate remittance file via EDI alongside ACH
```

---

## ⚖️ B2B Payment Timing

| Payment Type | Timing | Rail | Notes |
|-------------|--------|------|-------|
| Payroll | Weekly/Bi-weekly | ACH PPD | Pre-funded |
| Vendor payments | Net-30/60/90 | ACH CCD / Wire | Based on terms |
| Tax payments | Deadline-driven | Wire | Urgent, EFTPS |
| International trade | Against docs | SWIFT/LC | Trade finance |
| Real-time B2B | On-demand | FedNow/RTP | Emerging |
| Recurring bills | Monthly | ACH / SEPA DD | Auto-debit |

---

## ⚖️ ACH CCD vs Wire vs SEPA (B2B)

| Feature | ACH CCD | Wire | SEPA CT |
|---------|---------|------|---------|
| Speed | T+1 | Immediate | D+1 |
| Cost | Low ($0.25–$1) | High ($15–$50) | Low |
| Limit | $1M (same-day) | No limit | No limit |
| Remittance | Limited (94 chars) | Limited | Rich (ISO 20022) |
| Reversibility | Up to 2 days | Irrevocable | Limited |
| Geography | USA only | Global | SEPA zone |

---

## 🧠 Mental Model

```
B2B payments = Corporate supply chain finance

  Invoice = Promise to pay
  Payment instruction = Order to pay
  Rail = The delivery mechanism
  Remittance = The packing slip (what's being paid)
  Reconciliation = Matching delivery to order
  
  B2B complexity > P2P:
    Multiple invoices per payment (bulk)
    Rich remittance data required
    Approval workflows
    Multi-currency, multi-entity
    ERP integration critical
```

---

## 🔗 Related Topics
- [ACH](../02-us/ach.md)
- [SEPA](../03-europe/sepa.md)
- [SWIFT](../04-cross-border/swift.md)
- [ISO 20022](../05-infrastructure/iso-20022.md)
- [Reconciliation](../07-architecture/reconciliation.md)
