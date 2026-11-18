# Hardening a multi-tenant SaaS

**Role:** fixed findings from audits and code review across APIs, database access, outbound requests and billing
**Stack:** Next.js route guards, PostgreSQL row-level security, Redis, JWT, Vitest

## The problem

The product holds many companies' messages, integrations and credits in one system. Features were shipping fast, and audits found the usual gaps of a fast-moving codebase: routes that could act across tenants, outbound requests that could be steered at internal addresses, and weak spots in token handling.

This page describes the classes of fixes, not specific weaknesses.

## Tenant isolation

- Authentication and workspace-membership checks on every affected route, and per-account sharing rules on shared mailboxes.
- Row-level security added to core tables, and anonymous database access revoked where it wasn't needed.
- Where a privileged database client was genuinely required, an explicit workspace filter on every statement, since that client bypasses row-level security.
- Webhooks that fail closed on missing or invalid signatures.
- Rate limits moved from per-process memory to Redis, so they hold across instances.

I grouped findings by class (missing auth, missing sharing check, leaked error details, unsafe outbound fetch) so each became a reusable guard with a test, not a one-off patch.

## Outbound request safety (SSRF)

Several features fetch URLs a user supplies: workflow test runs, API calls, connector setup and attachments. I built one shared fetch helper:

- It resolves the address and pins the connection to it, so a DNS change between check and use can't redirect the request.
- It re-validates every redirect hop.
- It strips sensitive headers on cross-origin redirects.

A first version passed review, but follow-up findings showed redirects could still slip through. Moving every caller onto one helper meant no caller could get it wrong on its own.

## Tokens and credentials

- Secret resolution was centralised, a hard-coded fallback secret removed, and issuer and audience claims added to tokens.
- Short-lived auth codes moved from process memory to Redis with atomic single-use redemption, bound to their redirect, and failing closed if Redis is unavailable.

## Making tests mean something

A database test suite protecting billing had been passing for months while running no assertions at all, because of a setup issue that silently skipped them. I rebuilt the harness so the tests actually execute. I also added a live integration suite of 26 tests for billing idempotency, credit grants and refunds. My rule since: check that a test can fail before trusting that it passes.
