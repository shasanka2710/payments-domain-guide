# Key Players in Payments

## 🧭 What is it
A taxonomy of every entity involved in moving money — from payers to central banks — and their roles in the payment chain.

---

## 🧱 Player Categories

- **End Users**
  - Consumers (payers / payees)
  - Merchants
  - Corporates

- **Financial Institutions**
  - Issuing banks (payer's bank)
  - Acquiring banks (merchant's bank)
  - Correspondent banks (intermediaries in cross-border)

- **Payment Networks & Schemes**
  - Card networks (Visa, Mastercard, RuPay, UnionPay, Amex)
  - ACH networks (Nacha, NPCI, BACS)
  - Wire networks (Fedwire, CHAPS, TARGET2)

- **Infrastructure Operators**
  - Clearinghouses (EBA Clearing, TCH, ClearCorp)
  - Settlement agents (Central banks, CLS)

- **Service Providers**
  - Payment gateways (Stripe, Razorpay, Adyen)
  - Payment processors (Worldpay, FIS, TSYS)
  - PSPs (PayPal, Square, PhonePe, Paytm)
  - Neobanks (Revolut, Chime, Jupiter)

- **Regulators**
  - Central banks (RBI, Fed, ECB, BoE)
  - Financial regulators (SEBI, SEC, FCA)
  - Standards bodies (ISO, SWIFT, BIS)

---

## 🔄 Who Does What

```
CARD TRANSACTION FLOW:

Cardholder → Merchant → Acquirer → Card Network → Issuer
                                      ↑
                                 (Visa/MC/RuPay)

BANK TRANSFER FLOW:

Payer → Payer's Bank → Payment Rail → Beneficiary's Bank → Beneficiary
                       (UPI/ACH/SWIFT)
```

---

## ⚙️ Role Breakdown

| Player | Role | Examples |
|--------|------|----------|
| **Issuer** | Issues card/account to payer, authorizes transactions | HDFC, Chase, Barclays |
| **Acquirer** | Accepts payments on behalf of merchant | Worldpay, Paytm PG, Stripe |
| **Card Network** | Routes auth + clears between issuer & acquirer | Visa, Mastercard, RuPay |
| **PSP** | Aggregates multiple payment methods for merchants | Razorpay, Adyen, PayPal |
| **Gateway** | API layer between merchant and processor | Stripe, Braintree |
| **Processor** | Handles technical processing of transactions | FIS, TSYS, Worldpay |
| **Clearinghouse** | Nets obligations between banks | Nacha, EBA, NPCI |
| **Central Bank** | Final settlement, issues reserves | RBI, Fed, ECB |
| **Correspondent Bank** | Routes cross-border payments | HSBC, JPMorgan, Citi |

---

## 🌍 Regional Operators

| Region | Retail Network | RTGS Operator | Card Schemes |
|--------|---------------|---------------|--------------|
| India | NPCI (UPI, IMPS, NACH) | RBI (RTGS) | RuPay, Visa, MC |
| USA | Nacha (ACH), TCH (RTP) | Fed (Fedwire) | Visa, MC, Amex |
| Europe | EBA Clearing | ECB (TARGET2) | Visa, MC |
| UK | Pay.UK (Bacs, FPS) | BoE (CHAPS) | Visa, MC |

---

## ⚖️ PSP vs Gateway vs Processor

| Feature | PSP | Gateway | Processor |
|---------|-----|---------|-----------|
| Merchant-facing | ✅ | ✅ | ❌ |
| Multi-method support | ✅ | Partial | ❌ |
| Direct bank connection | ✅ | ❌ | ✅ |
| Settlement to merchant | ✅ | ❌ | Via acquirer |
| Examples | Razorpay, Stripe | Stripe, Authorize.Net | FIS, TSYS |

---

## 🧠 Mental Model

```
Think of payments like a TRADE ECOSYSTEM:

  Consumer = Buyer
  Merchant = Seller
  PSP/Gateway = Trading Platform (eBay/Amazon)
  Acquirer = Seller's Bank
  Issuer = Buyer's Bank
  Card Network = Stock Exchange (routing rules)
  Central Bank = Settlement Agent (clearing house)
```

---

## 🔗 Related Topics
- [Payments Landscape](payments-landscape.md)
- [Payment Gateways](../05-infrastructure/payment-gateways.md)
- [Payment Processors](../05-infrastructure/payment-processors.md)
- [Correspondent Banking](../04-cross-border/correspondent-banking.md)
