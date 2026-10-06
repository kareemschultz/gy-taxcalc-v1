# GYCalc: archived previous version

Archived previous version of GYCalc, kept for comparison only. Its calculations are out of date and have known errors:
do not use it for decisions. Current app: https://kareemschultz.github.io/gy-taxcalc/

Live archive: https://kareemschultz.github.io/gy-taxcalc-v1/ (served from the `gh-pages` branch, which holds only the built static site).

## What this is

The exact site that was live just before the 3.0 rebuild, built from source commit
`ecc7e1306cdc68ce979ae97e804cb6ef45447d1d` of the private GYCalc repo (merge of PR #1, 2026-10-05; CHANGELOG 2.8.1; the in-app badge
reads "v2.4.0", which is the old app's own text). It was the last commit deployed before the rebuild (`90a5238`).
No source is kept here.

## The only changes to the old code

1. `next.config.ts`: `basePath` `/gy-taxcalc` -> `/gy-taxcalc-v1`, `assetPrefix` `/gy-taxcalc/` -> `/gy-taxcalc-v1/`.
2. `lib/brand.ts`: `SITE_URL` -> `https://kareemschultz.github.io/gy-taxcalc-v1` (only used for canonical/Open Graph URLs).
3. `app/layout.tsx`: `robots: { index: false, follow: false }`, which adds `<meta name="robots" content="noindex, nofollow">`.

No visible UI, text or calculation change. The old app has no service worker and no web app manifest, so it cannot claim
`/gy-taxcalc/` scope or offer an install.

## Storage on the shared origin (kareemschultz.github.io)

- `localStorage["theme"]`: next-themes, `light` or `dark`, written only when the visitor toggles the theme.
- Cookie `sidebar_state`: `true`/`false`, 7 days, `path=/`, written when the sidebar is toggled.
- No financial value is ever stored (source checked, and observed in a browser after using the calculators).
- The new app at `/gy-taxcalc/` writes the same two names, and reads only `theme` (a display preference); it reads
  no other key the old app writes.

Built with `npm ci && NODE_ENV=production npm run build` (Node 22), published as `out/` plus `.nojekyll`.
