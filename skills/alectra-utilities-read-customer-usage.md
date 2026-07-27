---
name: Read an authorised Alectra customer's Green Button usage data
description: >-
  Confirm a customer's Connect My Data authorisation is still active, then walk from
  that authorisation to the customer's usage points, over Alectra Utilities' mandated
  Green Button (NAESB REQ.21 ESPI) surface. Read-only.
api: openapi/alectra-utilities-green-button-espi-openapi.json
operations:
  - findAuthorizations
  - getAuthorization
  - findUsagePoints
  - getUsagePoint
generated: '2026-07-27'
method: generated
---

# Read an authorised Alectra customer's Green Button usage data

## Before you start — this API is not self-serve

You cannot call Alectra Utilities' Connect My Data service by obtaining a key. There
is no developer portal, no published base URI, no sandbox and no documentation. The
sequence is:

1. Register as a third party at <https://alectrautilitiesonboarding.savagedata.com/>
   (hosted by Alectra's data custodian vendor, Savage Data Systems; it is a Blazor
   application and needs a real browser).
2. Accept the [Green Button Connect My Data Terms and Conditions of Access and Use](https://alectrautilities.com/green-button-connect-my-data-terms-and-conditions-access-and-use),
   which bind you to the Green Button Rules and Standards at greenbuttondata.org, to
   supplying a privacy policy and a cybersecurity policy to customers, and to using
   the data only for the purposes the customer expressly consented to.
3. Be approved by Alectra. Ontario has no accredited-data-recipient regime, so this is
   Alectra's own commercial and compliance decision, not a regulator's.
4. Only then does an individual customer authorise the connection in Alectra's Green
   Button portal, choosing the data and the time period.

Alectra issues your base URI and OAuth client credentials through that onboarding
relationship. Do not guess a host: every path on
`https://alectrautilitiesgbportal.savagedata.com/` HTTP 302 redirects to a customer
sign-in, including deliberately invented paths, so a 302 there tells you nothing.

## Auth

OAuth 2.0 Bearer token. `authorizationCode` for customer-consented data,
`clientCredentials` for your own registration-level calls. Send
`Authorization: Bearer <token>`. See `authentication/alectra-utilities-authentication.yml`.

## Steps

1. **List the consents you hold** — `findAuthorizations`
   (`GET /espi/1_1/resource/Authorization`). Page with `start-index` (1-indexed) and
   `max-results`; narrow with `updated-min` / `updated-max` as RFC 3339 instants to
   pick up consents that changed since your last sync.
2. **Check the consent is live** — `getAuthorization`
   (`GET /espi/1_1/resource/Authorization/{authorizationId}`). Stop if `status` is
   `0` (Revoked) or `2` (Denied); only `1` (Active) may be read. Also check
   `expires_at`. Keep `scope` — it is issued at consent time, not from a published
   catalogue — and keep `resourceURI`, which is where that customer's data lives.
3. **Find the metered points** — `findUsagePoints`
   (`GET /espi/1_1/resource/UsagePoint`). `ServiceCategory` `0` is electricity, `1`
   gas, `2` water; Alectra distributes electricity and bills water for some
   municipalities, so do not assume electricity.
4. **Read a specific point** — `getUsagePoint`
   (`GET /espi/1_1/resource/UsagePoint/{usagePointId}`). Raise `depth` to inline more
   of the related ESPI graph in one response.

## Rules

- **Everything is XML.** Responses are `application/atom+xml`: Atom feeds and entries
  (RFC 4287) wrapping ESPI resources in the `http://naesb.org/espi` namespace. There
  is no JSON representation. Follow `link rel="self"` / `rel="up"` to traverse.
- **No idempotency contract, and none needed** — every operation is a GET.
- **Errors are bare status codes.** No RFC 9457 problem details, no error body schema.
  `400` means a malformed parameter (check your RFC 3339 instants and 1-indexed
  `start-index`); `403` almost always means the token or the customer's consent, not a
  missing resource. See `errors/alectra-utilities-problem-types.yml`.
- **`202 Accepted` is not a failure** — the standard uses it for asynchronous
  preparation. Retry rather than treating it as an error.
- **No rate limits are published.** Be conservative and back off on 4xx/5xx.
- **This is personal data.** Consumption interval data for an identified retail
  customer. Use it only for the purpose the customer consented to, and stop reading
  the moment the Authorization is no longer Active.

## Caveat on grounding

The operation ids above come from the Green Button Alliance's own ESPI specification,
harvested verbatim into `openapi/` — the contract Ontario Regulation 633/21 obliges
Alectra to implement. Alectra publishes no specification of its own, and no Alectra
endpoint could be exercised anonymously to confirm the shape. Treat the first live
call against your issued base URI as the real verification step.
