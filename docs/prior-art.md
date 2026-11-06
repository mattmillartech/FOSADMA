# Prior art (surveyed 2026-11-06)

**Verdict:** nothing open-source covers ag spray/spread operations + checklists + tank mixes + compliance + a two-way agent interface. Start the core from a blank slate; cherry-pick parsers, patterns and integrations. No candidate is worth forking.

| Project | License | What it is | Use it for |
|---|---|---|---|
| [Open DroneLog](https://github.com/arpanghosh8453/open-dronelog) | AGPL-3.0 | DJI `.txt` / Litchi / Airdata log analyzer; Tauri desktop or Docker web (Axum REST + DuckDB + React); parser plugins via `parsers.json`. Camera-drone focus; no Agras/SmartFarm or KML import listed; no MCP | Optional companion for telemetry; parser-plugin pattern. Not a fork base |
| [DroneOpsCommand](https://github.com/BigBill1418/DroneOpsCommand) | MIT (per ecosyste.ms) | Self-hosted ops platform for US FAA Part 107 *camera* operators (FastAPI, React, Postgres, Celery, Ollama). Heavy (8 GB RAM minimum); not offline/PWA | Ideas only: mission entity model, report generation |
| [farmOS](https://docs.farmos.org/development/api) | GPL-2.0 | Farm record system with JSON:API, OAuth2, JSON Schema. Spray-record quick forms are still a [community request](https://farmos.discourse.group/t/spray-job-quick-form/1245). PHP/Drupal, not offline-first | Optional **sync target**: push application records as farmOS input logs |
| [dji-log-parser](https://github.com/lvauvillier/dji-log-parser) / [pydjirecord](https://pypi.org/project/pydjirecord/) | MIT | Parse DJI `.txt` logs to JSON/CSV/GeoJSON/KML. v13+ logs need a DJI developer API key to fetch decryption keychains | Telemetry ingest *if* Agras logs turn out to use this format (unverified) |
| [FieldPilot](https://github.com/Aryan221224/fieldpilot) | not verified | Hackathon prototype: spray-drone day planner, Open-Meteo weather windows, rule packs, tank-mix calculator | Idea source: the tank-mix trap (per-hectare label dose vs ~20 L drone carrier volume) |
| dronelytics-mcp, aviation-weather-mcp | MIT / small | MCP servers for US airspace and METAR/TAF | Pattern reference for MCP tool design |
| [Aerobridge](https://github.com/openskies-sh/aerobridge) | — | Drone ops management server; **archived** Dec 2023 | Nothing |

Commercial references that set the feature bar (closed): AcreConnect, Agri Flight Logs, DroneBundle, FlyFreely, DJI SmartFarm. The shared shape is job → field → pilot certificate valid on date → aircraft → product/rate → flight log → weather at application.

## Agras data access (constraint on integration)

- No automated third-party export. [FlyFreely's import path](https://knowledge.flyfreely.io/importing-agras-data-into-flyfreely) is a manual SmartFarm Web → `.xlsx` export.
- [Airdata](https://app.airdata.com/wiki/Help/DJI+AGRAS) receives Agras flights from SmartFarm as KML, without detailed telemetry.
- DJI states Agras data stays on the controller and drone unless the operator opts in to DJI servers ([AgWeb](https://www.agweb.com/news/business/technology/dji-launches-new-ag-spray-drones)).
- Field boundaries go *into* the controller as shapefiles ([PIX4Dfields export](https://support.pix4d.com/hc/en-us/articles/360019956578)).

**Consequence:** FOSADMA cannot control the aircraft or pull live telemetry. Plan for manual and agent-assisted logging, SmartFarm xlsx/KML import, and shapefile export of planned boundaries.
