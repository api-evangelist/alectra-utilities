# Alectra Utilities (alectra-utilities)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
