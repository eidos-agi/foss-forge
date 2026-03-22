---
id: '0005'
title: >-
  The friction is intentional — per-package publisher registration is a security
  feature
status: open
evidence: MODERATE
sources: 1
created: '2026-03-22'
---

## Claim

The manual registration step (going to PyPI, filling in org/repo/workflow/environment) is deliberately per-package because it creates an explicit binding between a PyPI project and a specific GitHub identity. A shared API token grants access to ALL packages in scope — if compromised, all packages are exposed. A trusted publisher configuration grants access to ONE package from ONE repo's ONE workflow — the blast radius of any single compromise is contained to that package. The "friction" is the security property.

## Supporting Evidence

> **Evidence: [MODERATE]** — Inference from OIDC claim-matching design + comparison with token scoping (content_hash:e5f3a774), retrieved 2026-03-22

## Caveats

None identified yet.
