---
name: Publish a changelog entry to a ReadMe project
description: Create and manage dated changelog entries in a ReadMe developer hub via the API.
api: ReadMe API (v2) — https://api.readme.com/v2
operations: [getChangelogs, createChangelog, updateChangelog, getChangelog]
generated: '2026-07-20'
method: generated
source: https://docs.readme.com/main/reference/readme-api
---

# Publish a changelog entry to a ReadMe project

Automate release notes by writing dated changelog entries into your ReadMe hub. All
calls go to `https://api.readme.com/v2` with `Authorization: Bearer <README_API_KEY>`.

## Steps

1. **List recent entries** — `getChangelogs` (paginated with `page`/`per_page`, up to
   100; see `conventions/readmeio-conventions.yml`) to avoid duplicates.
2. **Create the entry** — `createChangelog` with the title, body (Markdown), and type
   (e.g. added/fixed/improved).
3. **Update if needed** — `updateChangelog` to revise an existing entry.
4. **Verify** — `getChangelog` for the entry you just wrote.

## Rules

- Auth: Bearer token (see `authentication/readmeio-authentication.yml`).
- Pagination: response carries a `paging` envelope (`next`/`previous`/`first`/`last`)
  plus `total`/`page`/`per_page`.
- Errors: RFC 9457 `application/problem+json` (see `errors/readmeio-problem-types.yml`).
- No idempotency-key is documented — guard against duplicate creates by listing first.
