# Antenna

Trend intelligence for India and France — an interactive, full-feature dashboard tracking breakout, rising and steady trends, AI-grounded startup ideas, and (where generated) AI-estimated SEO/content insights per trend.

**Live site:** https://adityashashidhar55-cpu.github.io/antenna/

A single self-contained `index.html` (dark SaaS-dashboard UI, Chart.js visualizations, search/filter/sort, a personal watchlist saved in your browser, and CSV export) that talks to a live automation backend — no build step, hosted free on GitHub Pages.

## Backend

Powered by an n8n workflow with three Data Tables (trends, startup ideas, and AI-estimated topic insights). Read-only public endpoints, CORS-open, base:

`https://adityashashidhar.app.n8n.cloud/webhook/antenna`

- `GET /trends` — live trend feed (also carries AI-estimated SEO keywords, content angles, channel breakdown, "why now" and forecast notes per trend, once generated)
- `GET /startup-ideas` — ~15 startup ideas per market, each grounded in a real tracked trend

SEO/content insight fields are clearly labeled in the UI as AI-generated estimates, not measured search data.

## Running locally

No build tools needed:

```bash
python3 -m http.server 8080
# open http://localhost:8080/index.html
```

## Deploying

This repo is served directly by **GitHub Pages** (Settings → Pages → deploy from `main` branch, root). Any push to `main` updates the live site within a minute or two.
