# InABox Games — Forager COI test

This is a separate test build. The live `main` branch and existing Apps Script deployment are not replaced.

## Files
- `public/index.html`: the complete existing InABox frontend with its existing features retained, plus the Apps Script API bridge and cross-origin-isolated iframe permission.
- `AppsScript-Code.gs`: the existing Apps Script backend with an allowlisted JSON `doPost` dispatcher added; the existing `doGet` and all other functions remain.
- `worker.js` and `wrangler.toml`: Cloudflare Worker and static asset configuration.

## Safe test setup
1. Open the existing Apps Script project and add the `doPost(e)` dispatcher from `AppsScript-Code.gs` (or replace Code.gs with this complete version). Do not delete the existing `Index.html` project file or Script Properties.
2. Create a **new web app deployment** from the updated script. Keep the current production deployment unchanged. Copy the new test deployment's `/exec` URL.
3. In `wrangler.toml`, replace `PASTE_NEW_TEST_APPS_SCRIPT_EXEC_URL_HERE` with that new test deployment URL.
4. Deploy from this folder with Wrangler: `cd cloudflare-test && npx wrangler deploy`.
5. Test the new Worker URL only. Your existing live site remains on its current URL.

## Verify
Check gallery loading, search, favorites, settings, existing game modal, SWF loading, artwork, shared backgrounds, admin tools, and Forager inside the existing player.

## Compatibility warning
This test uses COOP `same-origin` and COEP `credentialless`. Cross-origin isolation can still block some third-party games. Credentialless contexts may change cookie/storage behavior and therefore affect saved progress or logins. Do not switch production until all important games and persistence have been tested.
