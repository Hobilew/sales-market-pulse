# Sales Market Pulse — Cursor

A Cursor-branded internal **sales briefing dashboard**. Combines:

- **Live pulse** — real-time stories from **Hacker News** (free public `hn.algolia.com` API, no key, no auth) scoped to **Cursor-relevant categories**: Cursor, AI coding tools, Developer experience, Enterprise AI.
- **Curated briefings** — human-authored stories with a Cursor sales angle and copy-pastable **talking points**.

**Built by Hobi Lew.**

- **Repository:** [github.com/Hobilew/sales-market-pulse](https://github.com/Hobilew/sales-market-pulse) (public)
- **Product plan:** [`prd.md`](./prd.md) (local) · canonical copy on [Notion](https://www.notion.so/35dda74ef0458022b028d6c3463e8958)

## Features

- **Daily brief** banner with stat counts and "live data fetched <relative time>"
- **Live pulse** grid of HN stories with category chips, sort (newest / points / discussion), domain, points, comments, and links to both the article and the HN thread
- **Curated briefings** with `summary`, full `article`, **Cursor sales angle**, and **Copy talking points**
- Global **search** across live + curated content (press `/` to focus, `Esc` to clear)
- Light / dark **theme toggle** (system preference default, persisted)
- Manual **Refresh** + **auto-refresh** every 5 min when the tab is visible
- Cursor-branded shell (gradient mark, sticky header, footer attribution)

## Run locally

Browsers block `fetch()` for local files (`file://`), so serve the folder:

```bash
cd ~/Desktop/projects/sales-market-pulse
python3 -m http.server 8765
```

Open [http://localhost:8765](http://localhost:8765).

You need an internet connection — the Live pulse fetches from `hn.algolia.com`. The curated briefings still render if HN is unreachable.

## Project layout

- `index.html` — UI, branding, live HN fetch, curated rendering, interactions (single file)
- `stub/news.json` — curated briefings (`summary`, `article[]`, `relevance[]`, `talkingPoints[]`) + `dailyBrief`
- `prd.md` — local copy of the product requirements (mirrors Notion)

## Tuning the Live pulse

Open `index.html` and edit the `PULSE_CATEGORIES` array near the top of the `<script>`:

```js
const PULSE_CATEGORIES = [
  { id: "cursor",     label: "Cursor",           query: "cursor ai editor" },
  { id: "ai-coding",  label: "AI coding tools",  query: "ai coding assistant copilot" },
  // …
];
```

Algolia's `query` is fuzzy full-text — use plain keywords, not boolean operators.

## Editing curated briefings

All copy lives in `stub/news.json`:

- **Add a story:** append to `items`. Fields: `id`, `headline`, `source`, `publishedAt`, `tags`. Optional: `summary`, `article[]`, `relevance[]`, `talkingPoints[]`.
- **Update the daily brief:** edit the top-level `dailyBrief` string.

## Roadmap (Phase 2.x)

- Additional free sources (Reddit JSON, Lobste.rs, RSS via a small proxy)
- Auto-generated daily brief from the live pulse
- Per-rep saved searches and pinning
- Slack export of the daily brief
