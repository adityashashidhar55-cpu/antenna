# Antenna

Strategic trend intelligence for India and France — a marketing site plus a full-feature dashboard tracking breakout, rising and steady trends, an AI Trend Radar, contextual strength scoring, AI-grounded startup ideas, an AI Foresight Analyst chatbot, and (where generated) AI-estimated SEO/content insights per trend.

**Live site:** https://adityashashidhar55-cpu.github.io/antenna/

## Site map

Static, no-build-step pages served directly by GitHub Pages:

- `index.html` — marketing landing page
- `app.html` — the product dashboard (single-page app: trends, Trend Radar, startup ideas, workspace/watchlist, pain points, products, startups, meta trends, tools)
- `pricing.html` — plans, monthly/annual toggle, Stripe-hosted checkout
- `account.html` — subscription status + billing portal
- `use-cases.html`, `reports.html`, `blog.html` — SEO content hub
- `terms.html`, `privacy.html`, `security.html`, `status.html` — legal/trust pages

Every page is a single self-contained HTML file (inline CSS/JS, Chart.js for visualizations) — no build tools, no bundler.

## Backend

Powered by an n8n workflow ("Antenna Billing & AI Assistant API" + the original trend-data workflow) with Data Tables for trends, startup ideas, AI-estimated topic insights, subscribers, and leads. Base URL:

`https://adityashashidhar.app.n8n.cloud/webhook/antenna`

Trend data endpoints (read-only, CORS-open):
- `GET /trends` — live trend feed (also carries AI-estimated SEO keywords, content angles, channel breakdown, "why now" and forecast notes per trend, once generated)
- `GET /startup-ideas` — ~15 startup ideas per market, each grounded in a real tracked trend

Billing endpoints (require a Stripe secret-key credential configured in n8n before they'll do anything beyond a graceful "not configured yet" response):
- `POST /billing/create-checkout-session`, `POST /billing/create-portal-session`, `GET /billing/status`, `POST /billing/contact-sales`

AI Foresight Analyst endpoint (keyword-ranks real stored trends, feeds only that real context to an LLM with a no-fabrication system prompt):
- `POST /ai-chat` (or `/foresight` — see app.html's chat wiring for the exact path)

SEO/content insight fields, AI forecast projections, and chat answers are clearly labeled in the UI as AI-generated/estimated, never presented as verified human research.

## Running locally

```bash
python3 -m http.server 8080
# open http://localhost:8080/index.html for the marketing site
# open http://localhost:8080/app.html for the dashboard
```

## Deploying

This repo is served directly by **GitHub Pages** (Settings → Pages → deploy from `main` branch, root). Any push to `main` updates the live site within a minute or two.

## `build/`

Internal build artifacts (the multi-agent build script, raw agent outputs, verification scripts/screenshots). Not part of the deployed site — excluded via `.gitignore`.

