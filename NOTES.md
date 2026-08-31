# Recreation Notes (corrected 2026-08-31)

This is a static, offline-editable copy of Houdy's Webflow "Home" page, rebuilt directly from the **actual live published HTML/CSS** (fetched right after the user republished the site), not from a Designer-only element-tree reconstruction.

## Correction from the first attempt
An earlier version of this export (via the Data API's full element tree) mistakenly included a Team/Founders section, an FAQ section, a second CTA section, and extra footer legal links. The user clarified these are **not real page content** — inside Page Wrapper, only two sections actually exist and publish: `Section-HeroBox` and `Footer Section`. This version reflects only those two, matching the live site exactly.

## What's included
- `index.html` — the real published markup for the navbar, hero (video background + pitch copy + contact form), and footer, with the SEO title/description already set this session.
- `styles.css` — the actual compiled Webflow stylesheet (`houdysvideocompany.webflow.shared.b7ebfd692.css`), pulled directly from the live site. Includes Webflow's own base framework CSS plus all custom classes — this is why the first export's layout was broken (it only had the ~173 custom classes, not Webflow's foundational grid/reset CSS) and this one isn't.
- `webflow.schunk.js`, `webflow.runtime.js` — Webflow's own interaction/runtime engine, downloaded locally from the site's CDN bundle.
- `assets/` — hero video (mp4+webm+poster), nav logo, and favicons, all downloaded locally so nothing depends on Webflow's CDN anymore.
- jQuery, GSAP (+ DrawSVG/ScrambleText plugins), and Google's WebFont loader are still referenced from their public CDNs (no reason to vendor those locally).

## Hosting
Self-hosted on GitHub Pages: https://jasonesg.github.io/web-flow-2-xpnsv-x7f2q/ (repo: https://github.com/jasonesg/web-flow-2-xpnsv-x7f2q). No Webflow dependency for hosting, styling, or media.

## Contact form
Wired to a Google Form instead of Webflow's backend — **confirmed working end-to-end as of 2026-08-31** (test submissions verified landing in the connected "Houdy's Contact. (Responses)" Sheet).
- The submit button (`#gform-submit-btn`) is a plain `<button>`, not a native form submit — a click handler builds a real hidden `<form>` (not `fetch`, which Google silently dropped in testing) and POSTs it into a hidden iframe targeting Google's `formResponse` endpoint.
- Field mapping (from the form's pre-filled link): `name` → `entry.1410514541`, `Email` → `entry.1511181486`, `URL` → `entry.1961264758`, `Text-Box` → `entry.677414797`.
- **Gotcha that caused early failures**: the Google Form's responder access defaulted to restricted, returning "We're sorry. This document is not published" to anonymous visitors. Fixed by setting responder access to "Anyone with the link" (Settings → Responses in the Form editor). Editor/collaborator access can stay restricted — that's separate from responder access.
- Because the request is cross-origin, there's still no way for the page to confirm success/failure to the visitor — the "Thank you" message always shows regardless of actual outcome. Worth knowing if submissions ever silently stop working again (e.g. if responder access gets reset).

## Known gaps
- Webflow's IX2 interaction data embedded in `webflow.runtime.js`/inline JSON drives things like the navbar scroll-blur effect; this should work the same as production since the real runtime files are used.
