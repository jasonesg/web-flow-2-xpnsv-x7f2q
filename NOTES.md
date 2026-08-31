# Recreation Notes (corrected 2026-08-31)

This is a static, offline-editable copy of Houdy's Webflow "Home" page, rebuilt directly from the **actual live published HTML/CSS** (fetched right after the user republished the site), not from a Designer-only element-tree reconstruction.

## Correction from the first attempt
An earlier version of this export (via the Data API's full element tree) mistakenly included a Team/Founders section, an FAQ section, a second CTA section, and extra footer legal links. The user clarified these are **not real page content** — inside Page Wrapper, only two sections actually exist and publish: `Section-HeroBox` and `Footer Section`. This version reflects only those two, matching the live site exactly.

## What's included
- `index.html` — the real published markup for the navbar, hero (video background + pitch copy + contact form), and footer, with the SEO title/description already set this session.
- `styles.css` — the actual compiled Webflow stylesheet (`houdysvideocompany.webflow.shared.b7ebfd692.css`), pulled directly from the live site. Includes Webflow's own base framework CSS plus all custom classes — this is why the first export's layout was broken (it only had the ~173 custom classes, not Webflow's foundational grid/reset CSS) and this one isn't.
- `webflow.schunk.js`, `webflow.runtime.js` — Webflow's own interaction/runtime engine, downloaded locally from the site's CDN bundle.
- jQuery, GSAP (+ DrawSVG/ScrambleText plugins), and Google's WebFont loader are still referenced from their public CDNs (no reason to vendor those locally).

## Known gaps
- The contact form will not actually submit anywhere (no backend) — it's cosmetic/static.
- Video/image assets (hero background clips, nav icon, brand logo) are still referenced from Webflow's CDN (`cdn.prod.website-files.com`) rather than downloaded locally — they'll keep working as long as those assets stay on Webflow's CDN, independent of this site's publish status.
- Webflow's IX2 interaction data embedded in `webflow.runtime.js`/inline JSON drives things like the navbar scroll-blur effect; this should work the same as production since the real runtime files are used.
