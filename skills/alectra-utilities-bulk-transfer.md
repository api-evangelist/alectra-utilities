---
name: Pull a Green Button bulk transfer from Alectra's data custodian
description: >-
  Retrieve a batch of ESPI resources by bulk id, handling the asynchronous 202 case,
  over Alectra Utilities' mandated Green Button surface. Read-only.
api: openapi/alectra-utilities-green-button-espi-openapi.json
operations:
  - downloadBulkData
generated: '2026-07-27'
method: generated
---

# Pull a Green Button bulk transfer from Alectra's data custodian

Connect My Data has two rhythms: read a customer's resources one at a time, or pull a
prepared batch. This skill is the batch path — the right one for a nightly sync across
many authorised customers instead of a per-customer walk.

## Prerequisites

An approved third-party registration with Alectra (see
`alectra-utilities-verify-registration.md`), an issued base URI, OAuth credentials,
and a `bulkId` supplied by the data custodian. Nothing here is guessable: Alectra
publishes no base URI, and the bulk id is assigned by the custodian.

## Step

**`downloadBulkData`** — `GET /espi/1_1/resource/Batch/Bulk/{bulkId}`

Query parameters: `published-min`, `published-max`, `updated-min`, `updated-max`
(RFC 3339 instants), `start-index` (1-indexed), `max-results`, `depth`.

## Handling the response

- **`200`** — an Atom feed (`application/atom+xml`) whose entries carry the ESPI
  resources. Page through with `start-index` + `max-results` until the feed returns no
  further entries; do not assume a total count is published.
- **`202`** — *Accepted, not an error.* The custodian is preparing the batch. Wait and
  re-request the same `bulkId` with backoff. Treating a 202 as a failure is the most
  common way to break a Green Button batch integration.
- **`400`** — malformed parameter. Check the RFC 3339 instants and that `start-index`
  is 1-indexed, not 0-indexed.
- **`403`** — your token, your registration status, or a customer authorisation that
  is no longer Active. It is not a "not found".

## Rules

- Use `updated-min` to make each run incremental — pull only what changed since the
  last successful sync — rather than re-downloading the whole batch.
- No idempotency key exists and none is needed: this is a GET, safe to repeat.
- No rate limits are published anywhere. Serialise your requests and back off.
- Everything is Atom + ESPI XML in the `http://naesb.org/espi` namespace. There is no
  JSON representation.
- A bulk feed can contain data for many identified retail customers. Every record in
  it is only usable for the purpose that customer consented to, and only while their
  Authorization remains Active — re-check with `getAuthorization` rather than trusting
  the batch.

## Caveat on grounding

`downloadBulkData` is defined in the Green Button Alliance ESPI specification
harvested into `openapi/` — the contract Ontario Regulation 633/21 obliges Alectra to
implement. Alectra publishes no specification and no reachable endpoint, so the live
behaviour (particularly how long a 202 persists) must be confirmed against your issued
base URI.
