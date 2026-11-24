# InABox Games — Forager COI test

This is a separate test build. The live `main` branch, production wrapper, and current live deployment are unchanged.

## Files
- `public/index.html`: the complete existing InABox frontend with the Apps Script bridge and cross-origin-isolated iframe permission added. Existing UI/features are retained.
- `AppsScript-Code.gs`: the existing Apps Script backend with an allowlisted JSON `doPost` dispatcher added; existing `doGet` and other functions remain.
- `worker.js` and `wrangler.toml`: Cloudflare Worker that serves the static frontend and proxies `/__inabox_api` to Apps Script.

## Test setup
1. In the Apps Script editor, add the `doPost(e)` function from this file to the existing project (or replace the project code with this complete file, keeping the same project and Script Properties). Keep the existing `doGet`; redeploy the web app so the current `/exec` deployment includes `doPost`.
2. Deploy this directory with Wrangler: `cd cloudflare-test && npx wrangler deploy`.
3. Test the Worker URL without changing the live site.

## Verify
Check gallery loading, search, favorites, settings, existing game modal, SWF loading, artwork, shared backgrounds, admin tools, and Forager inside the existing player.

## Compatibility warning
This test uses COOP `same-origin` and COEP `credentialless`. Cross-origin isolation can still block some third-party games. Credentialless contexts may change cookie/storage behavior and therefore affect saved progress or logins. Do not switch production until all important games and persistence have been tested.
