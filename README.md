# Volt Padel Thailand

Landing page for Volt Padel Thailand, the official Volt Padel distributor in Thailand and Southeast Asia. It's a single static page: `index.html` plus images in `assets/`. There's no build step.

## Run locally

Open `index.html` in a browser, or serve the folder:

```sh
npx serve .
```

## Editing

- **Prices, specs, descriptions**: the `RACKETS` array in the `<script>` at the bottom of `index.html`. The cards are rendered from it. Prices must match the table in `CLAUDE.md`.
- **WhatsApp number**: `WHATSAPP` at the top of the same script (digits only, international format). The `href` values in the HTML are fallbacks for when JavaScript doesn't run.
- **Colors and fonts**: CSS variables in `:root` at the top of the `<style>` block.

## Coach referral links (prepared, not launched)

`https://<domain>/?ref=CODE` stores the code in the visitor's browser for 30 days. Every WhatsApp message they send from the site then ends with `Coach code: CODE`, so the sale can be traced to that coach. Codes may use letters, numbers, `-` and `_` (2–24 characters).

## Deploy (Cloudflare Pages)

1. Cloudflare dashboard → Workers & Pages → Create → Pages.
2. Connect this GitHub repo, or use **Upload assets** and drag in the folder.
3. Build settings: framework preset **None**, build command empty, output directory `/`.
4. After the first deploy: **Custom domains** → add `voltpadelthai.com` (or the domain you register). If the domain is on Cloudflare, DNS is set up automatically.

With the GitHub connection, every push to the production branch redeploys automatically.
