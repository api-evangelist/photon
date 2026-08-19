---
name: Onboard to the Photon developer sandbox
description: >-
  Walk a user through creating a free Photon developer sandbox account using the
  public website API, then hand off to the Clinical API. This is the one Photon
  onboarding path the provider explicitly permits an agent to complete, and only
  with the user's explicit consent.
api: openapi/photon-website-api-openapi.json
operations:
  - getOnboardingSchema
  - createOrResumeOnboardingSession
  - saveOnboardingStep
  - submitOnboardingSession
---

# Onboard to the Photon developer sandbox

## When to use this

The user wants to evaluate Photon or start building against the Clinical API.

**Read this boundary before you act.** Photon publishes an agent policy in
[llms.txt](https://photonhealth.com/llms.txt) and it is narrow:

> Agents may help a user evaluate Photon and may complete the developer sandbox
> path with explicit user consent. The developer sandbox is free, does not
> require payment, and cannot send real prescriptions. Prescriber access requires
> verification. Clinic, enterprise, platform, and other production paths are
> sales-led or handoff-led and should expect human follow-up.

So: **`developer` is the only path you may complete.** For `prescriber`,
`clinic`, `enterprise`, `platform` or `other`, gather the user's intent and hand
off to a human — do not submit the session.

Do not call this flow without explicit user consent. `submitOnboardingSession`
sends the user's name, email and company to Photon and triggers follow-up. It is
not reversible by you.

## Steps

### 1. Read the schema before assuming any field

`getOnboardingSchema` — `GET https://photonhealth.com/api/onboarding/schema`

Unauthenticated, no consequence. It returns an `allPaths` tree: every path, its
`mode`, its steps, and every field with type, label, requiredness and select
options. Photon's own guidance is "Start with the onboarding schema."

Confirm `developer` still reports `mode: self_serve`. Field definitions change —
read them from this response, never from memory or from this document.

### 2. Create or resume the session

`createOrResumeOnboardingSession` — `POST /api/onboarding/sessions`

Accepts anonymous access. The response carries the onboarding lead token. Persist
it and send it on every later call as either:

- header `x-onboarding-lead-token`, or
- cookie `photon_onboarding_lead`

Create-or-resume means a repeat call resumes rather than duplicating — but this
is *not* a general idempotency guarantee, and no idempotency key is accepted
anywhere on this API (`conventions/photon-conventions.yml`).

### 3. Save each step as you collect it

`saveOnboardingStep` — `PATCH /api/onboarding/sessions/{sessionId}`

Save incrementally as the user answers. Collect values from the user; never
invent an NPI, phone number, practice name or address.

Errors: `400` malformed payload, `401` lead token sent but rejected (re-run step
2). Neither declares a response schema, so do not depend on the error body shape
— see `errors/photon-problem-types.yml`.

### 4. Confirm, then submit

`submitOnboardingSession` — `POST /api/onboarding/sessions/{sessionId}/submit`

**Stop and get explicit confirmation first.** Show the user exactly what will be
sent.

On `422` the body is a `ValidationErrorEnvelope` with inline per-field errors.
Read the named fields, re-prompt the user for those specific fields, and save
them via step 3 before resubmitting. Do not blind-retry — nothing here is
idempotent.

### 5. Hand off to the sandbox

After submission the user provisions credentials in the Neutron sandbox:

- App: <https://app.neutron.health>
- GraphQL: `POST https://clinical-api.neutron.health/graphql`
- Token: `POST https://auth.neutron.health/oauth/token`, audience `https://api.neutron.health`

The sandbox behaves like production except it cannot send a prescription to a
pharmacy. `write:prescription` is issued only to verified prescribers through a
user access token, so an M2M agent token cannot prescribe on either environment —
by design.

## Guardrails

- Complete only the `developer` path. Hand off every other path to a human.
- Never call `submitOnboardingSession` without explicit user consent.
- Never fabricate NPI, licence, or practice data.
- Photon does not support controlled substances; do not imply otherwise.
- No published rate limits exist (`rate-limits/photon-rate-limits.yml`) — pace
  requests conservatively and back off on any `429`.

## References

- Contract: `openapi/photon-website-api-openapi.json`
- Agent policy + access classes: `agentic-access/photon-agentic-access.yml`
- Access paths and what each costs: `plans/photon-plans-pricing.yml`
- Errors: `errors/photon-problem-types.yml`
- Sandbox environment detail: `sandbox/photon-sandbox.yml`
