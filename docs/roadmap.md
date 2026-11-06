# Roadmap and open questions (tentative)

## Open questions

- [ ] License: GPL-3.0 is in place. Decide whether to switch to AGPL-3.0 to cover network-hosted forks, before any outside contributions arrive (relicensing later needs contributor consent).
- [ ] Is the operating site in controlled airspace? This decides whether each flight needs an ATC/NAV Drone authorization.
- [ ] Ontario pesticide applicator licensing for drone application.
- [ ] Real Agras controller logs and SmartFarm `.xlsx`/KML exports to test against dji-log-parser (needs an aircraft owner to contribute samples; strip location data first).
- [ ] Spike: stateless remote MCP on a free-plan Cloudflare Worker; auth in front of it; R2 payment-method requirement.
- [ ] Client-side local-first database choice (must work offline, sync to SQLite/D1).
- [ ] First jurisdiction rule pack format and verification workflow.

## Proposed milestones

1. **Data model + MCP tool list** (spec only): entities for aircraft, pilot credentials and recency, sites/fields, checklists and runs, products and labels, tank mixes, jobs, application records, weather snapshots, audit events.
2. **Walking skeleton:** one Worker + D1 + PWA shell, one checklist run written through both the UI and an MCP tool, with actor on every audit row.
3. **Checklist engine + Canada rule pack v0** (recency gate, SAD check, 152.4 m confirmation, flight-plan step).
4. **Tank-mix calculator** with label-rate sanity checks.
5. **Imports/exports:** SmartFarm xlsx/KML import, shapefile export, farmOS sync.
6. **Docker self-host reference** and Cloudflare deploy template.
