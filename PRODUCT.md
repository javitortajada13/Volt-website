# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

Static HTML/CSS/JS, no framework (confirmed by Javi). Hosting: Cloudflare Pages.

## Users

Padel players in Thailand, mostly Bangkok: expats and Thai players at club level who want a premium racket and are comparing options, often on their phone at or around the club. Secondary: players in Singapore, Malaysia and Vietnam. Future audience: padel coaches who refer their players (coach program not launched yet).

## Product Purpose

Direct sales channel for Volt Padel rackets in Thailand and Southeast Asia, presented as Volt Padel Thailand, the official distributor (run by Javi Tortajada, who is not named on the site). Target: visitors discover, compare, choose and pay on the website (payment architecture still undecided). WhatsApp Business is a separate complementary channel where Javi advises and sells personally. Success is a completed purchase, on the site or through WhatsApp.

## Positioning

The only local source of Volt Padel, a premium Portuguese brand, in Thailand. Direct WhatsApp ordering with a Volt catalogue, free Bangkok delivery, and trials arranged privately on request. Priced below the competitor reference (quad-sports.com top model at ฿16,669).

## Operating Context

- Ordering today: WhatsApp Business "Volt Padel Thailand" (+66 97 302 5462). Target: checkout on the website; WhatsApp stays as a complementary channel. Payment options are compared in docs/payment-options.md; nothing implemented yet.
- Payment: bank transfer or PromptPay to Javi's personal account. There is no registered company.
- Delivery: Bangkok 1–2 days (free), rest of Thailand 2–4 working days, SEA quoted per order.
- Trying a racket: arranged privately on WhatsApp on request. No venue is named on the site.
- Sterling Padel Bangkok is Javi's base but must never appear on the site (sales there go through another channel with lower commission).

## Capabilities and Constraints

- Models (current v5 range only): V1000 (Power, Diamond, ฿13,500), V600 (Control, Round, ฿12,500), V500 (Control, Round, ฿9,500). Specs come from the official voltpadel.com v5 product pages.
- Prices in Thai baht only. They include import costs and Bangkok delivery. Never show euros.
- WhatsApp links pre-fill the model and price. A `?ref=CODE` coach referral code is carried into messages (prepared, not live).
- Never mention invoices, VAT, tax receipts or a company name.
- Not published yet.

## Brand Commitments

- Two channels: the website is Volt Padel Thailand, potentially full ecommerce (no personal names, no story built around a person, neutral CTAs); WhatsApp Business is a complementary channel where Javi handles customers personally with the Volt catalogue. André's WhatsApp is the reference for that channel only, not for the website's payment flow. No Sterling, no visible +34 number, no personal Instagram on the site. The WhatsApp destination lives in one config value.
- The brand is VOLT (never "Bolt"). Tagline "Unleash the tension" and the "Choose your voltage" phrase come from Volt's own site.
- Look must stay close to voltpadel.com: white/light backgrounds (no dark or black page backgrounds), Volt yellow `hsl(54,100%,49%)`, black ink, DIN-style condensed uppercase headings.
- Official Volt logo and v5 racket images in `assets/` (downloaded from voltpadel.com).

## Evidence on Hand

- Real: official racket images and specs, the logo, prices, delivery terms, WhatsApp contact.
- Absent (do not fabricate): testimonials, sales numbers, player endorsements, ratings, press, founding year.

## Product Principles

1. Every racket has one clear buy path, and help is always one WhatsApp tap away. Buying and asking are separate actions.
2. Trust before persuasion: official distributor, direct WhatsApp contact, clear terms, no surprises at payment. The brand speaks, not an individual.
3. Look like Volt. A customer comparing with voltpadel.com or Instagram should see the same brand.
4. Phone first. Most visitors arrive from Instagram or the club on a phone.
