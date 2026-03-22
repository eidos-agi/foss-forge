---
id: '0004'
title: PEP 740 + Sigstore are the next layer — provenance on top of identity
status: open
evidence: HIGH
sources: 1
created: '2026-03-22'
---

## Claim

Trusted publishing, PEP 740, and Sigstore are complementary layers: Trusted Publishing answers "did this upload come from the expected repo/workflow?" (identity). Sigstore answers "can we produce a verifiable signature tied to that identity without long-lived signing keys?" (provenance). PEP 740 answers "can PyPI store and serve those attestations so consumers can verify?" (distribution). The full stack: build → Sigstore attestation → upload via OIDC → attestation stored on PyPI (PEP 740) → consumers verify artifact hash + attestation + identity constraints.

## Supporting Evidence

> **Evidence: [HIGH]** — GPT-5.2 analysis of PEP 740 + Sigstore relationship (content_hash:d4e2f663), retrieved 2026-03-22

## Caveats

None identified yet.
