---
name: Sync a patient into Photon
description: Create a patient record in Photon and read it back so downstream prescribing/ordering can reference it.
api: graphql/photon-clinical-api-schema.json
operations: [createPatient, patient, patients]
method: generated
source: graphql/photon-clinical-api-schema.json + docs.photon.health/docs/sync-patients
---

# Sync a patient into Photon

Grounds an agent in the real GraphQL fields for onboarding a patient before prescribing or ordering.

## Auth
- Get an OAuth2 client-credentials access token from `https://auth.photon.health/oauth/token` (sandbox: `https://auth.neutron.health/oauth/token`) with `audience=https://api.photon.health` and `grant_type=client_credentials`.
- Send it as `Authorization: Bearer <token>` on `POST https://clinical-api.photon.health/graphql`.
- Requires scope `write:patient` (create) and `read:patient` (read back).

## Steps
1. **Create the patient** — call the `createPatient` mutation with the patient's name, dateOfBirth, sex, and contact fields. It returns a `CreatePatientResult` carrying the new `pat_`-prefixed id.
2. **Read it back** — call the `patient` query with that id to confirm the record and hydrate `treatmentHistory` / `benefits`.
3. **List/deduplicate** — use the `patients` query with filter arguments to check for an existing record before creating a duplicate.

## Rules
- IDs are opaque, type-prefixed (`pat_...`). Never construct them.
- No idempotency key is supported — dedupe with `patients` before `createPatient`.
- Errors arrive in the GraphQL `errors[]` array (`extensions.code`); a 401 means the token is missing/expired.
