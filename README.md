# FOSADMA

**Free, Open-Source Agricultural Drone Management App** — a self-hostable, offline-capable app for running agricultural drone operations (spraying, spreading, mapping, surveying), with a first-class two-way **AI-agent interface**.

> **Status: planning only.** There is no code yet. Everything in this repo is a tentative design, open to change. Nothing here is legal, regulatory, agronomic or flight-safety advice; verify every rule against its primary source before relying on it.

## Why

Agricultural drone operators juggle many things outside the flight controller: regulatory checks, pre-flight checklists, weather go/no-go, tank-mix preparation, product and label records, pilot and aircraft compliance, maintenance, and an application record. Existing options are closed commercial products, camera-drone log tools, or hackathon prototypes. See [docs/prior-art.md](docs/prior-art.md).

## Principles (tentative)

1. **The drone maker's software stays primary for everything it does** (field mapping, route planning, flight control, on-aircraft logs). FOSADMA covers everything else and *references* those jobs and exports. It never controls the aircraft and never competes with the flight app.
2. **Agents are first-class users.** An OpenAPI-first REST API plus a remote MCP server, so any assistant can check weather, walk the operator through the checklist with prompt cards, help prepare the payload, and log the result. See [docs/architecture.md](docs/architecture.md).
3. **Go/no-go is always a human (pilot) confirmation.** Agents gather and present; they never decide.
4. **Every write records who made it** (human or agent identity) in an append-only audit log.
5. **Offline-first installable PWA** (desktop and mobile). No Firebase/Firestore.
6. **Self-hostable on free services or private hardware**, with templates and instructions for each. See the Cloudflare free-plan analysis in the architecture doc.
7. **Domain knowledge as versioned, cited data, not code:** aircraft spec packs, checklist templates, jurisdiction rule packs, product/label library.
8. **Jurisdiction-pluggable.** Canada (Ontario) is the first rule pack because that is where the author operates; the model must not hard-code it.

## Documents

| Doc | Contents |
|---|---|
| [docs/prior-art.md](docs/prior-art.md) | Existing projects evaluated; fork vs cherry-pick vs blank slate |
| [docs/architecture.md](docs/architecture.md) | Agent interface, data model sketch, offline/sync, deployment targets, Cloudflare free-plan feasibility |
| [docs/canada-regulatory-notes.md](docs/canada-regulatory-notes.md) | Canadian rules relevant to medium (25–150 kg) drones, pilot recency, as rule-pack inputs |
| [docs/roadmap.md](docs/roadmap.md) | Open questions and proposed first milestones |

## License

[AGPL-3.0](LICENSE). It keeps hosted forks open (network users can get the source) and permits reuse of AGPL and MIT components.

## Contributing

Issues and design discussion are welcome, especially from operators, regulators' guidance readers, and people with real DJI Agras data exports.
