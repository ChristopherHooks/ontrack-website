# OnTrack Dispatch — Website

Multi-page HTML + Tailwind CSS site for the pivot from dispatch services to dispatch software & tools.
Design system generated and persisted by the UI UX Pro Max skill: see `design-system/ontrack/MASTER.md`.

## Pages

| File | Purpose |
|---|---|
| `index.html` | Home — new value prop, three offerings, comparison table, trust section |
| `dashboard.html` | OnTrack Dashboard product page + founding-member early-access CTA |
| `eta-calculator.html` | Free interactive HOS-aware truck ETA calculator (top-of-funnel) |
| `bundle.html` | Run Your Dispatch Vault ($97) → Gumroad CTA |
| `about.html` | The pivot story |
| `contact.html` | Email / phone / OKC + free 15-min consult link |

Header and footer are identical blocks in every page (marked with `<!-- HEADER/FOOTER (shared) -->` comments). Since this is a no-build static site, edit them with find-and-replace across all six files, or move to partials if you later adopt a static-site generator.

## Design system

- Palette: primary `#2563EB`, navy `#1E40AF`, CTA orange `#F97316`, background `#EFF6FF`, body text slate-900
- Font: Plus Jakarta Sans (Google Fonts)
- Source of truth: `design-system/ontrack/MASTER.md`; per-page overrides go in `design-system/ontrack/pages/`

## Preview locally

Just open `index.html` in a browser — no build step. For a proper local server (needed for the ETA tool's route lookup on some browsers):

```bash
cd "Site Redesign"
python3 -m http.server 8080
# then visit http://localhost:8080
```

## ETA tool — implementation choice

Built as a **fully interactive, ungated tool** (no email capture). Reasons: better SEO (a working free tool earns links and repeat direct visits), better goodwill with a skeptical audience, and the page itself upsells the Dashboard and Vault. Route miles come from free OpenStreetMap services (Nominatim geocoding + OSRM routing — no API key, no cost); if the lookup fails or is rate-limited, the tool falls back to manual mile entry and all HOS math still works. If traffic grows large, consider self-hosting OSRM or a paid routing API; I flagged this rather than adding one now.

## Deploy

Any static host works — drag the folder into **Netlify**, or push to GitHub and enable **GitHub Pages**, or use **Cloudflare Pages** / **Vercel**. No server code required. Point the `ontrackhs.com` domain at the host and you're done.

## If you stay on Squarespace

Squarespace can't host multi-page raw HTML sites cleanly. Options, best to worst:

1. **Recommended:** host this site on Netlify/Cloudflare Pages (free) and point your domain there; retire the Squarespace site.
2. **Code injection (partial port):** individual sections (the ETA calculator's form + script, the Vault content grid) can be pasted into Squarespace **Code Blocks** per page. Tailwind via CDN must be added in Settings → Advanced → Code Injection (header). Expect styling conflicts with your Squarespace template; budget cleanup time.
3. Keep Squarespace pages but embed the ETA tool via an `<iframe>` pointing at the hosted version of `eta-calculator.html`.

## Punch list — still needed from you (Chris)

1. **Logo** — replace the "OT" mark in the header/footer of all six pages (marked `<!-- LOGO SLOT -->`).
2. **Dashboard screenshots** — the mockups on `index.html` and `dashboard.html` are labeled illustrative; swap in real product shots when ready.
3. **Dashboard pricing & purchase** — nothing is set up yet. Recommendation: run early access via the email CTA now (already built), and when ready to charge, use a **Gumroad membership product** for the subscription — you already have Gumroad, it handles cards/tax, zero new infrastructure. Then replace the early-access card with a real pricing table.
4. **Confirm the contact email** — the site uses `dispatch@ontrackhs.com` per your spec; your current address is `dispatch@ontrackhaulingsolutions.com`. Make sure `ontrackhs.com` mail actually routes to you (or tell me to swap it).
5. **Gumroad URLs** — currently pointing at `2327315340655.gumroad.com/l/dispatch-vault` and `/l/consult`. Consider setting a custom Gumroad username so links read `ontrackdispatch.gumroad.com/...`.
6. **Domain decision** — `ontrackhs.com` vs a new `ontrackdispatch.com`; brand on the site is "OnTrack Dispatch" per your approval.
