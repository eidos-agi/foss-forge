---
id: '0001'
title: >-
  Trusted publishers eliminate the highest-risk attack vector: long-lived CI
  secrets
status: open
evidence: HIGH
sources: 1
created: '2026-03-22'
---

## Claim

API tokens stored in GitHub Actions secrets are long-lived bearer tokens. If leaked (compromised repo admin, malicious PR, accidental logging, exfiltrating third-party action, compromised runner), the attacker can publish arbitrary versions of the package until the token is manually revoked. Trusted publishers replace this with short-lived OIDC tokens minted just-in-time by the CI provider — there is no static PyPI credential to steal. The token is audience-restricted, identity-bound, and expires in minutes. This closes the entire class of "steal the CI secret and replay it later" attacks.

## Supporting Evidence

> **Evidence: [HIGH]** — GPT-5.2 analysis of OIDC flow + PyPI documentation (content_hash:a8f3c210), retrieved 2026-03-22

## Caveats

None identified yet.
