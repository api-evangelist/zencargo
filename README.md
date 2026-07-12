# Zencargo (zencargo)

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
