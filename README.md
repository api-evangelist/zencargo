# Zencargo (zencargo)

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Zencargo is a digital freight forwarder and supply-chain visibility platform for ocean, air, road, and rail shipments. Its **GraphQL API** gives enterprise customers programmatic access to bookings, shipment tracking and voyage milestones, purchase orders, products, packing lists, and accounts, plus HTTP webhooks for booking and purchase-order events.

## Access model (read this first)

The Zencargo API is **not openly self-service**. It is a customer-provisioned GraphQL API:

- **You must be a Zencargo customer.** Your account manager provisions a dedicated **staging** and **production** endpoint of the form `https://{accountReference}.api.{environment}.zencargo.com/graphql` (for example `https://zawesome.api.production.zencargo.com/graphql`). There is no single shared public base URL.
- **All operations are `POST /graphql`.** GraphQL — one endpoint, operation defined in the request body. There is no REST resource layout.
- **Authentication is HTTP Basic.** You generate an API Key (an ID/UUID + secret) in the Zencargo app under *Profile Settings > API Keys*. Join them as `keyId:secret`, base64-encode, and send `Authorization: Basic <base64>`.
- **A live GraphQL gateway exists** at `https://graphql.zencargo.com/` (Apollo Federation / Apollo Router) and at each tenant subdomain, but both reject unauthenticated introspection. The public schema in this repo is modeled from the official documentation at [api-docs.zencargo.com](https://api-docs.zencargo.com/), not from an authenticated introspection dump.

Everything published here that is not directly quoted from the public docs is marked as **modeled**. The GraphQL SDL is a grounded, representative schema (documented type/field/enum names, trimmed field sets on the largest objects).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/zencargo/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/zencargo/refs/heads/main/apis.yml)

## Tags

- Freight Forwarding
- Supply Chain
- Logistics
- Ocean Freight
- Shipment Tracking
- Bookings
- Supply Chain Visibility
- Freight
- SaaS
- GraphQL

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

All GraphQL surfaces below share the single per-tenant endpoint `https://{accountReference}.api.production.zencargo.com/graphql`.

### Zencargo Bookings API

Query bookings by Zencargo reference and retrieve booking details: cargo, consignor/consignee, forwarder, incoterms, load type, mode of transport, bills of lading, required delivery date, and attached booking documents (assetUrl for download).

- **Human URL:** [https://api-docs.zencargo.com/download_booking_documents/](https://api-docs.zencargo.com/download_booking_documents/)
- **Base URL:** `https://{accountReference}.api.production.zencargo.com/graphql`

#### Tags

- Bookings
- Freight
- GraphQL

#### Properties

- [Documentation](https://api-docs.zencargo.com/download_booking_documents/)
- [API Reference](https://api-docs.zencargo.com/object/booking/)
- [GraphQL](graphql/zencargo.graphql) — [GraphQL SDL](https://spec.graphql.org/)
- [Postman Collection](collections/zencargo.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zencargo.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Zencargo Shipment Visibility API

Track shipment progress through scheduled carriage legs, cargo journey details (estimated/actual collection and delivery), and voyage milestones (collected, gate in, cargo aboard, departed/arrived terminal, delivered) with estimated and actual timestamps for predictive ETAs.

- **Human URL:** [https://api-docs.zencargo.com/object/voyagemilestone/](https://api-docs.zencargo.com/object/voyagemilestone/)
- **Base URL:** `https://{accountReference}.api.production.zencargo.com/graphql`

#### Tags

- Shipment Tracking
- Supply Chain Visibility
- Milestones

#### Properties

- [Documentation](https://api-docs.zencargo.com/object/scheduledleg/)
- [API Reference](https://api-docs.zencargo.com/object/voyagemilestone/)
- [GraphQL](graphql/zencargo.graphql) — [GraphQL SDL](https://spec.graphql.org/)
- [Postman Collection](collections/zencargo.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zencargo.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Zencargo Purchase Orders API

Create, query, update, close, and delete purchase orders and their ordered line items and SKU-level Lots. Keeps an ERP in sync with Zencargo as the source of truth for pre-booking PO data.

- **Human URL:** [https://api-docs.zencargo.com/query_purchase_orders/](https://api-docs.zencargo.com/query_purchase_orders/)
- **Base URL:** `https://{accountReference}.api.production.zencargo.com/graphql`

#### Tags

- Purchase Orders
- Supply Chain
- Lots

#### Properties

- [Documentation](https://api-docs.zencargo.com/create_purchase_orders/)
- [API Reference](https://api-docs.zencargo.com/object/purchaseorder/)
- [GraphQL](graphql/zencargo.graphql) — [GraphQL SDL](https://spec.graphql.org/)
- [Postman Collection](collections/zencargo.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zencargo.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Zencargo Products API

Manage the product catalog - create, query, update, archive, and unarchive products (and core products with characteristics, dimensions, weights, tariff codes, and pricing), plus product categories and attributes.

- **Human URL:** [https://api-docs.zencargo.com/query_product/](https://api-docs.zencargo.com/query_product/)
- **Base URL:** `https://{accountReference}.api.production.zencargo.com/graphql`

#### Tags

- Products
- Catalog
- SKU

#### Properties

- [Documentation](https://api-docs.zencargo.com/create_product/)
- [API Reference](https://api-docs.zencargo.com/object/coreproduct/)
- [GraphQL](graphql/zencargo.graphql) — [GraphQL SDL](https://spec.graphql.org/)
- [Postman Collection](collections/zencargo.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zencargo.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Zencargo Packing Lists API

Query packing lists for a booking (`BOOKING_REFERENCE`) or a specific cargo (`CARGO_ID`), returning per-container lines with the Lot and Product behind each packed item.

- **Human URL:** [https://api-docs.zencargo.com/query_packing_lists/](https://api-docs.zencargo.com/query_packing_lists/)
- **Base URL:** `https://{accountReference}.api.production.zencargo.com/graphql`

#### Tags

- Packing Lists
- Cargo
- FCL

#### Properties

- [Documentation](https://api-docs.zencargo.com/query_packing_lists/)
- [API Reference](https://api-docs.zencargo.com/object/packinglist/)
- [GraphQL](graphql/zencargo.graphql) — [GraphQL SDL](https://spec.graphql.org/)
- [Postman Collection](collections/zencargo.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zencargo.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Zencargo Accounts and Locations API

Retrieve account details by UUID and search assignable accounts (customers, suppliers, manufacturers) and their locations to resolve the origin, destination, and manufacturer IDs referenced when creating purchase orders and bookings.

- **Human URL:** [https://api-docs.zencargo.com/query_accounts_and_locations/](https://api-docs.zencargo.com/query_accounts_and_locations/)
- **Base URL:** `https://{accountReference}.api.production.zencargo.com/graphql`

#### Tags

- Accounts
- Locations
- Network

#### Properties

- [Documentation](https://api-docs.zencargo.com/query_accounts_and_locations/)
- [API Reference](https://api-docs.zencargo.com/object/account/)
- [GraphQL](graphql/zencargo.graphql) — [GraphQL SDL](https://spec.graphql.org/)
- [Postman Collection](collections/zencargo.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/zencargo.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Zencargo Webhooks

Outbound HTTP webhooks. Zencargo POSTs a JSON payload (`topic`, `targetType`, `targetId`) to a customer-registered HTTPS callback URL when events such as `BOOKING_CREATED` occur, signed with a base64 `Zencargo-Hmac-SHA256` header for verification. This is server-to-endpoint HTTP push, **not** a WebSocket or GraphQL subscription. Subscriptions are configured in the Zencargo app, not via the API.

- **Human URL:** [https://api-docs.zencargo.com/webhooks/](https://api-docs.zencargo.com/webhooks/)

#### Tags

- Webhooks
- Events
- Notifications

#### Properties

- [Documentation](https://api-docs.zencargo.com/webhooks/)

## Common Properties

- [Domain Security](security/zencargo-domain-security.yml)
- [Authentication](authentication/zencargo-authentication.yml)
- [GitHub Organization](https://github.com/zencargo)
- [LinkedIn](https://www.linkedin.com/company/zencargo)
- [Website](https://www.zencargo.com/)
- [Documentation](https://api-docs.zencargo.com/)
- [Plans](plans/zencargo-plans-pricing.yml)
- [Rate Limits](rate-limits/zencargo-rate-limits.yml)
- [Fin Ops](finops/zencargo-finops.yml)
- [Blog](https://www.zencargo.com/resources/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
