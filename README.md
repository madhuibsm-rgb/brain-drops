# Brain Drops — Premium Hero Landing Page

A single, self-contained landing page for **The Drops Co. — Brain Drops**.

## Deploy

Everything is inlined into `index.html` (fonts, scripts, images). To host:

- **Netlify / Vercel / Cloudflare Pages** — drop this folder in, or connect the git repo. No build step.
- **GitHub Pages** — push to a repo, enable Pages on the branch root; `index.html` is served automatically.
- **Any static host / S3 / cPanel** — upload `index.html`.

## Needs internet (normal for a hosted site)

- **Ingredient video** in the "Trusted For Generations" section is a live HLS stream.
- **Waitlist form** posts Name / Email / City / Phone to a Google Sheet. See
  `google-sheet-setup.md` to create the Apps Script endpoint and paste its URL into the form handler.

## Files

- `index.html` — the complete website.
- `google-sheet-setup.md` — how to wire the waitlist to Google Sheets.
