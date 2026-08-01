---
name: Sync an API definition into a ReadMe project
description: Validate an OpenAPI definition and upload/update it in a ReadMe project's API Reference.
api: ReadMe API (v2) — https://api.readme.com/v2
operations: [validateApi, getApis, createApi, updateApi]
generated: '2026-07-20'
method: generated
source: https://docs.readme.com/main/reference/readme-api
---

# Sync an API definition into a ReadMe project

Use the ReadMe API v2 to publish or update an OpenAPI definition in your project's
API Reference. All calls go to `https://api.readme.com/v2` with
`Authorization: Bearer <README_API_KEY>`.

## Steps

1. **Validate the definition** — `validateApi`. Send your OpenAPI/Swagger document.
   Fix any problems returned (errors come back as RFC 9457 `application/problem+json`
   with `type`/`title`/`status`/`detail`/`errors`).
2. **List existing definitions** — `getApis`. Check whether the API already exists so
   you know to create vs. update.
3. **Create or update**:
   - New: `createApi` with the validated definition.
   - Existing: `updateApi` targeting the existing definition's identifier.
4. **Confirm** by re-running `getApis` and checking the returned definition.

## Rules

- Auth: Bearer token (see `authentication/readmeio-authentication.yml`). This route set
  is only available to projects using ReadMe Refactored.
- Errors: handle `application/problem+json` (see `errors/readmeio-problem-types.yml`);
  a 401 means a bad/missing key, a 400 means the definition failed validation.
- Prefer the `rdme openapi upload`/`validate` CLI (`cli/readmeio-cli.yml`) for CI.
