# Sales Market Pulse (MVP)

Static dashboard with **stubbed** market and news data—no external APIs.

**Repository:** [github.com/Hobilew/sales-market-pulse](https://github.com/Hobilew/sales-market-pulse) (public)

Product plan: **`prd.md`** (local); canonical copy on [Notion](https://www.notion.so/35dda74ef0458022b028d6c3463e8958).

## Run locally

Browsers block `fetch()` for local files (`file://`). Serve the folder, then open the app:

```bash
cd ~/Desktop/projects/sales-market-pulse
python3 -m http.server 8765
```

Open [http://localhost:8765](http://localhost:8765).

## Project layout

- `prd.md` — product requirements (mirrors Notion)
- `index.html` — UI and client-side filtering
- `stub/market.json` — sample indices / tickers
- `stub/news.json` — briefing-style stories: **`article`** (paragraph strings) and **`relevance`** (why it matters for Cursor sales); optional **`relevanceTitle`**

Edit the JSON files to change demo data. Replace with real sources in a later phase.
