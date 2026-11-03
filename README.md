# Stream mapper

A guided value stream mapping tool. It is a single static file (`index.html`): no build step, no server, no database. Maps and uploaded documents stay in each person's browser.

## Put it online

Pick whichever your team already uses. All of them just serve `index.html` over HTTPS.

| Host | Steps |
|---|---|
| Netlify | Go to app.netlify.com/drop and drag this folder onto the page. You get a link immediately. |
| GitHub Pages | Create a repo, upload `index.html`, then Settings > Pages > deploy from the main branch. |
| Cloudflare Pages or Vercel | Create a project from the repo or folder. Framework: none. Build command: none. Output directory: the folder holding `index.html`. |
| Internal web server | Copy `index.html` to any folder served by IIS, nginx, Apache or an S3-style bucket with static hosting. |

Use HTTPS. Copy-to-clipboard and some file features need a secure page.

## What works with no AI connection

Everything except the Claude features: scope, step-by-step mapping, improvements with sliders, results, the report, image and CSV downloads, and document upload with text preview. Downloads use the browser's normal download.

## Optional: Claude features

Drafting a map from a document, checking a step, finding ideas and asking your documents need an API connection. Users open **Reference documents > Claude connection** and either:

1. Paste their own Anthropic API key. It is kept in the browser tab only, unless they tick "Remember on this device". Requests go straight from the browser to the endpoint shown.
2. Or, for a team rollout, you set the **Endpoint** to your own proxy, which holds the key server side. Then nobody needs a key. The proxy must accept POST `/v1/messages`, allow cross-origin requests from your site, and add the `x-api-key` header itself.

Notes:
- The default model is `claude-sonnet-5-5`. It can be changed in the same panel.
- Anything a user sends to Claude leaves their browser, so check your data policy before people upload client documents.
- A key stored in a browser is only as safe as that browser. On shared computers, use the proxy approach.

## Third-party files it loads

For a locked-down network, allow these or host copies yourself.

- Google Fonts: fonts.googleapis.com and fonts.gstatic.com (falls back to system fonts if blocked).
- cdnjs.cloudflare.com, loaded only when needed to read an uploaded file: pdf.js 3.11.174 (PDF), mammoth 1.6.0 (Word), SheetJS 0.18.5 (Excel).
- Text, CSV and pasted text need none of these.

## Updating

Replace `index.html` with the new version. Saved maps carry over because they live in each person's browser under the same site address. If the address changes, saved maps do not move with it.

## Limits to know about

- Data is per browser and per device. There are no accounts and no shared maps.
- Reading PDFs relies on the file's text layer. Scans need to be uploaded as images (needs the Claude connection) or pasted as text.
- Each uploaded document is trimmed to about 30,000 characters, and PDFs are read up to 40 pages.
