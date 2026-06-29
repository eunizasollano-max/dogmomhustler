# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Pages in This Project

| File | What it is | Edit when you want to… |
|------|-----------|------------------------|
| `index.html` | **Paws & Breathe sales page — light theme (active)** | Hero, story, pricing, testimonials, FAQs, UBC cross-promo, digital products shop sections |
| `index-v2.html` | Alt sales page — dark luxury theme (not in use) | Same content as index.html but completely different visual design |
| `checkout.html` | **Paws & Breathe checkout page** | 3 payment tabs (Stripe, QR Code, PayPal), SeaBank QR, product summary |
| `registration.html` | **Free registration page** | Name + email form that redirects to the Systeme.io access page (no payment) |
| `kumayunitywelcome.html` | **Paws & Breathe post-payment welcome page** | "You're in, dogmom!" confirmation; PayPal redirects here, links to `accessthesnoot.html` |
| `accessthesnoot.html` | **Paws & Breathe post-purchase access page** | Welcome message, 26 resource buttons, welcome video embed |
| `ubcmain.html` | **UBC sales page** | Hero (with logo), features, 25 course modules, testimonials, FAQs, P&B cross-promo, digital products shop sections |
| `checkoutubc.html` | **UBC checkout page** | Stripe one-time + 3-month plan buttons, PayPal Smart Button, product sidebar |
| `3monthubc.html` | **UBC 3-month payment plan page** | Important notice, order summary, Stripe button, Systeme.io button |
| `ubcaccess.html` | **UBC post-purchase access page** | Congratulations header, welcome video, Skool community link |
| `checkout-pathway.html` | **Standalone checkout — Pathway to Digital Products** | Stripe + PayPal tabs, $15 USD, redirects to `thankyou-pathway.html` on PayPal success |
| `checkout-instagram.html` | **Standalone checkout — Instagram Growth Guide** | Stripe + PayPal tabs, $12 USD, redirects to `thankyou-instagram.html` on PayPal success |
| `checkout-faceless.html` | **Standalone checkout — Faceless Marketing + Reels Vault** | Stripe + PayPal tabs, $10 USD, redirects to `thankyou-faceless.html` on PayPal success |
| `checkout-threads.html` | **Standalone checkout — Threads Unleashed + Super Seller** | Stripe + PayPal tabs, $17 USD, redirects to `thankyou-threads.html` on PayPal success |
| `thankyou-pathway.html` | **Thank-you page — Pathway to Digital Products** | 1 Canva download button |
| `thankyou-instagram.html` | **Thank-you page — Instagram Growth Guide** | 1 Canva download button |
| `thankyou-faceless.html` | **Thank-you page — Faceless Marketing + Reels Vault** | 2 buttons: Canva guide + Google Drive reels folder |
| `thankyou-threads.html` | **Thank-you page — Threads Unleashed + Super Seller** | 2 buttons: Canva guide + Google Drive file |
| `catalog.html` | **Full product catalog** | All products in one page — flagship, mini guides, coming soon, free resources |
| `images/` | Shared images | `hero.png`, `story.png`, `triumph.png`, `win-1/2/3.png`, `seabank-qr.png`, `ubc-logo.png`, `logo.png` |

All HTML files are **completely independent** — editing one never affects the others.

---

## Architecture

**No build step. No frameworks. No bundler.** Every page is a self-contained HTML file with all CSS in a `<style>` block and all JS in `<script>` tags at the bottom.

### Light theme design system
Used by: `index.html`, `checkout.html`, `registration.html`, `accessthesnoot.html`, `kumayunitywelcome.html`, all `checkout-*.html` and `thankyou-*.html` pages.
```css
--bg: #FFFAF8        --bg-alt: #FFF1ED     --bg-card: #FFFFFF
--pink: #C8707A      --pink-soft: #E8A8AE  --pink-pale: #FAE8EA
--border: #EDD5D7    --text: #2D1A1A       --muted: #8A6860
--radius: 12px
```
Fonts: `Playfair Display` (headings) + `Nunito` (body/buttons)

### UBC design system
Used by: `ubcmain.html`, `checkoutubc.html`, `3monthubc.html`, `ubcaccess.html`. Same structure as light theme but with a **darker rose pink** accent:
```css
--pink: #A85060      --pink-soft: #C4889A  --pink-pale: #EFD8DE
--border: #DFC8CE    --text: #2D1A1A       --muted: #8A6860
```
Fonts: same (`Playfair Display` + `Nunito`)

### index-v2.html — Dark luxury design system
CSS custom properties + Tailwind CDN:
```css
--bg: #0D0508        --bg-alt: #160B0E     --bg-card: #1E1014
--pink: #E8909A      --pink-soft: #C8707A  --pink-pale: #3A1A20
--gold: #D4A96E      --cream: #F5E6E8      --border: #3A2028
```
Fonts: `DM Serif Display` (h1) + `Playfair Display` (h2/h3) + `Nunito` (body)

### Shared cursor (all pages)
Heart-shaped paw SVG cursor — hollow by default, fills pink on `:active`. Embedded as base64 data URI in `--paw-hollow` and `--paw-filled` CSS variables. When changing the pink color on a page, update both the CSS variable value **and** the `%23XXXXXX` hex codes inside the SVG data URIs and all `rgba(R,G,B,...)` shadow values.

---

## Payment Integrations

### Paws & Breathe (checkout.html) — ₱2,499 PHP
| Method | Implementation |
|--------|---------------|
| **Stripe** | Redirect to `https://buy.stripe.com/3cI28sgskfuiaTV59Les001` |
| **PayPal** | Smart Button via PayPal JS SDK — captures ₱2,499 PHP, redirects to `kumayunitywelcome.html` on success |
| **QR Code** | SeaBank InstaPay — `images/seabank-qr.png`, scrolls to `#qr-payment` section |

### UBC (checkoutubc.html) — $499 USD
| Method | Implementation |
|--------|---------------|
| **Stripe one-time** | Redirect to `https://buy.stripe.com/00wdRa1xqfuigef59Les003` |
| **Stripe 3-month plan** | Redirect to `3monthubc.html` (standalone plan page) |
| **PayPal** | Smart Button via PayPal JS SDK — captures $499 USD, redirects to `ubcaccess.html` on success |

### UBC 3-month plan (3monthubc.html) — $499 USD split
| Method | Implementation |
|--------|---------------|
| **Stripe** | Redirect to `https://buy.stripe.com/28E28sfog4PE4vx59Les002` |
| **Systeme.io** | Redirect to Systeme.io checkout link |

### Standalone Digital Products (checkout-*.html) — USD
| Product | Price | Stripe Link | Thank-you page |
|---------|-------|-------------|----------------|
| Pathway to Digital Products | $15 | `https://buy.stripe.com/6oU14o8ZSeqe5zB7hTes004` | `thankyou-pathway.html` |
| Instagram Growth Guide | $12 | `https://buy.stripe.com/fZu5kEgsk2HwaTV9q1es005` | `thankyou-instagram.html` |
| Faceless Marketing + 600 Reels | $10 | `https://buy.stripe.com/bJeaEYa3Wa9Ye67cCdes006` | `thankyou-faceless.html` |
| Threads Unleashed + Super Seller | $17 | `https://buy.stripe.com/7sY5kE1xqdma4vxeKles007` | `thankyou-threads.html` |

All standalone checkout pages use `currency=USD` in the PayPal SDK URL and `currency_code: 'USD'` in `actions.order.create()`. PayPal `onApprove` redirects to the product-specific thank-you page.

**Stripe note:** Stripe success URLs must be configured in the Stripe Dashboard for each payment link — they are not controlled in the HTML. Set each link's success URL to the matching `thankyou-*.html` on your deployed domain.

**PayPal Client ID** (public, safe in frontend): `AR2LKMzynpl2QrnW3lzl5LOiAS5-FGtPkyGioy1X-FAYR5x5ZnT9qnxeqgk36v_ySDvaFBONn4a8hk8y`

PayPal SDK is loaded in `<head>` with `defer`. Buttons are initialized in a `window.addEventListener('load', ...)` block at the bottom of each checkout page. The SDK `currency` param must match the `currency_code` in `actions.order.create()`.

---

## User Flows

### Paws & Breathe purchase
`index.html` → `checkout.html` → Stripe / SeaBank QR → *(Stripe success URL configured in dashboard)* → `kumayunitywelcome.html` → `accessthesnoot.html`
PayPal path: `checkout.html` → PayPal `onApprove` → `kumayunitywelcome.html` → `accessthesnoot.html`

### UBC purchase
`ubcmain.html` → `checkoutubc.html` → Stripe one-time / PayPal → `ubcaccess.html`
3-month path: `checkoutubc.html` → `3monthubc.html` → Stripe / Systeme.io

### Standalone digital products
`index.html` or `ubcmain.html` (Digital Products section) → `checkout-[product].html` → Stripe / PayPal → `thankyou-[product].html` (with download links)

### Free registration / gifted access
`registration.html` → `https://dogmomhustler.systeme.io/accessthesnoot`
- Name + email form with JS validation (`getAccess()` function)

### Paws & Breathe post-purchase access
`accessthesnoot.html` — 26 resource buttons (Canva, Google Drive, Mega, Telegram, PDFs) + YouTube welcome video (`https://youtu.be/UM70lP2cp7c`). To update a resource link, find `<a href="..." class="resource-btn">` in the resource list section.

> **P&B is self-paced** — no Zoom calls, no live sessions. The "What's Inside" list and FAQ on `index.html` reflect this. Do not add bi-weekly Zoom or pre-recorded tutorial mentions back.

---

## Cross-Promotion Sections

Both main products link to each other:
- **index.html** has two UBC teaser sections: one after the Hero (`.ubc-teaser-wrap` div) and one above the footer. Both link to `ubcmain.html`.
- **ubcmain.html** has a Paws & Breathe teaser section above the footer, linking to `index.html`.

Both `index.html` and `ubcmain.html` also share an identical **"More Digital Products"** section above the footer (a 2×2 grid of `.bonus-card` / `.dp-card` elements). In `index.html` this reuses existing `.grid-2` and `.bonus-card` classes. In `ubcmain.html` it uses `.dp-grid` and `.dp-card` defined in an inline `<style>` block just before the section, since those class names don't exist in ubcmain.html's main CSS.

Both navs also have a **"🛍️ More Products"** link → `catalog.html`. In `index.html` it sits inside `.nav-text-links` (hidden on mobile). In `ubcmain.html` it sits in a flex wrapper next to the "Join Now" button using the `.nav-back` style.

---

## Page Structure Reference

### Standalone checkout pages (`checkout-pathway.html`, `checkout-instagram.html`, etc.)
1. Nav (logo + "← Back to shop" link to `index.html`)
2. Pink page header (product name + USD price badge)
3. Two-column layout: **left** (2-tab payment: Stripe · PayPal) | **right** (product sidebar, sticky)
4. Footer + PayPal SDK init script
- No QR tab, no contact form — simplified from `checkout.html`
- `currency=USD` in PayPal SDK

### Thank-you pages (`thankyou-pathway.html`, `thankyou-instagram.html`, etc.)
1. Nav (logo only, centered)
2. Aurora background
3. Centered `.welcome-card`: paw icon → "Payment Confirmed" eyebrow → "Thank you for your purchase!" h1 → divider → message → download button(s) → help text
4. Footer
- Products with 2 downloads show a filled pink button + an outline pink button (`.btn-download.outline`)

### index.html (top → bottom)
1. Countdown banner → sticky nav
2. Hero (split layout) + mobile sticky buy bar + scroll-to-top button
3. **UBC teaser** (`.ubc-teaser-wrap`) — cross-promo with pill badges → `ubcmain.html`
4. "Are You in a Similar Situation?" — 2-col pain points grid
5. Pull quote
6. My Story (split layout)
7. From Adversity to Triumph (split layout)
8. What's Inside — product box (2-col item grid) + stats sidebar
9. Bonuses — 3-col cards
10. Personal Wins — 3 screenshot images
11. Testimonials — 3 cards with expandable "See more"
12. Pricing / offer card
13. FAQ — native `<details>`/`<summary>`
14. Final CTA section
15. **UBC bottom teaser** — second cross-promo → `ubcmain.html`
16. **Digital Products shop** — 2×2 grid (`.grid-2` + `.bonus-card`) → individual `checkout-*.html`
17. Footer

### ubcmain.html (top → bottom)
1. MRR banner → sticky nav (← Back to `index.html`)
2. Hero — UBC logo (`images/ubc-logo.png`) + title + Join Now button
3. Why UBC? — 5-item features grid
4. Testimonials — 3 cards side by side
5. Course Layout — 25 modules (accordion `<details>`) + Bonus Content Vault
6. Q&A — 6 FAQ items
7. Final CTA → `checkoutubc.html`
8. **Paws & Breathe teaser** — cross-promo → `index.html`
9. **Digital Products shop** — 2×2 grid (`.dp-grid` + `.dp-card`) → individual `checkout-*.html`
10. Footer

### checkout.html (top → bottom)
1. Countdown banner → nav ("← Back to sales page")
2. Pink page header with price badge
3. Two-column: **left** (contact form + 3 payment tabs: Stripe · QR · PayPal) | **right** (product sidebar, sticky)
4. Testimonials (3 cards)
5. SeaBank QR section (`id="qr-payment"`)
6. Footer + PayPal SDK init script

### checkoutubc.html (top → bottom)
1. Nav ("← Back to UBC")
2. Pink page header
3. Two-column: **left** (contact form + Stripe buttons + PayPal button + installment option) | **right** (product sidebar with `ubc-logo.png`, sticky)
4. Footer + PayPal SDK init script

### 3monthubc.html (top → bottom)
1. Nav
2. Pink page header
3. Important notice
4. Order summary
5. Stripe button
6. Systeme.io button
7. Footer

### registration.html (top → bottom)
1. Nav
2. Pink page header ("Register for Access")
3. Two-column: **left** (name + email form + access button) | **right** (product sidebar, sticky)
4. Testimonials (3 cards)
5. Footer

### accessthesnoot.html (top → bottom)
1. Nav
2. Pink thank-you header
3. Two-column intro: product image + instructions | numbered steps + video CTA
4. Welcome video (YouTube embed)
5. "Where do I Start?" — 26 pink resource buttons
6. Important notice / reselling instructions
7. Footer

### ubcaccess.html (top → bottom)
1. Nav
2. Congratulations header + UBC logo
3. Welcome video (YouTube embed)
4. Skool community link / next steps
5. Footer

### catalog.html (top → bottom)
1. Nav — "Paws & Breathe" logo + "← Back to home" link
2. Pink page header — "Digital Product Catalog"
3. **Flagship Products** section (`--bg-alt`) — 2-col grid: UBC (⭐ Best Seller badge) + P&B
4. **Guides, Courses & Vaults** section (`--bg`) — 2-col grid: 4 mini guides (Pathway, Instagram, Faceless, Threads)
5. **Coming Soon** section (`--bg-alt`, dashed card) — "Another Day, Another Chance" physical journal
6. **Free Resources** section (`--pink-pale`) — 2 freebies with Google Drive links (`.btn-outline`)
7. Footer

All catalog cards use `.prod-card` with a `.card-footer` row (price + button). Free items use `.price-free` pill + `.btn-outline`. Coming soon card uses `border-style: dashed`.

### kumayunitywelcome.html (top → bottom)
1. Nav (logo centered)
2. Aurora background animation
3. Centered card: paw icon → "You're in, dogmom!" → link to `accessthesnoot.html`
4. Footer

---

## Design Recreation Workflow (rules/)

The `rules/` folder contains workflow instructions for when the user provides a screenshot to recreate:

1. **Generate** a single HTML file using Tailwind CSS (via CDN). Include all content inline.
2. **Screenshot** the rendered page and compare against the reference image. Check: spacing/padding (px), font sizes/weights, colors (exact hex), alignment, border radii/shadows, responsive behavior.
3. **Fix** every mismatch. Re-screenshot and compare again.
4. **Repeat** until no visible differences remain (target: within ~2–3px of reference).

**Constraints:** Do not add features or content not in the reference. Match exactly — do not "improve" the design. Use `https://placehold.co/` for placeholder images when source images aren't provided.

---

## Deploying

No build step — deploy the entire folder (`*.html` + `images/`) as a static site.

**Netlify drag & drop (fastest):** [app.netlify.com/drop](https://app.netlify.com/drop)

```bash
netlify deploy --dir . --prod   # Netlify CLI
vercel --prod                   # Vercel
surge .                         # Surge
```

**GitHub Pages:** repo Settings → Pages → source: `main` branch `/root`.

> PayPal Smart Buttons require HTTPS to render. They will not load on `file://` — use a local server (`npx serve .`) or deploy to test.
