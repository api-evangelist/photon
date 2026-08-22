# Photon (photon)

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
