# Harf by HIA — Website Build Hand-off

For Claude Code. Put this file at `docs/HANDOFF.md` in the repo and point `CLAUDE.md` to it.
Design reference (canvas, three working screens): https://claude.ai/artifact/Gy43Wa4PbqBEx61dATjP8n
Brand hand-off: `docs/brand-handoff.md` (copy the project's "Harf by HIA — Brand Hand-off" there).
Character sheet (locked): https://claude.ai/artifact/1mjGEE9mAmnFSGQQ2jivta

---

## 1. What we're building

A shop for Harf by HIA: printed Arabic-learning products for children from about age 3. The buyers are parents, starting with the Dawoodi Bohra community. India first; EU and UAE later.

The site reads like a story. Every section answers the question the one before it raises. Nothing should feel out of place or out of context.

Tone: playful for children, trustworthy for parents. Characters and motion can bounce; text, layout and claims stay calm, clean and grown-up. No hype. Claims only about products that exist.

## 2. Phases

**Phase 1: the site (build now).** All pages, animations, cart and checkout UI. Product data lives in a typed file (`src/content/products.ts`). Payment uses a mock adapter so the full flow can be clicked through. No database, no accounts needed.

**Phase 2: selling (later, when accounts exist).** Supabase (database + admin login), Razorpay UPI QR (payment), Resend (email). Swap the mock adapter for the real one; move products into Supabase.

**Phase 3: abroad.** EU and UAE checkout path (cards), currency, shipping zones.

Build every Phase 1 piece so Phase 2 slots in without redesign: keep payment, order storage and email behind small interfaces.

## 3. Stack

- Next.js (App Router) + TypeScript, deployed on Vercel. Repo on GitHub.
- Tailwind CSS with the tokens below as theme variables.
- Animations: CSS keyframes for simple loops; the `motion` library (`motion/react`) for scroll-triggered and gesture animations.
- Fonts via `next/font/google`: Fraunces (600, italic 400), Fredoka (400/500/600), Baloo Bhaijaan 2 (500/700/800), Amiri (400/700), DM Sans (500/600).
- Cart state in a client store (Zustand or React context), persisted to `localStorage`.

## 4. Brand rules (non-negotiable)

1. Right to left by default for anything Arabic: tracing direction, letter sequences, tile order, form tiles (Isolated → Initial → Medial → Final reads right to left). Use `dir="rtl"` on Arabic runs.
2. Pair every Arabic label with a short English one. Arabic-Indic numerals (١ ٢ ٣) beside Western ones where numbers are shown to children.
3. Characters: Insiyah, Husena, Hasan exactly as on the character sheet. Export their SVGs from the canvas; never redraw from memory. Full sleeves for all; girls' hair covered; no rida on a 3-year-old; Insiyah visibly taller.
4. Religious words get non-figurative pictures (Alif = Allah = mosque at dusk). First letter of each word highlighted, except الله.
5. Footer always shows "Harf · by HIA".
6. Colour never gives away a puzzle answer. Generous space, one clear message per section.

## 5. Design tokens

**Base (brand pastels)**
| Token | Hex | Use |
|---|---|---|
| cream | #FFF8F1 | page background |
| plum | #4A4560 | text, primary buttons, footer |
| plum-soft | #5A5570 | body copy |
| lavender | #6A5AA8 | kickers, italic accents (passes contrast on cream) |
| lilac-line | #C9BDEB | dotted thread, outlines |
| blush | #F7C6CE | tile ح |
| mint | #BFE6D6 | tile ر |
| sky | #C6DDF3 | tile ف |
| butter | #F6D98A | secondary buttons, badges |

**Accents (kids' bright, used sparingly)**: coral #F2665E, sunshine #F7B32B, mint #2EC4A6, sky #3FA7E8, lavender #9B7FE6, orange #FF8A3D, leaf #7CC04B, pink #F06BAE. Never white text on these brights (contrast fails); use plum or a dark tint.

**Flash card palette (only on flash card mockups)**: cream #F7F2EA, ink #2F3A45, terracotta #C4785A, sand #D8B27A, sage #8EA58C, dusty blue #7E99AE, blush #E9D5C6.

**Type**: Fraunces for headlines and the wordmark (italic for accents). Fredoka for UI and body. Baloo Bhaijaan 2 for Arabic display. Amiri for Arabic on flash cards. DM Sans for small uppercase kickers (14px, 0.14em tracking).

**Shape**: radii 22–48px on cards and sections, pill buttons (999px), touch targets ≥ 44px (buttons 48–56px). Soft, no hard outlines.

## 6. Site map

| Route | Page |
|---|---|
| `/` | Homepage (story, 8 chapters) |
| `/shop/[slug]` | Product page |
| `/our-story` | Full family letter |
| `/cart` | Cart |
| `/checkout` | Details form → payment sheet |
| `/order/[orderNumber]` | Success / order status |
| `/shipping`, `/replacements`, `/privacy`, `/terms`, `/contact` | Policies |
| `/admin` | Family admin (Phase 2: login required) |

## 7. Homepage chapters

A dotted lilac "thread" (the tracing line from the logo) connects every chapter. Copy below is final unless marked [placeholder].

1. **A letter appears (hero).** ح ر ف tiles drop in one by one (right to left), the pencil draws the dotted line right to left. Kicker in Arabic: حرفاً حرفاً. Headline: "Arabic, one letter *at a time.*" Sub: "Flash cards, tracing and puzzle books that turn the Arabic alphabet into play. Made by our family, for little hands from about age 3." Buttons: Explore the shelf / Read our story.
2. **Why paper.** "There will be a whole lifetime for screens." + "These first years are for crayons and pencils, for tracing a letter with one small finger, getting it a little wrong, and trying again." Three cards: Touch / Trace / Play.
3. **Meet the Harf friends.** Husena ("Salaam! I'm Husena.") and Hasan ("And I'm Hasan. Look, it's ب!") gently bobbing in a lavender masjid-toned panel.
4. **How Harf teaches.** "Start at the dot. *Follow the line.*" ب traces itself on scroll from the numbered start dot, right to left, then its dot appears. Example word: بيت · bayt · house.
5. **The shelf.** Product cards, the whole-shelf bundle, "Peek at the cards" (three flash cards that flip on tap: Alif, Ba, Ta), then Coming soon (Colouring book, Story books) with "Tell me when it's ready".
6. **How to order.** 1/١ Choose · 2/٢ Scan and pay ("Scan the QR with any UPI app. That's all you do.") · 3/٣ Packed with love · 4/٤ On its way ("We email you a tracking link when it ships.").
7. **From our family to yours.** Insiyah illustration; "We started Harf for our daughter." Short excerpt; H/I/A chips (Husena, our daughter · Insiyah, her mother · Aliasgar, her father); link to `/our-story`.
8. **FAQ.** Age, payment, delivery [X–Y days], damaged items (replace; no refunds otherwise).

## 8. Animations

| Where | Behaviour |
|---|---|
| Hero tiles | Drop with overshoot, staggered 0.25s, settle at slight tilts (-7°, 5°, -3°) |
| Hero line + pencil | Dotted path draws right → left; pencil travels with it |
| Sparkles | Slow twinkle loops |
| Characters | Gentle bob/tilt loop, offset so they never move in sync |
| Thread between chapters | Draws as it scrolls into view |
| Letter trace | Stroke-dashoffset trace from start dot when in view; dot pops in after |
| Product cards | Lift + slight tilt on hover |
| Flash cards | 3D flip on tap/click (keyboard accessible: they are `<button>`s) |
| Checkout sheet | Slides up; "waiting" dots pulse; success tick pops |

All motion off (static end state) under `prefers-reduced-motion`. Don't animate anything that blocks reading or buying. Keep the page light for weak mobile connections: inline SVG, no video, lazy-load below the fold.

## 9. Products (Phase 1 data)

```ts
type ProductStatus = 'available' | 'coming_soon' | 'sold_out';
type Product = {
  slug: string;
  name: string;            // English
  nameAr: string;          // Arabic label
  summary: string;
  format: string;          // e.g. "A6 · 28 two-sided cards"
  pricePaise: number | null; // integer paise; null = placeholder
  status: ProductStatus;
  wipeClean: boolean;      // shows a "Wipe-clean" badge only when true
  images: string[];        // mockups now, real photos later
};
```

| slug | name | Arabic | format | status |
|---|---|---|---|---|
| flash-cards | Alphabet flash cards | بطاقات | A6, 28 two-sided cards: word + picture front; tracing + four forms back | available |
| tracing-book | Wipe & Write tracing book | اكتب | A4, 53 pages: 28 letters + numbers ١–٢٠ | available |
| puzzle-book | Letter puzzle book | ألغاز | A5, 20 colour pages: hunts, mazes, matching, word search, certificate | available |
| bundle | The whole shelf | — | all three together | available |
| colouring-book | Colouring book | — | [details] | coming_soon |
| story-books | Story books | — | [details] | coming_soon |

Prices, delivery charge and delivery days are placeholders: render `[₹ PRICE]` when `pricePaise` is null. `wipeClean`: [confirm per product].

## 10. Checkout and payment

**Customer does only this:** cart → Pay now → one short form (name, mobile, PIN code, email, address; city/state auto-filled from PIN) → pay sheet with a QR → scan and pay → the screen turns into "Payment received!" by itself. No UTR, no WhatsApp, no screenshots.

**Phase 2 implementation (Razorpay UPI QR):**
1. On "Pay", the server creates an order (status `pending_payment`) and a Razorpay **single-use, fixed-amount UPI QR** for that order, with a short expiry (e.g. 15 min) and the order number in `notes`.
2. The sheet shows the QR image. On a phone, also offer "Open UPI app" (a customer can't scan their own screen). Confirm in Razorpay's docs the best way to offer the same-phone UPI intent alongside the QR; Standard Checkout may be needed for that path.
3. Razorpay sends the `qr_code.credited` webhook to `/api/webhooks/razorpay`. Verify the signature, check amount = order total, mark the order `paid` (idempotent), close the QR.
4. The browser learns about it by polling `/api/orders/[n]/status` every 2–3s (or Supabase Realtime) and switches to the success screen.
5. On `paid`: email the customer a receipt; email the admin inbox the full order (items, address, phone, payment id).
6. Expired/unpaid QRs: order becomes `expired`; customer can retry.

Razorpay needs a verified merchant account (KYC, bank account) before going live. Use test mode until then.

**Phase 1:** a `PaymentProvider` interface with `MockProvider` (QR placeholder + "simulate payment" in dev only) and later `RazorpayProvider`.

## 11. Orders, admin and notifications

Statuses: `pending_payment → paid → packed → shipped (tracking link) → delivered`, plus `expired`, `cancelled`.

**Admin page (`/admin`, phone-first):** tabs Paid / Packed / Shipped; one big button per order to move it forward; "Mark shipped" asks for courier + tracking link and triggers the customer's shipping email. Phase 2 login: Supabase magic link with an allowlist of family emails.

**Notifications:** email (Resend) from an address on the shop's domain. Admin alert on every paid order; customer emails on paid and shipped. WhatsApp alerts are optional later (needs WhatsApp Business API).

**Claude as CRM (Phase 2):** connect Claude to Supabase via its MCP server, scoped to this project only. Family and Aliasgar use it for product changes (price, status, new products), order lookups and reports. Claude confirms before any write. Product changes in the database show on the site without a redeploy.

## 12. Our story (`/our-story`) — final copy

> We started Harf because of something we kept seeing.
>
> Our daughter Husena, her friends, the children all around us: so many little hands were already reaching for a phone, swiping before they could hold a pencil, watching instead of making.
>
> As parents, that stayed with us. So we asked ourselves a simple question: what do we want her childhood to feel like?
>
> We want it to feel like paper. Like the squeak of a crayon and the smudge of a sketch pen. Like tracing a letter with one small finger, getting it a little wrong, and trying again. Like ink on her hands, and, honestly, sometimes on her arms too.
>
> There will be a whole lifetime for screens. The reels and the games will still be there later. But these first years pass so quickly, and they only come once. We believe this is the time for real things she can touch, hold and make her own, so the creativity inside her has room to come to life.
>
> So we started making them. First alphabet flash cards, then a tracing book, then a puzzle book. Harf (حرف) means "letter," and that is where every child's journey with Arabic begins: one letter at a time.
>
> The name HIA is us. **H** for Husena, our daughter, who started it all. **I** for Insiyah, her mother. **A** for Aliasgar, her father. You'll meet Husena and her mother in our books, along with her best friend Hasan.
>
> We are a small, homegrown family brand from India. Every order is packed by hand by our family and sent with love to yours.
>
> We hope your little one enjoys them as much as ours does.
>
> With love,
> Insiyah & Aliasgar

## 13. Policies and legal (placeholders)

Shipping, replacements (damaged items replaced; no refunds otherwise), privacy, terms, contact with seller details and a grievance contact. Indian e-commerce rules and GST should be checked with a CA before launch. Store only what's needed to ship (name, phone, email, address).

## 14. Quality bar

- Mobile first (most buyers are on phones); works at 360px.
- Lighthouse ≥ 90 on performance and accessibility.
- Text contrast ≥ 4.5:1; real buttons and links; flip cards keyboard-operable; visible focus states.
- SEO: titles, descriptions, Open Graph image per page; `lang` and `dir` set correctly on Arabic runs.

## 15. Build order for Claude Code

1. Scaffold Next.js + Tailwind, tokens, fonts, layout, header, footer.
2. Export character SVGs and logo from the canvas into `src/components/art/`.
3. Homepage chapters 1–8 with animations and the thread.
4. Product data + product pages.
5. Cart, checkout form, pay sheet, success page with `MockProvider`.
6. Our story + policy pages.
7. Admin UI with mock data.
8. (Phase 2) Supabase schema + RLS, Razorpay webhook, Resend emails, admin login, Claude MCP.

## 16. Open items

- Prices, bundle price, delivery charge, delivery days.
- Which products are wipe-clean.
- Domain name and admin email inbox.
- Real product photos to replace mockups.
