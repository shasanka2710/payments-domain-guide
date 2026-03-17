# Reconciliation in Payment Systems

## 🧭 What is it
The process of matching internal transaction records against external bank/network records to ensure completeness, accuracy, and consistency — and resolving any discrepancies.

---

## 🧱 Core Components

- **Internal Ledger** — System's own record of all transactions
- **External Statement** — Bank/network settlement file (MT940, camt.053, ACH settlement report)
- **Matching Engine** — Algorithm that pairs internal vs external records
- **Exception Handler** — Workflow for unmatched / mismatched records
- **Nostro Reconciliation** — For banks: matching correspondent account statements
- **Position Reconciliation** — Ensuring net position matches settlement

---

## 🔄 Reconciliation Process

```
1. COLLECT:
   Internal: Pull all transactions from ledger DB for the period
   External: Receive bank statement (MT940/camt.053/CSV)

2. NORMALIZE:
   Standardize formats, currencies, timestamps, reference fields

3. MATCH:
   Automated 1:1 matching on: amount + reference + date
   Or 1:N matching for bulk payments with split entries

4. EXCEPTIONS:
   Unmatched internal → check if bank delayed (timing diff)
   Unmatched external → investigate (unknown credit/debit)
   Amount mismatch → fee deductions, FX differences
   
5. RESOLVE:
   Aging analysis → escalate to bank/network
   Adjust entries → accounting corrections
   
6. SIGN-OFF:
   Finance team approves reconciled ledger
   Report generated for audit trail
```

---

## ⚙️ Match Types

| Type | Description | Example |
|------|-------------|---------|
| 1:1 | One internal → one external record | Single wire transfer |
| 1:N | One internal → multiple external | Bulk payment with fee breakout |
| N:1 | Multiple internal → one external | Batch ACH file settled as one net |
| N:N | Multiple each side | End-of-day netting reconciliation |
| Unmatched Internal | In ledger, not in bank | Timing difference or failed txn |
| Unmatched External | In bank, not in ledger | Unknown debit, bank fee |

---

## ⚙️ Reconciliation Data Sources

| Source | Format | Frequency |
|--------|--------|-----------|
| SWIFT MT940/942 | Fixed text | Intraday / EOD |
| ISO 20022 camt.053 | XML | EOD statement |
| ACH settlement report | NACHA format | Post-settlement |
| Visa/MC clearing file | Proprietary | Daily |
| UPI NPCI settlement | CSV/SFTP | 4× daily |
| Core banking system | Internal API/DB | Real-time |
| Gateway reports | CSV / API | Daily |

---

## ⚖️ Reconciliation Challenges

| Challenge | Cause | Solution |
|-----------|-------|---------|
| Timing differences | Bank and system in different timezones | Grace period matching window |
| Duplicate transactions | Retry without idempotency | Idempotency keys + dedup |
| Missing references | Bank truncates reference fields | Regex matching, amount+date fallback |
| FX discrepancies | Rate difference between booking and settlement | FX tolerance bands |
| Fee deductions | Bank deducts fees from settlement | Gross-up reconciliation |
| Partial settlements | Network settles differently than expected | Manual exception workflow |

---

## 🧠 Mental Model

```
Reconciliation = Balancing your checkbook against bank statement

  Your checkbook (ledger) = What YOU think happened
  Bank statement = What BANK says happened
  
  Reconciliation = Compare the two, explain every difference
  
  For payments at scale:
    Your ledger = millions of transactions
    Bank statement = one net settlement figure
    
  Challenge: Map N transactions → 1 settlement line
  Solution: Structured references + matching algorithms
```

---

## 🔗 Related Topics
- [High-Level Architecture](high-level-architecture.md)
- [Idempotency](idempotency.md)
- [Retries](retries.md)
- [Clearing vs Settlement](../05-infrastructure/clearing-vs-settlement.md)
- [ISO 20022](../05-infrastructure/iso-20022.md)
