# Payment options for the Volt Padel Thailand website

Research notes, September 2026. Nothing here is implemented. Fees and rules change; confirm with each provider before signing up. This is not legal or tax advice.

## The real blocker is the legal setup, not the code

- Most Thai payment gateways (Stripe Thailand, Opn/Omise, GB Prime Pay, 2C2P, PayPal Thailand) pay out in THB to a Thai bank account and run business verification (KYC) against a Thai business or a Thai-resident individual.
- Foreigners generally cannot register a Thai sole proprietorship. Retail trade by a majority-foreign company falls under the Foreign Business Act (Foreign Business Licence or very high capital); the usual route is a Thai company with at least 51% Thai ownership. Working in Thailand also needs a work permit.
- Some Thai gateway users report that Opn asks foreigners for a work permit.
- Questions to settle with a Thai accountant or lawyer before choosing: Javi's visa and work-permit status; whether he has (or will create) a Thai company or a partner structure; whether a Spanish autónomo registration exists; which bank accounts are in his name.

## Current situation (September 2026)

- No Thai company.
- Not registered as self-employed in Spain, and no plan to register.
- Personal Thai bank accounts with PromptPay.
- Wise and Spanish bank accounts exist, but must not be assumed to be viable ecommerce merchant or settlement accounts.
- Thai visa and work permit in place. Whether the current work permit covers this separate commercial activity has **not** been legally verified.

## Questions that need professional confirmation in Thailand

1. Does the current work permit cover selling rackets as a separate commercial activity? If not, how can it be regularised?
2. Which legal structure fits: a Thai company with a Thai partner holding at least 51%, or another arrangement?
3. Can a foreign resident open Stripe Thailand (or a similar gateway) as an "Individual", and would that be compliant?
4. How must this income be declared and taxed?

## Realistic routes (none chosen)

| Route | What it is | Status |
|---|---|---|
| 1. Manual PromptPay or bank transfer to a personal Thai account | What happens today. On a website it would mean showing an amount and a QR, with manual (or slip-verified) confirmation | Technically possible with existing accounts. Not a gateway; confirmation is manual. The legal questions above apply to it as well |
| 2. Stripe Thailand as "Individual" | Stripe Thailand lists "Individual" as an account type | **Unverified.** Whether a foreign resident is eligible, and whether it would be compliant, is not confirmed. Not an available solution |
| 3. Thai company with a Thai partner (51%) | The standard structure; the company opens Stripe Thailand or Opn and gets full card and PromptPay checkout | Requires setting up a company and finding a partner |
| 4. An existing Thai business sells and collects payment, paying a commission | Similar to a reseller or agent arrangement | Depends on a partner and on negotiated terms |

Ruled out for now: Stripe Spain, Wise payment links and Spanish accounts as the merchant side, because they require a business registered outside Thailand. A company in Hong Kong or elsewhere would add cost without removing the Thai legal questions, since the stock, the seller and the deliveries are in Thailand, and it would still not offer PromptPay.

**The payment implementation is undecided.** None of these routes is the planned interim checkout.

## Two different things

- **Payment gateway / hosted checkout**: the customer pays on a secure page (card or PromptPay). The gateway confirms the payment automatically, the order is marked paid, refunds go through the dashboard.
- **Showing bank details or a PromptPay QR**: the customer transfers money themselves. Nothing confirms it automatically; someone checks the bank app or a transfer slip, and refunds are manual transfers.

## Options

| Option | Pays fully on the website | Cards | PromptPay | Automatic confirmation | Money lands in | Approx. fees | Main requirement | Integration with this static site |
|---|---|---|---|---|---|---|---|---|
| Stripe Thailand | Yes (hosted Checkout or Payment Links) | Visa and Mastercard, Thai debit cards; not Amex/JCB/UnionPay | Yes | Yes | THB, Thai bank | Thai cards 3.65% + ฿10; foreign cards 4.75% + ฿10 (+2% if FX); PromptPay 1.65% (+฿10 per refund); no monthly fee | Stripe account in Thailand; business registration number and tax ID requested; Thai bank account | Easiest: one Payment Link per racket, no backend. Webhooks optional (Cloudflare Pages Function) |
| Opn Payments (Omise) | Yes | Visa, Mastercard, JCB, Amex, UnionPay | Yes | Yes | THB, Thai bank | Cards 3.65%, PromptPay 1.65%, mobile banking ฿10 per payment; payout ฿20 (VAT treatment varies by source) | Thai business KYC; reports of work permit being required for foreigners; review can take weeks | Needs a small server function to create charges |
| GB Prime Pay, 2C2P, Pay Solutions and similar Thai gateways | Yes | Yes | Yes | Yes | THB, Thai bank | PromptPay about 1-1.65%, cards about 3-3.65% (quotes on request) | Thai business registration | Server function or plugin needed |
| Stripe Spain (Javi as Spanish autónomo) | Yes (Payment Links) | All major cards; Thai cards count as international | **No** (PromptPay needs a Thai Stripe account) | Yes | EUR, Spanish bank (a Wise EUR account also works) | International cards 3.15% + €0.25, +2% FX | Spanish business registration; the tax and legal position of selling goods delivered in Thailand needs advice | Easiest: Payment Links, no backend |
| Wise Business payment links | Per-order payment link, not a shop checkout | Cards, Apple Pay, Google Pay | No | Yes | Wise balance | 2.9% + US$0.30 (domestic cards), 4.2% + US$0.30 (foreign cards) | Business registered in the EEA, UK, US, SG and a few others; **not Thailand** | Links are created per order, so it doesn't fit a product page's buy button well |
| PayPal Thailand | Yes (PayPal buttons) | Via PayPal | No | Yes | THB, Thai bank (withdrawals take up to about 7 working days) | Rates not verified; 7% VAT on fees for business accounts | Thai PayPal account and Thai bank | JS button, no backend for simple use. Less common with Thai buyers |
| Manual PromptPay QR (no gateway) | No: the customer pays in their bank app | No | Yes | No; manual, or semi-automatic with slip-check services (EasySlip, SlipOK: free tiers about 100 slips/month) | The PromptPay account shown | No gateway fee | A PromptPay account; the same legal question about whose account receives business income | QR with the amount can be generated on the page; slip checking needs a small server function |
| Shopify or another full platform | Yes | Through a third-party gateway | Through a third-party gateway | Yes | Depends on the gateway | Monthly fee plus gateway fees | Shopify Payments is **not** available in Thailand, so a Thai gateway is still needed | Replaces this site; not needed for three products |

## How it would fit this site

The website can show proper "Buy V500 / V600 / V1000" actions now, as placeholders for a future checkout. What happens behind them is decided after the legal and payment setup is clear.

If a hosted checkout is chosen later (Stripe Payment Links, for example), the current static site would not need a platform or a backend:

`Buy V1000` → hosted secure checkout (card or PromptPay) → Stripe's receipt email to the customer and payment notification to Javi → Javi ships.

A small server function is only needed for extras such as automatic order emails or recording the coach referral code (Payment Links can carry a reference parameter for that).

## Refunds and confirmation

- Gateway card payments: confirmed instantly; refunds from the dashboard.
- Stripe PromptPay: confirmed instantly; for refunds Stripe emails the customer for the bank account the payment came from, then refunds automatically.
- Manual PromptPay or bank transfer: confirmation by checking the bank app or a slip; refunds are manual transfers.

## Sources

- Stripe Thailand pricing: https://stripe.com/th/pricing
- Stripe Thailand supported payment methods: https://support.stripe.com/questions/supported-payment-methods-currencies-and-businesses-for-stripe-accounts-in-thailand
- Stripe Thailand account information: https://support.stripe.com/questions/what-information-is-required-to-open-a-stripe-account-in-thailand
- Stripe PromptPay docs: https://docs.stripe.com/payments/promptpay
- Stripe Spain pricing: https://stripe.com/es/pricing
- Stripe Payment Links: https://stripe.com/payments/payment-links and https://docs.stripe.com/payment-links/post-payment
- Omise/Opn Thailand pricing: https://www.omise.co/en/pricing/thailand
- Thai gateway comparison: https://boldrails.com/blog/best-payment-gateways-thailand
- Wise card payments: https://wise.com/us/business/accept-card-payments/
- PayPal Thailand: https://www.paypal.com/th/webapps/mpp/merchant-fees?locale.x=en_TH
- Shopify in Thailand: https://www.xendit.co/en-th/blog/top-payment-gateway-for-shopify-ecommerce-brands-in-thailand-2026/
- Foreigners and online retail in Thailand: https://osos.boi.go.th/One-Stop/faq-group/96/Online-sale-business-in-Thailand/ and https://tilalegal.com/blog/company-registration-thailand-e-commerce-businesses-everything-you-need-know
- Slip verification: https://document.easyslip.com/en/guide/getting-started
