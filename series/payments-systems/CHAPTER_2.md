# 2. Payments System Overview

## Payments System Models

- models
  - open loop
    - cards
    - ACH
    - wire transfers
    - check images
  - closed loop
    - PayPal
    - Western Union
  - hybrid

## Payments Systems in the United States

- Cash
- The checking system
- The card systems
- The ACH (Automated Clearing House) system
- The wire transfer systems
- faster payments / immediate funds transfer system
  - HK FPS run by HKICL

### "payments system" vs "payment network"

## Payments System Volumes

## Payments System Functions

- Processing
- Rules
- Brand

## Domains of Payments

- POS
- Remote commerce
- Bill payment
- P2P
- B2B
- C2B
- Income payment

## Payments Systems Flow

- Push
- Pull
  - Card network rules specify that merchants receiving this "yes" reply are covered for both insufficient funds and fraud risk
  - issuer tokenization to address the risk of data breaches

## Payments System Settlement

- net basis settlement
  - end-of-day settlement process in a batch
  -  it's the payments system's rules to specify how to handle the obligation derived from default of overdrafting
- gross basis settlement
  - end-of-day settlement

## The Virtual Systems

1. Two core United States payments systems, cash and checking, operate on a virtual basis.
   - cash is a push system

## Payments System Ownership and Regulation

- Bank-owned system
- Non-bank-owned system
- rules
  - public
    - Visa, Mastercard, NACHA
  - private
    - CHIPS for wire transfer
    - PIN debit card

## Economic Models for Payments Systems

- interchange
  - wire transfer
  - ACH (caveat: same day ACH do have it)
  - checking
- non-interchange
  - credit card      
- Float is the value earned from money held over a period of time.

## Risk Management

1. Major forms of risks

  - credit risk
  - fraud risk
  - liquidity risk

2. secondary forms of risks

  - Operational risk
  - Data security risk (PCI-DSS)
  - Reputation risk
  - Regulatory risk

## Comparing Payments Systems

Payments systems users consider it when evaluating new payments forms.

- Open or closed loop? 
- “Push” or “pull” payments? 
- [Net](https://corporatefinanceinstitute.com/resources/knowledge/finance/net-settlement/) or gross settlement? 
- Ownership—private vs. public; 
- bank owned or not? 
- Regulation—private rules and/or law/regulations? 
- Batch or real-time processing?
- Economic model—at par?; is there interchange between participants? 
- Which brand is used (and how)? 
- Does the payment system define “products”? 
- Do payment system rules determine: 
  - If payment is guaranteed or not? 
  - Timing of funding—before, at the time of, or after the transaction? 
- How are exceptions handled? 
- Fraud management procedures? 
- Dispute handling—is it handled as part of the payment system? 
- How are “on-us” transactions handled?

a basic set of important economic factors

- Risk pays—how do you assess and price for risk? 
- “Ad valorem” fees are better than flat fees 
- Cross-currency is lucrative 
- Processing demands scale to be viable 
- Businesses pay to be paid 
- Banked consumers don’t pay to pay; unbanked consumers generally do 
- Exception processing is expensive 
- Simplicity has economic value

Thick or Thin?

- Visa, Mastercard, American Express and PayPal are all examples of what we Visa, Mastercard, American Express and PayPal are all examples of what we call thick model network
- houses, the ACH, and PIN debit networks are all examples of this “thin model.”

## Cross-border Payments

As background, remember that payments systems, by definition, operate on an in-country basis: only banks that are chartered or licensed to operate in a country may join a payments system in that country. Because of this, transferring money between countries often requires two separate transactions, one in the sending country and one in the receiving country. This is true even if the transaction is denominated in the same currency in both systems.

[example of transaction with Exchange](https://github.com/omgnetwork/ewallet/blob/master/docs/design/transactions_and_entries.md)

examples:

- In reality, however, the global card network is keeping the complexity of the cross-border system “under the hood.”
- ACH-to-ACH service, Federal Reserve's Global ACH service
- SEPA (Single Euro Payments Area)

correspondent bank accounts -> 往来账户
- The global financial services messaging service [SWIFT](https://www.swift.com/) plays an important role in carrying instructions about these payments from one bank to another.
- [How the SWIFT System Works](https://www.investopedia.com/articles/personal-finance/050515/how-swift-system-works.asp)






