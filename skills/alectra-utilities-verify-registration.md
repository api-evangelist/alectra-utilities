---
name: Verify your third-party registration with Alectra's Green Button data custodian
description: >-
  After Alectra approves your third-party registration, read back the
  ApplicationInformation record that carries your OAuth client identity, redirect URIs
  and application status before attempting any customer-data call. Read-only.
api: openapi/alectra-utilities-green-button-espi-openapi.json
operations:
  - findApplicationInformations
  - getApplicationInformation
generated: '2026-07-27'
method: generated
---

# Verify your third-party registration with Alectra's Green Button data custodian

`ApplicationInformation` is the ESPI resource that represents *you* — the registered
third party — inside the data custodian. Read it first: if its status fields are not
right, every customer-data call will fail with a `403` that looks like a token problem
but is actually a registration problem.

## Prerequisites

Registration submitted at <https://alectrautilitiesonboarding.savagedata.com/> and
approved by Alectra, with a base URI and OAuth client credentials issued to you
through that relationship. Alectra publishes neither publicly.

## Auth

OAuth 2.0. Use the `clientCredentials` flow for these registration-level calls —
they are about your application, not about a customer's data, so a customer
authorisation is not involved.

## Steps

1. **List** — `findApplicationInformations`
   (`GET /espi/1_1/resource/ApplicationInformation`). Supports `start-index`,
   `max-results`, `depth`, and the `published-min` / `published-max` /
   `updated-min` / `updated-max` RFC 3339 filters.
2. **Read your record** — `getApplicationInformation`
   (`GET /espi/1_1/resource/ApplicationInformation/{applicationInformationId}`).

## What to check on the record

- `dataCustodianApplicationStatus` and `thirdPartyApplicationStatus` — your standing
  with the custodian. The specification does not enumerate these integers; confirm the
  expected values with Alectra during onboarding rather than guessing.
- `client_id` / `client_name` / `client_secret` — the OAuth identity to use.
- `redirect_uri[]` — must exactly match the callback you send to the authorisation
  endpoint, or the customer consent flow will fail before it starts.
- `scope[]` and `grant_types[]` — what you were actually granted. Do not assume: the
  harvested contract carries an **empty** OAuth scopes map, so the operative scope
  values are whatever the custodian issued to you.
- `thirdPartyApplicationType` — `1` Web, `2` Desktop, `3` Mobile, `4` Device.
- `dataCustodianId` — identifies the custodian instance you are talking to. Alectra's
  Green Button surfaces are operated by the vendor Savage Data Systems, so expect a
  vendor-operated custodian rather than an Alectra-run one.

## Rules

- Responses are `application/atom+xml` (Atom entry wrapping the ESPI resource); there
  is no JSON.
- Both declared error responses are bare status codes — `400` malformed request,
  `403` not permitted. There is no problem-details body to read.
- Never log or persist `client_secret`.

## Caveat on grounding

These operation ids come from the Green Button Alliance ESPI specification harvested
into `openapi/`, which is the standard Alectra is mandated to implement. Alectra
authors no specification and exposes no anonymous endpoint, so the live contract can
only be confirmed once you hold an issued base URI.
