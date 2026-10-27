# AI-managed online shop

A complete store: customer storefront, an AI chat assistant, a free-promotion studio and an admin panel.
No database. Only dependency: Express. Needs Node 18+.

## Run it

```bash
npm install
ADMIN_PASSWORD=choose-a-password GEMINI_API_KEY=your-key node server.js
```

- Shop: http://localhost:3000
- Admin: http://localhost:3000/admin (log in with ADMIN_PASSWORD)
- Get a free Gemini key at https://aistudio.google.com/apikey (free tier is enough to start).
- Without a key the shop still works and the chat answers basic shipping/returns/payment questions.

Optional environment variables: `PORT`, `SITE_URL` (your public URL, used in promo links and sitemap),
`GEMINI_MODEL`, `AUTOPILOT=off` (turn off the daily promo drafts).

## What the AI agent does

| Job | How |
|---|---|
| Chats with customers | Chat bubble on the shop. Knows your products, shipping, returns, coupon. Never invents facts. Passes angry or unclear cases to you with the customer's contact. |
| Free promotion | Admin > Free promotion. Writes TikTok/Reels scripts, Instagram captions, Pinterest pins, Facebook posts, X posts, WhatsApp Status text and SEO blog posts, with tracked links. Autopilot adds fresh drafts daily. |
| Writes product pages | Admin > Products > "AI write description". |
| Daily briefing | Dashboard summarises orders, chats needing you, and what customers keep asking. |

## What you still do (and why)

1. Post the promo drafts. TikTok, Instagram and Pinterest suspend accounts that auto-post, so copy, paste, post. About 5 minutes a day.
2. Confirm orders. Admin > Orders. Contact the customer, then order the item from your supplier (AliExpress, CJ Dropshipping, etc.) and paste the tracking number in.
3. Replace the demo products with real ones from your supplier. Use their real photos (Image URL field) and real specs. The demo products are placeholders.
4. Check the AI's text against the supplier listing before saving, especially specs.

## Before you take real orders

- Payments: checkout collects the order and you confirm by phone/message. When you are ready for card payments, add Stripe Checkout or a local provider (for example Chapa or Telebirr in Ethiopia). Do not collect card numbers yourself.
- Edit the shipping, returns and contact details in Admin > Settings so they are true. Customers rely on them.
- Add real customer reviews only after real customers leave them. Never fake them.
- Check the consumer and import rules for the countries you sell to.
- Back up the `data/` folder (it holds orders, chats and subscribers).

## Free hosting

Any Node host works (Render, Railway, Fly.io free tiers, or a small VPS). Set the environment variables above and `SITE_URL`.
Free tiers can sleep or wipe files, so use a host with a persistent disk for `data/`, or back it up often.

## Files

- `server.js`: API, AI agent, promo studio, SEO (sitemap, product meta tags)
- `public/index.html`: storefront (cart, checkout, order tracking, chat)
- `public/admin.html`: admin panel
- `data/`: products.json, settings.json, plus orders/chats/promo created as you go
