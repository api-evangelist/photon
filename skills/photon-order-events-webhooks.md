---
name: Subscribe to Photon order events
description: Register and manage a webhook endpoint to receive Photon order lifecycle events (CloudEvents 1.0).
api: graphql/photon-clinical-api-schema.json
operations: [createWebhookConfig, webhooks, webhook, updateWebhookConfig, deleteWebhookConfig]
method: generated
source: graphql/photon-clinical-api-schema.json + docs.photon.health/docs/order-events
---

# Subscribe to Photon order events

Grounds an agent in the real GraphQL fields for configuring order-event webhooks and the events they deliver.

## Auth
- OAuth2 client-credentials Bearer token (audience `https://api.photon.health`) on `POST /graphql`.

## Steps
1. **Register the endpoint** — `createWebhookConfig` mutation with your HTTPS callback URL; it returns the new webhook config id.
2. **Verify** — `webhooks` query lists configs; `webhook` fetches one by id.
3. **Handle deliveries** — Photon POSTs CloudEvents 1.0 envelopes to your URL. Verify the signature (see docs "Signature Verification") before trusting the payload.
4. **Maintain** — `updateWebhookConfig` / `deleteWebhookConfig` to rotate or remove endpoints.

## Events delivered
- `photon:order:created` — an order has been created
- `photon:order:placed` — sent to a pharmacy
- `photon:order:fulfillment` — fulfillment status update
- `photon:order:completed` — picked up or delivered
- `photon:order:canceled` — canceled
- `photon:order:rerouted` — routed to a different pharmacy

## Envelope (CloudEvents 1.0)
`id`, `type`, `specversion` (1.0), `datacontenttype` (application/json), `time`, `subject` (order id), `source` (org), `data`.

## Rules
- Always verify the webhook signature; treat unsigned/failed-verification payloads as untrusted.
- Correlate with the `order` query using the `subject` id for authoritative order state.
