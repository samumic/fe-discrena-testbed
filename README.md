# Discrena Widget Testbed

A public, GitHub-Pages-hosted fictional customer site used to test the Discrena widget against the Staging backend on a real third-party domain.

## What this is

This repository simulates a real customer website embedding the Discrena widget. It is hosted on GitHub Pages so the widget loads on a domain that is genuinely third-party from `*.staging.discrena.io` — meaning Cross-Origin behaviour, cookie handling, and CDN delivery match real customer integrations.

The pages are styled to look like a plausible fictional company (**Sonderlin**, a Swiss premium coffee subscription service) so that visitor classification has realistic content to work against.

## Pages

| Page          | Path             | Purpose                                                                                  |
| ------------- | ---------------- | ---------------------------------------------------------------------------------------- |
| Home          | `index.html`     | Landing-page demo. Generic browsing context — should classify as informational/awareness. |
| Pricing       | `pricing.html`   | Pricing-context demo. Should drive `pageCategory='pricing'` and price-oriented signals.  |
| Debug Console | `debug.html`     | Developer view — shows resolved widget config, window globals, and a live network log.   |

The `debug.html` page is intentionally not linked from `index.html` or `pricing.html` (it appears in its own nav only). Reach it via direct URL.

## Local development

```bash
git clone <repo>
cd fe-discrena-testbed

# Replace placeholders with your real Staging credentials
# (do this in your local working copy only — see security note below)
sed -i '' 's/REPLACE_WITH_PROPERTY_ID/your-property-id/g' index.html pricing.html debug.html
sed -i '' 's/REPLACE_WITH_API_KEY/your-api-key/g' index.html pricing.html debug.html

# Serve locally
python3 -m http.server 8000
# Open http://localhost:8000
```

On Linux drop the `''` after `sed -i`.

## Important security note

> **Never commit credentials.** The placeholder strings (`REPLACE_WITH_PROPERTY_ID`, `REPLACE_WITH_API_KEY`) are committed to git. You replace them only in your local working copy when testing. **Do not** stage, commit, or push the replaced versions.
>
> Because the placeholders live in tracked files, `.gitignore` cannot protect you here — it relies on developer discipline.

### Local-only credential workflow

1. Clone the repo locally.
2. Replace the placeholders in your local files with real Staging credentials.
3. Test locally with `python3 -m http.server 8000`.
4. **Do not commit** your changes. When you are done, either `git restore .` or revert the placeholders manually.
5. Push only the placeholder versions.

A defensive belt-and-braces option: copy each HTML file to a `*.local.html` variant (already in `.gitignore`) and edit those instead.

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. **Settings → Pages → Source**: `main` branch, `/ (root)` folder.
3. Wait ~1 minute for the first deploy.
4. URL becomes: `https://<username>.github.io/<repo>/`

## Live URL

`https://samumic.github.io/fe-discrena-testbed/` *(placeholder until Pages is enabled)*

## Tech stack

Plain HTML and CSS. No build step, no JavaScript framework, no npm. Three HTML pages and one shared stylesheet — instantly editable, instantly deployable.
