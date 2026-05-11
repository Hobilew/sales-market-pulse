# PRD: Sales Market Pulse (MVP)

**Source:** [Notion — PRD: Sales Market Pulse (MVP)](https://www.notion.so/35dda74ef0458022b028d6c3463e8958)  
**Exported locally:** 2026-05-11

---

> **Scope (v1):** This PRD describes a **public, local-first MVP** with **stubbed** market and news data. No external APIs in the initial ship; real-time feeds are a **Phase 2** follow-on.

# Product Review: Sales Market Pulse (MVP)

- **Author:** Hobi Lew
- **Team:** Sales / GTM (Cursor)
- **Date:** 2026-05-11
- **Status:** Draft

## Opportunity

> Cursor sales teams benefit from a single place that connects **market context** with **narrative-relevant news**—especially stories tied to Cursor, AI tooling, and enterprise software buying. Today that information is scattered across terminals, RSS, and social feeds, which makes prep inconsistent and slow.

This MVP proves the **workflow and information architecture** with **deterministic stub data**: a fast dashboard that a rep can scan before calls or territory planning. Shipping a simple, **public** reference implementation builds internal alignment and creates a clean foundation to swap stubs for live sources later—without redesigning the UI.

## Customer Pains

- **Fragmented prep:** Reps jump between market charts, headlines, and internal docs; nothing is tuned to “what matters for Cursor this week.”
- **Latency vs. trust:** “Close to real time” matters, but not at the cost of unclear provenance; users need to see **source** and **timestamp** even in stub mode.
- **Noise:** Generic finance or tech news is overwhelming; the product must prioritize **Cursor-adjacent** themes (IDEs, AI-assisted dev, security/compliance, enterprise procurement).

## Proposed Solution(s)

### Selected approach: Static-first “Sales Pulse” dashboard (MVP)

A small **public** web app (or static site) that renders:

1. **Market snapshot** — key indices / tickers as **stub JSON** (e.g., last close, daily change %), formatted as cards or a compact table.
2. **News river** — curated **stub headlines** with tags such as `Cursor`, `AI devtools`, `Enterprise sales`, each with fake timestamps and “source” labels.
3. **Rep mode** — optional filters (topic chips) that only rearrange **client-side** data (no network beyond hosting the static assets).

**Trade-offs:** No live accuracy in v1 (acceptable for IA/UX validation). **Benefit:** zero API keys, trivial hosting (e.g., GitHub Pages), instant load, reproducible demos.

### Deferred (Phase 2)

Live market + news providers, auth, personalization, and alerting. Those require contracts, rate limits, and compliance review—explicitly **out of scope** for MVP per engineering constraint.

## Mocks / Visuals / Prototype (required)

**MVP visual spec (text wireframe — replace with screenshots when built):**

```
+------------------------------------------------------------------+
| Sales Market Pulse                         [Topic: All v]       |
+--------------------------+---------------------------------------+
| MARKET (stub)            | NEWS (stub, Cursor-relevant)         |
| SPX  +0.4%               | • "Enterprise IDEs adopt AI agents"   |
| QQQ  -0.1%               |   Source: StubWire • 09:12 ET       |
| CRUD (stub ticker) +2.1% | • "Buyer checklist for AI coding"   |
|                          |   Tag: Procurement • 08:05 ET       |
+--------------------------+---------------------------------------+
| Footnote: Data is simulated for MVP (no external APIs).          |
+------------------------------------------------------------------+
```

**Prototype plan:** Implement the layout in the public repo first; attach **2–3 screenshots** to the Notion page before **Ready for Review**.

## Goals & Non-Goals

| Goals (MVP) | Non-Goals (MVP) |
|-------------|-----------------|
| Single-screen overview; stub data; public source; no secrets | Live market data, live news fetch, login, CRM sync |
| Clear labeling that data is **simulated** | Investment advice or trading execution |

## Success Metrics (MVP)

- **Qualitative:** 3+ sales stakeholders say the layout matches their weekly prep workflow.
- **Quantitative (lightweight):** p95 load < 1s on broadband for static build; zero reported “I thought this was live” confusion after adding disclaimer copy.
- **Engineering:** repo is **public**; CI builds green; README documents how to swap stub files.

## Technical Notes

- **Data:** `stub/market.json`, `stub/news.json` (or equivalent) checked into the repo; versioned fixtures for demos.
- **Runtime:** Prefer static generation or client-only rendering—**no server-side external calls**.
- **Privacy:** No PII; no API keys in the client.

## Key Questions for Leadership

1. **Positioning:** Should v1 live under a personal GitHub org vs. a Cursor OSS namespace—any brand requirements for “public”?
2. **Phase 2 priority:** When live data is allowed, do we prefer **one** paid market vendor vs. free tiers with stricter rate limits?
3. **Editorial policy:** Who owns the taxonomy for “Cursor-relevant” tags when news is real—Sales, Comms, or a shared rubric?

## Appendix: Original idea (verbatim)

My Idea is to make an app that pulls in free, close to real time, market data and gives me an overview of all news that is related to Cursor or is relevant to a Salesperson at Cursor.

**Note:** MVP intentionally stubs data and defers external integrations.
