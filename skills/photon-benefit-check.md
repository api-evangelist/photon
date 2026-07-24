---
name: Run a patient benefit check
description: Generate coverage options and create a benefit for a patient using Photon's Patient Benefits API.
api: graphql/photon-clinical-api-schema.json
operations: [generateCoverageOptions, createBenefit, patient]
method: generated
source: graphql/photon-clinical-api-schema.json + docs.photon.health/docs/benefit-check-documentation
---

# Run a patient benefit check

Grounds an agent in the real GraphQL fields for Photon's Patient Benefits API (coverage, copay, formulary).

## Auth
- OAuth2 client-credentials Bearer token (audience `https://api.photon.health`) on `POST /graphql`.
- Requires `read:patient` / `write:patient`.

## Steps
1. **Resolve the patient** — `patient` query by `pat_` id to confirm the subject.
2. **Create the benefit** — `createBenefit` mutation to attach the patient's insurance/benefit context (member id, BIN, PCN, group).
3. **Generate coverage** — `generateCoverageOptions` mutation returns a `Coverage` with estimated out-of-pocket cost, alternative medications, pharmacy dispensing options, and insurance coverage details.

## Sandbox test data (verbatim, from docs)
- Patient ids: `pat_123`, `pat_456`
- Member id: `PCMSMEM001` (or empty `""` for the no-coverage case)
- BINs: `020321`, `610014`
- Pharmacy ids: `phr_01GA9HPV354YPQATCPCCE8D9N3`, `phr_01GA9HPXP2NQQFPTXZHHJ5QTR6`
- Medications: `Victoza Subcutaneous Solution Pen-injector 18 MG/3ML`, `Amoxicillin Oral Tablet 500 MG`

## Rules
- Run against the sandbox (`clinical-api.neutron.health`) with the test data above before production.
- `groupId` and `pcn` may be null.
