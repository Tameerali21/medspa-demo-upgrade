# "Never Miss a Customer" — Interactive Demo (MED SPA)

A fictional US med spa website (**Glow Haus Med Spa — Aesthetics & Wellness, Austin TX**)
with an embedded AI aesthetic coordinator (**Ava**) that demonstrates Tameer Ali's
**"Never Miss a Customer"** automation system to a med spa owner in ~60 seconds.

**100% static. No backend, no build step, zero external requests, zero tracking.**
Works from `file://` and any static host.

Part of the multi-niche demo factory (see `~/workspace/outreach/demo-links.md`).
Siblings: `~/workspace/outreach/demo/` (Casa Verde restaurant + Maya),
`~/workspace/outreach/demo-dental/` (Bright Smile Dental Studio + Nora).

## What it demonstrates (the 4 flows)

1. **Treatments / pricing Q&A** — ask about Botox (from $12/unit), lip filler
   ("how much is lip filler?" → from $549), laser hair removal (from $99/session),
   facials (from $129), peels, microneedling, and the Glow Membership ($149/mo).
   Consultations are always free — zero pressure.
2. **Consultation booking** — treatment interest → name → optional text reminder →
   preferred day → time → confirmation card with booking reference (e.g. `GH-KT9X2`).
3. **After-hours lead capture** *(the money flow)* — tap "🌙 After-hours demo":
   a notice reads *"It's 11:42 PM — we're closed right now, but I'm Ava,
   Glow Haus's aesthetic coordinator, and I'm still here."* A midnight
   glow-curious inquiry → name + phone + treatment interest → "Saved! The morning
   team will reach out first thing" → a mini **"Saved to your dashboard"** card
   appears. This is the moment that sells the system: *every midnight visitor
   becomes a morning consultation, not a client lost to the spa down the street.*
4. **Review request** — tap "⭐ Rate your visit" → tap the stars:
   - **5 stars** → "Would you share that on Google?" + Google review button.
   - **1–4 stars** → "What could we do better?" → feedback captured →
     "Our spa director will personally follow up."

Plus: graceful fallbacks for off-script input (never dead-ends), quick-reply chips,
typing indicator with realistic delays, auto-open nudge after ~8s, and the site's
"Book a consultation" buttons jump straight into the booking flow.

Copy is in **buyer language** ("never miss a client", "after-hours", "consultation
slots go fast") — never "AI chatbot" jargon. Widget header/footer carries a small
credit: *"Live demo by Tameer Ali · AI Automation"*.

## Personalize per prospect

Append query params — the spa name, tagline, city, address and phone swap
everywhere (page + widget + booking-reference prefix):

```
index.html?biz=Lumiere%20Med%20Spa&tagline=Medical%20Aesthetics&city=Denver%2C%20CO&address=88%20Blake%20St%2C%20Denver%2C%20CO%2080202&phone=%28303%29%20555-0119
```

| Param     | Default                          |
|-----------|----------------------------------|
| `biz`     | Glow Haus Med Spa                |
| `tagline` | Aesthetics & Wellness            |
| `city`    | Austin, TX                       |
| `address` | 2412 S Congress Ave, Austin, TX 78704 |
| `phone`   | (512) 555-0164                   |

`?fast=1` skips animation delays (used by the automated test harness).

**Outreach workflow:** for each med spa prospect, generate their link with
`?biz=<Their Spa Name>` so the demo greets them as *their own* spa.
The personalized demo is the outreach hook — audit opens, demo closes.

## Hosting options

- **Fastest (recommended):** Netlify Drop / Vercel / Cloudflare Pages / GitHub Pages —
  drag the `demo-medspa/` folder, get a public HTTPS link in ~1 minute.
- **Any static host** works — it's plain HTML/CSS/JS.
- **Local preview:** `python3 -m http.server` inside `demo-medspa/`, or just double-click
  `index.html` (works from `file://`).

Hosting is handled by the parent agent — this subagent builds and verifies only.

## Verification

End-to-end harness at `/tmp/verify/verify-medspa.js` (puppeteer-core + local Chromium):
walks all 4 flows, the 5-star and 3-star review branches, bad-phone rejection,
graceful fallback, `?biz=` personalization (incl. multi-word name with `&`),
hero-CTA booking jump, and a mobile viewport — and fails on **any** console/page error.

## Honesty note (2026-10-02 upgrade)

Like the other niche demos, this one originally carried invented "1,200+ Google
reviews" claims and three fabricated named testimonials. The 2026-10-02 upgrade
removed all of them (standing honesty rule): the reviews section is now an honest
"How it works" block describing the automation's real capabilities, and the hero
badges describe the demo (24/7 answers, 60-sec in-chat booking, free consultations).
Open Graph + Twitter Card tags added so shared links render previews. Fictional
business details (Glow Haus Med Spa, (512) 555-0164 — 555 range) remain placeholders
for `?biz=` personalization per prospect.

## Files

- `index.html` — med spa site + widget markup
- `assets/style.css` — all styling (system fonts only, no external requests)
- `assets/widget.js` — Ava conversation engine (intents, booking/after-hours/review
  state machines, personalization, test hooks via `window.__maya`)

*Note: bookings, leads and reviews in this demo are simulated in the browser —
the footer says so. A real client build wires these to the spa's actual
scheduling/CRM/notification stack.*
