# Architecture (tentative)

## 1. Agent interface (the product, not an add-on)

- **OpenAPI-first REST API** is the source of truth; the MCP server is a thin layer over it.
- **Remote MCP server** (streamable HTTP). Sketch of tools:
  - `weather_window` — forecast and go/no-go *inputs* for a site and time window (never the decision)
  - `start_checklist`, `record_check_item` — walk a checklist item by item
  - `compute_tank_mix` — carrier volume, product rates and batch quantities, with label-rate sanity checks
  - `log_application` — write the application record
- **Checklists as MCP prompts**, so an assistant can present each as a prompt card.
- **Actor on every write** (human id or agent id) into an **append-only audit log**.
- **Go/no-go is a pilot confirmation.** Agents may recommend; the record shows who confirmed.

## 2. Scope boundary

The aircraft maker's app stays primary for mapping, route planning, flight control, execution and on-aircraft logs. FOSADMA owns: pre-flight and regulatory checklists, weather go/no-go inputs, flight-plan filing step (a checklist item with a captured reference number), tank-mix preparation, product/label records, pilot and aircraft compliance (including pilot recency), maintenance, and the application record.

## 3. Offline PWA and sync

Local-first client database synced to a small server behind a **storage adapter**. No Firebase/Firestore. Google Sheets/Drive are export targets only (no transactions, rate limits, weak for audit and agents). Heavy parsing (spreadsheet/KML import) runs in the client, not on the server.

## 4. Domain packs (versioned, cited data)

Aircraft spec packs, checklist templates, jurisdiction rule packs (first: Canada/Ontario), product/label library. Every rule is tagged as a **legal requirement** (with a source link) or an **operator preference**. Default checklists contain legal requirements only; the owner can add preference items, but cannot remove legal ones. Every rule carries a source link and a "last verified" date; rules such as manufacturer declaration listings are re-checked on a schedule because they can change.

## 5. Deployment targets

| Target | Shape |
|---|---|
| Private hardware | Docker, single service, SQLite |
| Cloudflare free plan | Workers (API/MCP) + static assets (PWA) + D1 (SQLite) + R2 (files) |

D1 is SQLite, so the same schema runs in both targets.

### Cloudflare free-plan feasibility (single user) — verdict: fits

Figures from Cloudflare's published pages as of 2026-11-06 ([Workers pricing](https://developers.cloudflare.com/workers/platform/pricing/), [Workers limits](https://developers.cloudflare.com/workers/platform/limits/index.md), [D1 pricing](https://developers.cloudflare.com/d1/platform/pricing/index.md), [R2 pricing](https://developers.cloudflare.com/r2/pricing/index.md), [Durable Objects](https://developers.cloudflare.com/durable-objects/index.md)). Re-verify before depending on them.

| Piece | Free limit |
|---|---|
| PWA shell (Workers static assets) | Static asset requests free and unlimited; up to 20,000 files per version, 25 MiB per file |
| API / MCP Worker | 100,000 requests/day (account-wide across all Workers and Pages Functions), 10 ms CPU per request (time awaiting I/O does not count) |
| D1 | 5 M rows read/day, 100 k rows written/day, 5 GB total |
| R2 | 10 GB-month, 1 M Class A and 10 M Class B ops/month, free egress |
| Durable Objects (SQLite-backed) | Available on the free plan (100 k requests/day) |

Design consequences:

- **Hard stops, not bills.** On the free plan, exceeding a limit makes that operation fail. The offline PWA must keep working from local data during an outage.
- **D1 counts rows *scanned*.** Index lookups that matter.
- **10 ms CPU** is fine for checklist state, audit writes and tank-mix arithmetic, but not for parsing large spreadsheets/KML on the server (unmeasured estimate), so do it in the client.
- **Quota is per account**, so keep other projects' Workers on a different account or budget for sharing.
- Third-party summaries list D1 at 500 MB per database and 50 queries per invocation on free; not confirmed against Cloudflare's own page.
- **Unverified, to spike:** whether a stateless remote MCP endpoint runs in a plain free-plan Worker, whether R2 needs a payment method on file even for the free tier, and how to put authentication in front of the endpoint.

## 6. Optional integrations

farmOS sync (JSON:API/OAuth2); weather provider behind an interface (Open-Meteo for non-commercial use, <10k calls/day, CC BY 4.0 data; Environment and Climate Change Canada services for commercial deployments); NAV Drone has no public API, so it is a checklist step.
