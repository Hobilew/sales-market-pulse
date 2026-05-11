# PRD: Sales Market Pulse (v1.1) — Cursor sales briefing

**Source:** [Notion — PRD: Sales Market Pulse](https://www.notion.so/35dda74ef0458022b028d6c3463e8958)
**Updated:** 2026-05-11 (rev. 1.1)

---

> **Scope (v1.1):** Browser-only, **public** app that combines a **live news feed** (free public APIs, no key/auth) with **curated briefings** that include a Cursor sales angle and copy-pastable talking points.
> The previous "market snapshot" section has been **removed** in favor of a tighter focus on stories that affect Cursor and the sales role.

# Product Review: Sales Market Pulse (Cursor sales briefing)

- **Author:** Hobi Lew
- **Team:** Sales / GTM (Cursor)
- **Date:** 2026-05-11 (rev. 1.1)
- **Status:** Draft

## What changed in v1.1

- **Removed** the financial Market Snapshot (tickers, sparklines). Reps don't trade; tickers were context, not action — and credible live market data needs a paid vendor.
- **Added** a real-time **Live pulse** feed sourced from **Hacker News** via the public `hn.algolia.com` search API (no API key, no auth, browser-side fetch).
- "Market" in the product name now means **the market for AI dev tools and the conversations shaping it**, not equities.

## Opportunity

> Cursor sales reps need a single screen that surfaces, in near-real time, **what's actually being said about Cursor, AI coding, developer experience, and enterprise AI** — plus a sharp, pre-written sales angle on the stories they should bring into calls.

The MVP validated the layout with stubs. v1.1 connects to **live, free** sources so reps see **what's being talked about right now**, while preserving curated briefings that contain the sales judgment Cursor reps actually need to repeat in conversations.

## Customer pains

- **Fragmented prep:** Reps assemble context from several places before a call.
- **Noise:** Generic tech news is overwhelming; the live feed must be **scoped by Cursor-relevant queries**.
- **No sales angle on raw news:** Reps don't want a generic feed reader — they want a single screen that says *"this story matters because…"*.

## Proposed solution

### A. Live pulse (NEW)

- Browser `fetch()` to **`https://hn.algolia.com/api/v1/search`** for a small set of **Cursor-relevant categories** (Cursor, AI coding tools, Developer experience, Enterprise AI). Categories are configured in `index.html` under `PULSE_CATEGORIES` and are easy to tune.
- **Per-card metadata:** title (links to original), HN discussion link, source domain, points, comment count, relative time, category chips.
- **Filters:** multi-select category chips; sort by Newest / Most points / Most discussed; global search box.
- **Refresh:** manual button; auto-refresh every 5 minutes when the tab is visible; "Live data fetched <relative time>" in the brief banner.

**Why HN Algolia:** free, no key, CORS-enabled (`Access-Control-Allow-Origin: *`), broad coverage of dev-tools/AI discourse, generous rate limits for personal use.

### B. Curated briefings (existing, stays)

- Stub JSON (`stub/news.json`) with `summary`, `article[]`, `relevance[]`, **`talkingPoints[]`** per item, plus a top-level `dailyBrief`.
- This is where the **sales judgment** lives — pre-written narrative the rep can drop into a conversation. The "Live pulse" surfaces what's hot; the "Curated briefings" tell the rep how to use it.
- Each briefing has a **Copy talking points** button (clipboard).

### Phase 2.x candidates (still deferred)

- Additional free sources (Reddit JSON, Lobste.rs, RSS via a small proxy).
- AI-generated daily brief from the live pulse (server-side or via Cursor's API).
- Per-rep saved searches and pinned stories.
- CRM/Slack export of the daily brief.

### Explicitly out of scope

- Live financial market data, auth, personalization, alerting, CRM sync.

## Mocks (text wireframe)

```
+--------------------------------------------------------------------+
| [logo] Sales Market Pulse                  [search /]  [theme] [↻] |
+--------------------------------------------------------------------+
| DAILY BRIEF                                                        |
| Lead with governance: enterprises are tightening AI-coding…        |
| 5 briefings · 24 live stories · fetched 2m ago                     |
+--------------------------------------------------------------------+
| LIVE PULSE   [HN · live]                                           |
| Chips: [Cursor] [AI coding tools] [Developer experience] [Ent. AI] |
| +----------------------------+  +----------------------------+     |
| | Cursor                     |  | AI coding tools            |     |
| | "Show HN: …"               |  | "AI coding assistants are…"|     |
| | hn.com · 132 pts · 48c · 4h|  | medium.com · 90 pts · 22c  |     |
| | Open story →  HN discussion|  | Open story →  HN discussion|     |
| +----------------------------+  +----------------------------+     |
+--------------------------------------------------------------------+
| CURATED BRIEFINGS                                                  |
| Headline · meta · summary                                          |
|   Story (collapsible)                                              |
|   Why this matters (collapsible) [ Copy talking points ]           |
+--------------------------------------------------------------------+
```

## Goals & Non-Goals (revised)

| Goals (v1.1) | Non-Goals (v1.1) |
|---|---|
| Live, free, no-key news feed scoped to Cursor relevance | Live financial market data |
| Curated briefings with copy-pastable talking points | Per-rep auth or CRM sync |
| Public repo, GitHub Pages compatible | Server-side fetching or background workers |
| Clear labeling of live vs. curated content | "AI brief" generation in v1 (Phase 2.x) |

## Success metrics (revised)

- A rep opens the page **once per day** for prep.
- ≥80% of HN stories surfaced by the queries are deemed **relevant** by a sample of reps (≤20% noise).
- Live pulse renders in **< 2 s on broadband**; failures degrade gracefully with a clear retry path.
- Briefings remain **edit-only-via-JSON** so non-engineers can update content.

## Technical notes

- **Live data:** `fetch()` to `https://hn.algolia.com/api/v1/search` from the browser; categories defined in `index.html` (`PULSE_CATEGORIES`).
- **Resilience:** `Promise.allSettled` per category; partial failures still render. If all fail, show inline error and a Refresh button.
- **Caching:** `cache: "no-store"` on fetch + 5-minute auto-refresh + manual refresh.
- **Privacy:** No PII, no telemetry, no keys. Static hosting compatible (e.g., GitHub Pages).
- **Files:** `index.html` (UI + logic, single file), `stub/news.json` (curated briefings + daily brief), `prd.md` (this doc).

## Key questions for leadership

1. **Coverage:** Is HN-only enough for v1.1, or do we want Reddit / Lobste.rs / RSS in v1.2?
2. **Editorial:** Who owns the curated briefings (Sales, Comms, GTM-shared)? Should they be authored in Notion and exported here?
3. **Freshness:** Is 5-minute auto-refresh appropriate, or do we want push-style updates?
4. **Naming:** Keep "Sales Market Pulse" (now meaning "the AI-dev-tool market") or rename to something like "Cursor Sales Pulse"?

## Appendix: Original idea (verbatim)

My Idea is to make an app that pulls in free, close to real time, market data and gives me an overview of all news that is related to Cursor or is relevant to a Salesperson at Cursor.

**Note:** v1.1 fulfills the intent of "free, close to real-time" by sourcing from the public Hacker News search API. The financial-market reading of "market data" was dropped in favor of the **AI dev tools market** — the conversation that actually moves Cursor sales cycles.
