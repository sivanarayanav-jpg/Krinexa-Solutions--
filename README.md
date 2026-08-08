# Krinexa Agri — Website

Single-file marketing site for the **Krinexa Agri** app
(*ప్రతి రైతుకు నమ్మకమైన తోడు — a trusted companion for every farmer*).

Built directly from the UAT build of the app, so every claim on the site maps to a
screen that actually exists: voice OTP, crop history, voice/photo advisory tickets,
agronomist recommendations with dosage and safety, ordering, tracking, GST invoices
and feedback.

```
index.html    ← the entire site: HTML + CSS + JS, no build step, no dependencies
README.md     ← this file
```

## Run it

Open `index.html` in any browser. For a local server:

```bash
python3 -m http.server 8000     # http://localhost:8000
```

## Deploy it

Any static host — drop `index.html` at the root.

| Host | How |
| --- | --- |
| **Netlify** | Drag the folder onto app.netlify.com/drop |
| **Vercel** | `vercel --prod` |
| **GitHub Pages** | Push → Settings → Pages → deploy from `main` |
| **Cloudflare Pages** | Connect repo, no build command, output `/` |

## Structure

The site is service-led, not investor-led — no revenue tables, market sizing,
projections or SWOT. It sells what the farmer gets.

| Section | ID | What it does |
| --- | --- | --- |
| Hero | — | Telugu headline, English support line, live app mockup |
| Trust strip | — | Scrolling band of service guarantees |
| Services | `#services` | Four numbered service cards, bilingual headings |
| **Farmer's Path** | `#path` | The centrepiece — seven steps from problem to solved, on a dashed rail |
| Inside the App | `#app` | Advisory-detail mockup + eight bilingual feature tiles |
| Why It Helps | `#useful` | Six outcome cards — what changes in the field |
| Everyone in the Chain | `#partners` | Farmer / Field Staff / Agronomist / FPO portal + service promise |
| Support | `#support` | Helpline, email, office, incubator |

### The Farmer's Path (the seven steps)

1. **నమోదు చేసుకోండి** — Register once (voice OTP, individual or FPO member)
2. **మీ పంటలు జోడించండి** — Add your crops (crop, stage, acreage, season)
3. **నిపుణుడిని అడగండి** — Ask an expert (voice, text or photos)
4. **సలహా అందుకోండి** — Get the recommendation (24h, dose + safety, in writing)
5. **సరైన ఉత్పత్తి కొనండి** — Order the right product (transparent pricing)
6. **ఇంటికి డెలివరీ** — Delivered and tracked (live tracker, GST invoice)
7. **అభిప్రాయం ఇవ్వండి** — Tell us if it worked (rating + field follow-up)

To add or reorder a step, copy a `.step` block inside `.path` — the dashed rail and
numbering are plain markup, nothing to recalculate.

## Branding

The palette is lifted from the app's own `:root` so the site and the product read as
one system:

```css
--brand-700:#2e7d32;   /* app --primary  */
--brand-200:#b7f1b5;   /* app --pc       */
--brand-50:#e8f5e9;    /* app light bg   */
--gold-500:#f9a825;    /* app --warn     */
--sky-700:#1565c0;     /* app --info     */
--ink:#1a1c19;         /* app --on       */
--line:#e2ebdb;        /* app --s3       */
--surface-2:#fbfdf7;   /* app --surface  */
```

Change these variables and the whole site follows.

## Bilingual typography

Three families, all from Google Fonts with system fallbacks:

- **Noto Sans Telugu** — every farmer-facing string. Applied with `class="te"`, or via
  `.bi b` / `.step__title b` which set it automatically.
- **Plus Jakarta Sans** — English headings and UI labels.
- **Inter** — body copy.

Pattern used throughout: Telugu leads, English supports underneath in smaller
uppercase green. That's the `.bi` component:

```html
<div class="bi"><b>సరైన మందు, సరైన మోతాదు</b><span>RIGHT INPUT, RIGHT DOSE</span></div>
```

If you add Telugu text anywhere, give it `class="te"` so it picks up the correct font
and line height — including Telugu inside an English heading (`<h2>From <span
class="te">"ఏమైంది నా పంటకు?"</span> to a solved problem</h2>`).

## Behaviour

~110 lines of vanilla JS in one IIFE: sticky nav, mobile menu (closes on link click
and `Esc`), `IntersectionObserver` scroll-reveal with stagger, scrollspy on the nav,
back-to-top. The trust strip marquee is pure CSS and pauses on hover.

## Accessibility & quality

- Semantic landmarks, `aria-expanded`/`aria-controls` on the menu, visible focus rings
- Full `prefers-reduced-motion` support — marquee, bob and reveal all disabled
- Responsive from 320px up; verified with no horizontal scroll at 390px and 1440px
- Print stylesheet drops nav, marquee and CTAs
- No external images — icons are inline SVG, the favicon is a data URL

## Customising

**Phone mockups** — they're plain HTML (`.phone` → `.phone__screen`), so you can edit
the Telugu strings directly, or swap the whole `.phone__screen` for a real screenshot:
`<img src="app-home.png" alt="Kisan Manager home screen">`.

**Add a language** — the `.te` class is the only Telugu-specific hook. For Hindi or
Tamil, add the font to the Google Fonts link and a matching `.hi` / `.ta` class.

**App store buttons** — when the app ships, replace the two hero buttons with store
badges; `.btn--ghost` already gives you the light secondary style.

**Contact form** — the CTAs currently use `mailto:` and `tel:`. For a real form, drop a
Formspree or Netlify Forms `<form>` into the right column of `.contact-card__inner`.

---

© Krinexa Solutions Private Limited
