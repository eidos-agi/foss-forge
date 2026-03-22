---
id: "GUARD-003"
type: "guardrail"
title: "Never overwrite existing files"
status: "active"
date: "2026-03-22"
---

## Rule
The `/foss-init` skill must never overwrite a file that already exists. It scaffolds what's missing and skips what's present.

## Why
Existing files represent decisions the maintainer already made. Overwriting them destroys context and customization. The right approach is to audit (via `/foss-check`) and let the maintainer decide what to update.

## Violation Examples
- Replacing an existing CONTRIBUTING.md with the template version
- Overwriting a custom .gitignore
- Replacing a project's existing CI workflow
