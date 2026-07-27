# Alectra Utilities (alectra-utilities)

Alectra Utilities Corporation is Ontario's second-largest municipally owned electricity distributor and one of the largest local distribution companies (LDCs) in Canada, serving roughly one million customers across seventeen communities in the Greater Toronto and Hamilton Area and the Golden Horseshoe — Alliston, Aurora, Barrie, Beeton, Bradford West Gwillimbury, Brampton, Guelph, Hamilton, Markham, Mississauga, Penetanguishene, Richmond Hill, Rockwood, St. Catharines, Thornton, Tottenham and Vaughan. It also bills water and wastewater/stormwater on behalf of several of those municipalities, and runs the GRE&T Centre for grid innovation. It sits squarely in the wires and metering layer of the Canadian value chain: it does not generate, it does not operate the market (the IESO does), and it is owned by its municipal shareholders rather than by investors — the Crown/municipal ownership pattern that dominates Canadian electricity. Its API posture exists only because a regulator created it. Ontario Regulation 633/21 (Energy Data) requires every Ontario electric and gas utility to implement Green Button Download My Data and Connect My Data to the NAESB REQ.21 ESPI v3.3 standard and to obtain Green Button Alliance certification, with an implementation deadline of 1 November 2023. Alectra publishes a Green Button page displaying GBA Certified DMD and CMD marks, a Green Button Connect My Data Terms and Conditions of Access and Use citing O. Reg. 633/21 by name, a live customer Green Button portal, and a live third-party registration and onboarding site — all three hosted by its data custodian vendor, Savage Data Systems, not by Alectra. What Alectra does not publish is any of the things that would let an outsider verify the implementation: there is no developer portal, no API documentation, no base URI, no OpenAPI, no scopes and no OAuth metadata anywhere on alectrautilities.com or on the portal host.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/alectra-utilities/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/alectra-utilities/refs/heads/main/apis.yml)

## Tags

- Energy
- Canada
- Utilities
- Electricity
- Ontario
- Green Button
- Smart Metering
- Energy Data
- Grid
- Municipal Utility
- ESPI

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### Alectra Utilities Green Button Connect My Data (CMD) API

Alectra's mandated Green Button Connect My Data service, required of every Ontario electric and gas utility by Ontario Regulation 633/21 (Energy Data) and implemented to the NAESB REQ.21 Energy Services Provider Interface (ESPI) v3.3 standard. It lets an Alectra account holder authorise the ongoing, secure transfer of their electricity usage and billing data, in the standardised Green Button XML format, to a third party that Alectra has approved. Access is not self-serve: a developer must complete Alectra's third-party registration and onboarding, accept the Green Button Connect My Data Terms and Conditions of Access and Use, and undertake to follow the Green Button Rules and Standards. No base URI is recorded because Alectra publishes none — the endpoint is disclosed to approved third parties through onboarding.

- **Human URL:** [https://alectrautilities.com/green-button-connect-my-data-terms-and-conditions-access-and-use](https://alectrautilities.com/green-button-connect-my-data-terms-and-conditions-access-and-use)
- **Base URL:** not published

#### Tags

- Green Button
- Connect My Data
- ESPI
- Energy Data
- Usage
- Billing
- Consent
- Ontario
- Canada

#### Properties

- [OpenAPI](openapi/alectra-utilities-green-button-espi-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://alectrautilities.com/green-button)
- [Documentation](https://alectrautilities.com/green-button-connect-my-data-terms-and-conditions-access-and-use)
- [Privacy Policy](https://alectrautilities.com/green-button-privacy-policy)
- [Registration](https://alectrautilitiesonboarding.savagedata.com/)
- [Portal](https://alectrautilitiesgbportal.savagedata.com/)
- [Documentation](https://www.greenbuttondata.org/cmd.html)
- [Documentation](https://www.greenbuttonalliance.org/certification)

## Mandate Posture

| Field | Value |
| --- | --- |
| Mandate regime | `green-button-ontario` — Ontario Regulation 633/21 (Energy Data) |
| Mandate status | `live-claimed-unverified` |
| Data standard | Green Button / NAESB REQ.21 ESPI v3.3 |
| Consumer data API | Yes — Green Button Connect My Data, consent + approval gated |
| Market data open | No — Ontario grid and market data belongs to the IESO and the OEB |
| Access gate | `application-approval` — third-party registration, terms acceptance, Alectra approval |
| Auth model | OAuth 2.0 authorization code per the Green Button CMD/ESPI profile (standard's model; unverified on Alectra) |
| Home market | Canada |

Ontario did what no other Canadian province did and what the United States never did: it made Green Button compulsory by regulation, named the standard, named the certifier and set a date. Alectra responded the way a municipally owned wires company responds to a compliance obligation — it bought the capability. Both public Green Button surfaces run on `savagedata.com` under Alectra branding. The mandate produced a service, not a product: there is a documented right to the data and a documented way to apply for it, and nothing resembling a developer experience.

Every path on the Green Button portal host — including a deliberately invented control path — returns HTTP 302 to a customer sign-in, so no ESPI endpoint could be confirmed. Full probe log with HTTP status for every URL is in [`review.yml`](review.yml).

## Common Properties

- [Website](https://alectrautilities.com/)
- [Documentation](https://alectrautilities.com/green-button)
- [Privacy Policy](https://alectrautilities.com/green-button-privacy-policy)
- [Terms of Service](https://alectrautilities.com/green-button-connect-my-data-terms-and-conditions-access-and-use)
- [Registration](https://alectrautilitiesonboarding.savagedata.com/)
- [Portal](https://myalectra.alectrautilities.com/)
- [LinkedIn](https://www.linkedin.com/company/alectra-utilities)

## Maintainers

- Kin Lane — kin@apievangelist.com
