# Canada regulatory notes (rule-pack inputs)

> Not legal advice. Compiled 2026-11-06 from primary sources on tc.canada.ca and laws-lois.justice.gc.ca (Canadian Aviation Regulations, consolidated to 2026-10-19, last amended 2026-06-17). Verify before relying; the rule pack must store a source link and verification date for every rule.

## Operation class

- The Phase 2 amendments to CARs Part IX took effect **2025-11-04**: a medium RPAS (over 25 kg up to 150 kg) can fly within visual line of sight under *advanced* operations without a Special Flight Operations Certificate ([TC summary of 2025 changes](https://tc.canada.ca/en/aviation/drone-safety/2025-summary-changes-canada-drone-regulations)).
- An RPAS Operator Certificate (RPOC) is for **BVLOS**; it is not needed for medium VLOS operations.

## Aircraft: Safety Assurance Declaration is the gate

A medium drone without a Safety Assurance Declaration cannot be flown in Canadian airspace ([Drone Zone, Dec 2025](https://tc.canada.ca/en/aviation/drone-safety/drone-zone/drone-zone-issue-5-december-2025)). Check the [TC declared-drone list](https://tc.canada.ca/en/aviation/drone-safety/learn-rules-you-fly-your-drone/choosing-right-drone-advanced-complex-operations); declarations can be invalidated after listing, so make this a **recurring** check.

As of 2026-11-06 the DJI Agras T50 is listed with declarations for Standard 922.04 (controlled airspace) and 922.08 (containment) only, per [Standard 922](https://tc.canada.ca/en/corporate-services/acts-regulations/list-regulations/canadian-aviation-regulations-sor-96-433/standards/standard-922-rpas-safety-assurance):

| CAR 901.69 case (medium, VLOS) | Standard 922 declaration | T50 listed? |
|---|---|---|
| (e) more than 500 ft (152.4 m) from anyone not involved | 922.08 | Yes |
| (h) in controlled airspace | 922.04 + 922.08 | Yes (plus NAV Drone/ATC authorization) |
| (f)/(g) closer than 500 ft | 922.07 pre-validated declaration | No |

Checklist rule that follows: record a confirmation that the whole flight, including transit, keeps at least 152.4 m from uninvolved persons. The aircraft must also be registered with TC.

## Pilot: certificate and recency

- Pilot Certificate – Advanced Operations required.
- **Recency, CAR 901.65:** within the 24 months before a flight the holder must have been issued the certificate, or passed a TC exam, completed a flight review, or completed a recurrent training activity under Standard 921.04. A dated record of those activities must be kept at least 24 months. **CAR 901.66:** the certificate and recency documentation must be easily accessible during the operation.
- Qualifying recurrent training: a TC-endorsed safety seminar, a flight-school recurrent training program, or a TC-endorsed self-paced study program. TC publishes a free [2026–2027 self-paced study program](https://tc.canada.ca/en/aviation/drone-safety/drone-pilot-licensing/drone-pilot-study-resources/recency-requirements-self-paced-study-program) (questions 1–30 for advanced pilots; sign, date and keep the copy 24 months; not submitted to TC).
- TC does not track recency and the pilot portal does not show it. **FOSADMA design:** a recency log, a pre-flight gate that blocks when the 24-month window has lapsed, and a reminder around month 22.

## Pesticides

Health Canada/PMRA policy (2026-06-30): drones may apply products already registered for **aerial** application, following the aerial label directions (volume, rate, droplet size, buffers). Products without aerial registration still need a label amendment ([announcement](https://www.canada.ca/en/health-canada/news/2026/06/government-of-canada-approves-new-technology-to-support-farmers-and-a-more-sustainable-use-of-pest-management-products.html)). **Provincial applicator licensing (Ontario) is not yet researched** and must be before any compliance rule ships.

## Airspace and NAV CANADA

NAV Drone has no public API. NAV CANADA selected Indra in May 2026 to build rFIMS for third-party RPAS service providers, with initial capability expected around 2029 ([Indra](https://www.indragroup.com/en/news/nav-canada-chooses-indra-group-as-its-technological-partner-for-the-safe-integration-of-drones-into-canadian-airspace)). Until then: a mandatory checklist step "flight plan / authorization filed or confirmed", with a deep link and a captured reference number as evidence.
