# CLAUDE.md

This file gives Claude Code (claude.ai/code) guidance when working in this repository.

## What this is

Landing page and sales channel for **Volt Padel Thailand**. Javi Tortajada is the exclusive distributor of Volt Padel (a premium Portuguese racket brand, voltpadel.com) in Thailand and Southeast Asia. The site handles direct orders outside Sterling Padel Bangkok.

## Business context

- Territory: Thailand (primary); ships to Singapore, Malaysia and Vietnam.
- Javi is based at Sterling Padel Bangkok (Sukhumvit Soi 24). Internal fact only: **Sterling must never appear on the public site** (see Public identity).
- Sales model: no online payment. The customer browses, messages on WhatsApp, and Javi confirms and arranges delivery.
- Payment: bank transfer or PromptPay to Javi's **personal** account. There is no registered company, so the site must never mention invoices, VAT/tax receipts or a company name ("Co., Ltd" etc.).
- Delivery times (confirmed): Bangkok 1–2 days (free), rest of Thailand 2–4 working days, SEA quoted case by case.
- Status: not published yet. Don't set up the domain or deploy until Javi says so.
- WhatsApp: +34 696 814 841 (`wa.me/34696814841`), Javi's current WhatsApp, where he has the Volt product catalogue set up and talks to customers directly. May be replaced later by a dedicated Volt business number or profile.
- Instagram: @javipadelbalance is Javi's personal account. Never link it from the public site. A dedicated Volt Thailand account may be added later.

## Public identity (requirement for the final site)

Two layers, deliberately separate (the same model as André's padelbangkok.com):

- **Website = Volt Padel Thailand.** The site presents the brand: the official Volt distributor in Thailand. It is not "Javi's Volt business" and is not built around a person.
- **WhatsApp = the sales conversation.** Every CTA leads to WhatsApp, currently Javi's own account with the Volt catalogue, where Javi handles the customer personally. That is fine: once the customer is in WhatsApp, talking to Javi is expected.

On the website:

- No personal names (no "Javi") in copy, CTAs, alt text or meta tags, and no brand story built around a person ("a real person who plays padel", "one person", "the distributor, Javi"). Write as the business: "we", "us", "Volt Padel Thailand".
- CTAs are brand-neutral: "Message us on WhatsApp", "Order on WhatsApp", "Contact us", "Order V600" and similar. Never "Message Javi".
- Payment copy: bank transfer or PromptPay; details are sent on WhatsApp once the order is confirmed. Don't say whose account it is.
- **Sterling Padel Bangkok never appears on the site**: no address, no pickup point, no demo rackets there, no "based at". Sales must go through the website and WhatsApp flow (a sale through Sterling pays Javi much less commission). If someone asks to try a racket, that is arranged privately on WhatsApp; the site may say "Want to try one first? Message us on WhatsApp" without naming a place.
- Don't show the +34 number as visible page content. Buttons and links still point to it behind the scenes.
- Don't link @javipadelbalance. Leave Instagram out until a Volt Thailand account exists.

Inside the WhatsApp flow:

- Pre-filled messages may stay neutral ("Hi! I'd like to order the Volt V600...") since the website doesn't name anyone; they must not mention Sterling. Javi replies personally from there.

Implementation:

- Keep the WhatsApp destination in one place: a single config value in the script. No hard-coded `wa.me/...` fallbacks or number text scattered through the HTML, so switching to a business number or profile is a one-line change.

Status: `index.html`, `index-b.html` and `index-c.html` predate this requirement and still contain personal references, Sterling mentions and the visible number. Apply it when the chosen version is finalised.

## Products and prices (source of truth)

| Model | Type      | Shape    | Price THB |
|-------|-----------|----------|-----------|
| V500  | Control   | Round    | ฿9,500    |
| V600  | Control   | Round    | ฿12,500   |
| V1000 | Power     | Diamond  | ฿13,500   |

Prices are in Thai baht only. They are higher than voltpadel.com's euro prices because they include import shipping and duties, so never show euro prices on the site. All prices include Bangkok delivery. SEA shipping is extra. Competitor reference: quad-sports.com top model at ฿16,669; Volt is positioned below that.

## Tech stack

- Static HTML/CSS/JS. No framework, no build step, no dependencies.
- Fonts: Google Fonts (Barlow Condensed for headings, Barlow for body), standing in for voltpadel.com's DIN Condensed / DIN 2014.
- Hosting: Cloudflare Pages (free tier). Domain: voltpadelthai.com or voltpadelthailand.com.

## Structure

- `index.html`: the whole site. CSS in `<style>`, JS in `<script>` at the end.
  - `RACKETS` array in the script: model data. The racket cards are rendered from it.
  - `WHATSAPP` constant: the number used for every WhatsApp link.
  - Page sections in order: nav, hero, shipping bar, rackets, how to order, about and coach teaser, FAQ, footer, WhatsApp FAB.
- `assets/`: logo and racket images, downloaded from the voltpadel.com Squarespace CDN. Never hotlink them.
  - `volt-padel-logo.png` is the original white logo; `volt-padel-logo-dark.png` is the recolored version for light backgrounds.
  - `v1000.png`, `v600.png`, `v500.png` are the current **v5** models (Volt 1000 v5, 600 v5, 500 v5). voltpadel.com also has older models (950, 900, 800…) with similar images. Don't mix them up: the model number is printed on the racket.
  - Specs on the cards come from the official v5 product pages: voltpadel.com/shop/products/p/volt-1000-v5, /volt-600-v5, /volt-500-v5.
- `README.md`: local preview and deployment steps.
- `index-b.html`: bold alternative design (Portuguese tile façade) for comparison. Not linked from the site. Once Javi picks a version, delete the other file before publishing.
- `index-c.html`: third direction (technical drawing sheet) for comparison. Uses `assets/c/` for self-hosted Barlow fonts and official Volt detail photos. Not linked from the site.
- `PRODUCT.md`, `.impeccable/`: product facts and design notes used by the design tooling.

## Commands

- Preview: `npx serve .` or open `index.html` directly.
- No lint or test setup yet. Before committing, check the page at 390px and 1440px widths and confirm there's no horizontal scroll.

## Design rules

- Match voltpadel.com: white/light backgrounds, minimal and premium. Headings are uppercase, light weight, with wide letter-spacing.
- Colors: ink `#111`, Volt yellow `#FAE100` (voltpadel.com's `hsl(54,100%,49%)`), cream `#F5F2E6`. Yellow is for fills and highlights only. Never use yellow text on white (not legible).
- Mobile-first. Keep a 16px side gutter on phones.

## Key behaviour

- Every WhatsApp link pre-fills a neutral message (no name, no Sterling). Racket buttons include the model and the price in ฿.
- Coach referral (prepared, not launched): `?ref=CODE` is saved in localStorage for 30 days and appended as `Coach code: CODE` to every WhatsApp message. The planned commission is 5% on sales traced to a code.

## What NOT to do

- No dark or black page backgrounds.
- No online payment, cart or checkout. WhatsApp only for now.
- The brand is VOLT, never "Bolt".
- Never invent prices. Use the table above.
- Show prices in Thai baht (฿) only. No euro prices or conversions.
- Never mention Sterling Padel Bangkok, show the personal +34 number as text, or link @javipadelbalance on the site.

## Working agreements

- Keep changes focused. Don't add unrelated refactors to a change.
- Don't commit secrets or `.env` files.
