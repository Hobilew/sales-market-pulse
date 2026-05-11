# Sales Market Pulse — Cursor

A Cursor-branded internal **sales briefing dashboard**: market snapshot + Cursor-relevant news with a "why this matters" sales angle on every story. Static, **stubbed** data — no external APIs.

**Built by Hobi Lew.**

- **Repository:** [github.com/Hobilew/sales-market-pulse](https://github.com/Hobilew/sales-market-pulse) (public)
- **Product plan:** [`prd.md`](./prd.md) (local) · canonical copy on [Notion](https://www.notion.so/35dda74ef0458022b028d6c3463e8958)

## Features

- **Daily brief** banner with rep-facing takeaway and stub disclaimer
- **Market snapshot** grouped by Indices / AI infra / Dev tools, with mini sparklines and color-coded change %
- **News briefings** with full multi-paragraph stories and a Cursor sales angle on every item
- **Talking points** per story with one-click **copy to clipboard**
- **Search** (slash to focus), multi-select **topic chips**, and **sort** controls
- **Light / dark theme toggle** with system-preference default and saved choice
- **Refresh** button to re-pull stub JSON without a page reload
- Polished Cursor-branded shell, sticky header, footer attribution, and small touches (toasts, skeletons, fade-in)

## Run locally

Browsers block `fetch()` for local files (`file://`), so serve the folder:

```bash
cd ~/Desktop/projects/sales-market-pulse
python3 -m http.server 8765
```

Open [http://localhost:8765](http://localhost:8765).

## Project layout

- `index.html` — UI, branding, interactions (single-file app)
- `stub/market.json` — grouped tickers with `history` arrays for sparklines
- `stub/news.json` — briefings: `summary`, `article[]`, `relevance[]`, `talkingPoints[]`, plus `dailyBrief`
- `prd.md` — local copy of the product requirements (mirrors Notion)

## Editing stub content

All copy lives in JSON — no code changes needed:

- **Add a ticker:** append to a group's `quotes` array in `market.json`. `history` should be ~12 numbers ending at the current value.
- **Add a story:** append to `items` in `news.json`. Required-ish fields: `id`, `headline`, `source`, `publishedAt`, `tags`. Optional: `summary`, `article`, `relevance`, `talkingPoints`.

## Roadmap (Phase 2)

- Swap stub fetches for real market + news providers (back-end key handling)
- Per-rep saved filters and pinning
- Slack export of the daily brief
