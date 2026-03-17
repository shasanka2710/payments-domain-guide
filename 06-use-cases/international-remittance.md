# International Remittance

## 🧭 What is it
Cross-border transfer of money by individuals — typically migrant workers sending money home (person-to-person across countries). A $700B+ annual market.

---

## 🧱 Core Components

- **Sender** — Individual in a foreign country (e.g., Indian worker in UAE)
- **Receiver** — Family member in home country (e.g., India)
- **Remittance Provider** — Wise, Western Union, Remitly, bank wire
- **FX Conversion** — Converting source currency to destination currency
- **Payment Rail** — SWIFT, ACH, IMPS, NEFT, local bank networks
- **Compliance** — KYC, AML, OFAC screening, source of funds

---

## 🔄 Remittance Flow (Modern Fintech Model)

```
Sender in USA wants to send $1,000 to India:

1. Sender logs into Wise/Remitly app
2. Enters: amount ($1,000 USD), receiver (Indian bank account)
3. Provider quotes exchange rate + fees upfront
4. Sender pays via ACH debit or bank transfer (USD)
5. Provider holds USD, converts to INR at spot rate
6. Provider's Indian entity (or partner bank) initiates IMPS/NEFT
7. Receiver's Indian bank account credited (₹83,000 approx)
8. Sender notified of delivery confirmation

Time: Minutes to hours (vs 2–5 days for traditional bank wire)
```

---

## 🌍 Top Remittance Corridors

| Corridor | Annual Volume | Key Players |
|----------|--------------|-------------|
| USA → India | ~$32B | Wise, Remitly, GPay, bank wires |
| USA → Mexico | ~$61B | Remitly, Western Union, Zelle |
| UAE → India | ~$20B | Exchange houses, banks |
| Saudi → India | ~$12B | Exchange houses |
| USA → Philippines | ~$10B | Remitly, Western Union |
| UK → India | ~$7B | Wise, bank transfers |

---

## ⚖️ Remittance Providers Comparison

| Provider | Model | Fee ($200 send) | FX Markup | Speed |
|----------|-------|----------------|-----------|-------|
| Traditional Bank | Correspondent | $20–$50 | 2–3% | 3–5 days |
| Western Union | Agent network | $5–$15 | 2–4% | Minutes to days |
| MoneyGram | Agent network | $5–$10 | 2–3% | Minutes to days |
| Wise | Local-to-local | $3–$6 | 0.3–0.7% | Minutes–1 day |
| Remitly | Fintech model | $3–$5 | 0.5–2% | Minutes–1 day |
| Revolut | App-based | $0–$3 | 0–1% | Instant–1 day |
| Crypto (USDC) | Blockchain | ~$0.50 | ~0% | Minutes |

---

## ⚙️ Wise's "Local-to-Local" Model

```
Key innovation: Avoid cross-border movement of money

Old model:
  USA → SWIFT → India  (expensive, slow)

Wise model:
  Sender → pays Wise USD account in USA
  Wise → pays from Wise INR account in India
  
  Wise holds pooled funds in both countries
  No actual cross-border transfer for each transaction!
  
  Net positions periodically rebalanced via wholesale FX
  
Result: Near mid-market rate, much lower fees
```

---

## ⚙️ Compliance Requirements

| Requirement | Detail |
|-------------|--------|
| KYC | ID verification for sender (passport, driving license) |
| AML | Transaction monitoring, SAR filing |
| OFAC / Sanctions | Screening against SDN and restricted lists |
| CTR | Currency Transaction Report (>$10K in US) |
| Source of Funds | Large transfers require documentation |
| FINTRAC (Canada) | Cross-border transfers >C$10K reported |
| FEMA (India) | Inward remittance reporting to RBI |

---

## 🧠 Mental Model

```
Remittance = Hawala modernized + regulated

Traditional Hawala:
  Person A gives money to Agent X in Country A
  Agent X messages Agent Y in Country B
  Agent Y pays equivalent to Person B
  No actual money crosses borders
  
Wise/Remitly: Same concept but:
  Regulated, licensed, tracked
  Technology-enabled (APIs, real-time FX)
  Compliant with AML/KYC
  Lower cost than traditional banks
```

---

## 🔗 Related Topics
- [SWIFT](../04-cross-border/swift.md)
- [Correspondent Banking](../04-cross-border/correspondent-banking.md)
- [Forex](../04-cross-border/forex.md)
- [UPI](../01-india/upi.md)
- [Key Players](../00-overview/key-players.md)
