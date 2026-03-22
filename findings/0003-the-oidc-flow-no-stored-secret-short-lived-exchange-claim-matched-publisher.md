---
id: '0003'
title: 'The OIDC flow: no stored secret, short-lived exchange, claim-matched publisher'
status: open
evidence: HIGH
sources: 1
created: '2026-03-22'
---

## Claim

The flow: (1) CI job requests OIDC ID token from GitHub (requires permissions: id-token: write), (2) GitHub issues signed JWT with claims including repo, workflow, ref, environment, (3) workflow sends JWT to PyPI's exchange endpoint, (4) PyPI validates signature via JWKS, checks claims match the registered publisher config (org, repo, workflow, environment), (5) PyPI issues short-lived upload credential scoped to that project, (6) workflow uploads with ephemeral credential. The key insight: the only "secret" is a just-in-time JWT minted by the CI provider. Nothing is stored in repo settings.

## Supporting Evidence

> **Evidence: [HIGH]** — GPT-5.2 technical breakdown + PyPI trusted publisher docs (content_hash:c9d1e552), retrieved 2026-03-22

## Caveats

None identified yet.
