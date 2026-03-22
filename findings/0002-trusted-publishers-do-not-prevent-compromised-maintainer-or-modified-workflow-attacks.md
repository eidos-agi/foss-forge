---
id: '0002'
title: >-
  Trusted publishers do NOT prevent compromised maintainer or modified workflow
  attacks
status: open
evidence: HIGH
sources: 1
created: '2026-03-22'
---

## Claim

Trusted publishing proves WHICH workflow/repo published, not that the code is benign. If an attacker can modify the release workflow on the default branch (via compromised maintainer account or merged malicious PR), they can cause a "legitimate" OIDC identity to publish malicious artifacts. It also doesn't protect against compromised CI runners that alter build outputs before upload. Trusted publishing is credential-theft resistance, not complete supply-chain integrity.

## Supporting Evidence

> **Evidence: [HIGH]** — GPT-5.2 security analysis (content_hash:b7e2d441), retrieved 2026-03-22

## Caveats

None identified yet.
