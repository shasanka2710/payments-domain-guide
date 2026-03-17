# Payment Messaging Formats

## 🧭 What is it
The technical standards and message formats used to communicate payment instructions between financial institutions, gateways, and networks.

---

## 🧱 Format Families

- **ISO 20022** — Modern XML/JSON structured messages (current standard)
- **SWIFT MT** — Legacy fixed-format messages (being phased out)
- **ISO 8583** — Card authorization and transaction messages
- **NACHA** — US ACH file format
- **EDIFACT / X12** — Trade and B2B data interchange

---

## ⚙️ ISO 8583 (Card Payments)

```
Structure: Fixed-length bit-mapped message

  MTI (Message Type Indicator) — 4 digits
    1xxx = Authorization
    2xxx = Financial
    4xxx = Reversal
    8xxx = Network management

  Bitmap — 64 or 128 bits, each bit = data element present
  Data Elements — Up to 128 fields

Common fields (Data Elements):
  DE2  = Primary Account Number (PAN)
  DE3  = Processing Code
  DE4  = Transaction Amount
  DE7  = Transmission Date/Time
  DE11 = Systems Trace Audit Number (STAN)
  DE12 = Local Transaction Time
  DE22 = POS Entry Mode
  DE35 = Track 2 Data (magnetic stripe)
  DE37 = Retrieval Reference Number (RRN)
  DE39 = Response Code (00=approved, 51=insufficient funds, etc.)
  DE41 = Terminal ID
  DE42 = Merchant ID
  DE49 = Currency Code
```

---

## ⚙️ SWIFT MT Messages (Legacy)

```
Format: Fixed-length text blocks

Structure:
  {1:} Basic Header Block    — sender BIC, session info
  {2:} Application Header    — message type, receiver BIC
  {3:} User Header           — optional fields (priority, etc.)
  {4:} Text Block            — actual message content
  {5:} Trailer Block         — authentication, checksum

Key MT messages:
  MT103 — Customer Credit Transfer
  MT202 — General Financial Institution Transfer
  MT700 — Issue of Documentary Credit (LC)
  MT940 — Customer Statement Message
  MT950 — Statement Message (bank-to-bank)
```

---

## ⚙️ ISO 20022 MX Messages

```
Format: XML with defined schema (XSD)

Example: pacs.008 (Customer Credit Transfer)
<Document>
  <FIToFICstmrCdtTrf>
    <GrpHdr>
      <MsgId>MSG123456</MsgId>
      <CreDtTm>2025-01-15T10:30:00</CreDtTm>
    </GrpHdr>
    <CdtTrfTxInf>
      <IntrBkSttlmAmt Ccy="USD">1000.00</IntrBkSttlmAmt>
      <Cdtr><Nm>John Doe</Nm></Cdtr>
      <CdtrAcct><Id><IBAN>US33...</IBAN></Id></CdtrAcct>
    </CdtTrfTxInf>
  </FIToFICstmrCdtTrf>
</Document>
```

---

## ⚙️ NACHA File Format (US ACH)

```
Structure: Fixed-width ASCII records

Record types:
  1 = File Header Record
  5 = Batch Header Record
  6 = Entry Detail Record (actual transaction)
  7 = Addenda Record (remittance info)
  8 = Batch Control Record
  9 = File Control Record

Entry Detail (94 chars):
  Record Type (1) + Transaction Code (2) + 
  Routing Number (9) + Account Number (17) +
  Amount (10) + Individual ID (15) + Name (22) +
  Discretionary Data (2) + Addenda Indicator (1) +
  Trace Number (15)
```

---

## ⚖️ Format Comparison

| Feature | ISO 8583 | SWIFT MT | ISO 20022 | NACHA |
|---------|---------|---------|-----------|-------|
| Type | Binary/fixed | Text/fixed | XML/structured | Fixed ASCII |
| Use case | Card auth | Cross-border messaging | All payments | US ACH batch |
| Data richness | Medium | Limited | Rich | Limited |
| Extensibility | Low | Low | High | Low |
| Adoption | Global (cards) | 200+ countries | Rapidly growing | US only |
| STP capability | High (card) | Medium | Very high | Medium |
| Future | Evolving | Sunset by 2025 | Future standard | Evolving |

---

## 🧠 Mental Model

```
Messaging formats = Languages spoken between banks

  ISO 8583  = Card-specific shorthand (fast, efficient, limited)
  SWIFT MT  = Old English (everyone knows it, but limited vocab)
  ISO 20022 = Modern English (rich, expressive, understood globally)
  NACHA     = US-only dialect (domestic ACH only)
```

---

## 🔗 Related Topics
- [ISO 20022](iso-20022.md)
- [SWIFT](../04-cross-border/swift.md)
- [ACH](../02-us/ach.md)
- [Payment Gateways](payment-gateways.md)
- [High-Level Architecture](../07-architecture/high-level-architecture.md)
