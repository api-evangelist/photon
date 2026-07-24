# Photon (photon)

Photon Health is a United States prescription-infrastructure and e-prescribing (eRx) platform that lets digital-health companies embed prescribing, pharmacy selection, prescription routing, and fulfillment tracking into their clinical applications. Rather than an HL7 FHIR interface, Photon exposes a native GraphQL Clinical API covering patients, prescriptions, orders, pharmacies, the medication/treatment catalog, drug interaction screening, and benefit checks, secured with OAuth2 client-credentials (Auth0).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/photon/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/photon/refs/heads/main/apis.yml)

## Tags

- Healthcare
- United States
- e-Prescribing
- Pharmacy
- Prescription Routing
- GraphQL
- Clinical API
- Digital Health
- Benefit Check
- OAuth2

## Timestamps

- **Created:** 2026-07-24
- **Modified:** 2026-07-24

## APIs

### Photon Clinical API

Photon's native GraphQL Clinical API for managing patients, prescriptions, orders, pharmacies, the treatment/medication catalog, drug-drug and drug-allergy interaction screening, webhooks, and organization/user administration. A single `POST /graphql` endpoint secured with OAuth2 client-credentials (Auth0) bearer tokens.

- **Human URL:** [https://docs.photon.health/reference/clinical-api](https://docs.photon.health/reference/clinical-api)
- **Base URL:** `https://clinical-api.photon.health/graphql`

#### Tags

- GraphQL
- e-Prescribing
- Pharmacy

#### Properties

- [GraphQL Schema](graphql/photon-clinical-api-schema.json) — harvested verbatim via introspection
- [Documentation](https://docs.photon.health/docs/getting-started)
- [API Reference](https://docs.photon.health/reference/clinical-api)
- [Authentication](https://docs.photon.health/docs/authentication)

### Photon Patient Benefits API

Photon's GraphQL Patient Benefits API for managing patient benefits and enabling pharmacy benefit checks (coverage options, copay, and formulary) during the prescribing workflow. Served over the same GraphQL endpoint via mutations such as `createBenefit` and `generateCoverageOptions`.

- **Human URL:** [https://docs.photon.health/reference/patient-benefits-api](https://docs.photon.health/reference/patient-benefits-api)
- **Base URL:** `https://clinical-api.photon.health/graphql`

#### Tags

- GraphQL
- Benefit Check
- Coverage

#### Properties

- [GraphQL Schema](graphql/photon-clinical-api-schema.json) — harvested verbatim via introspection
- [Documentation](https://docs.photon.health/docs/benefit-check-documentation)
- [API Reference](https://docs.photon.health/reference/patient-benefits-api)
- [Authentication](https://docs.photon.health/docs/authentication)

## Authentication

OAuth2 **client-credentials** (Auth0). Token endpoint `https://auth.photon.health/oauth/token` (sandbox `https://auth.neutron.health/oauth/token`), audience `https://api.photon.health`. Machine-to-machine and user access tokens with prescription/order scopes (`read:patient`, `write:patient`, `read:prescription`, `write:prescription`, `read:order`, `write:order`). Not SMART-on-FHIR; Photon is not a FHIR server.

## Common Properties

- [Website](https://photonhealth.com/)
- [Developer Portal](https://docs.photon.health/)
- [Documentation](https://docs.photon.health/docs/getting-started)
- [API Reference](https://docs.photon.health/reference/clinical-api)
- [Getting Started](https://docs.photon.health/docs/getting-started)
- [Authentication](https://docs.photon.health/docs/authentication)
- [Sign Up / Onboard](https://photonhealth.com/onboard)
- [GitHub Organization](https://github.com/Photon-Health)
- [LinkedIn](https://www.linkedin.com/company/photonhealth)
- [Status Page](https://status.photon.health)
- [Trust Center](https://trust.photon.health)
- [Blog](https://photonhealth.com/blog)
- [Privacy Policy](https://photonhealth.com/privacy)
- [Terms of Service](https://photonhealth.com/terms)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
