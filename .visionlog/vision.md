---
title: "foss-forge — Open-Source Standards for Agentic Software"
type: "vision"
date: "2026-03-22"
---

## North Star

foss-forge is the Eidos AGI standard for publishing great open-source **agentic software** — tools that AI agents use, not tools that humans use.

The agentic software ecosystem is young. Most open-source MCP servers, agent SDKs, and AI tool packages ship without the basics: no license, no changelog, no tests, no publish pipeline. The bar is low. We raise it.

## What Makes Agentic Software Different

Agentic software has a different consumer than traditional FOSS:

| Traditional FOSS | Agentic FOSS |
|-----------------|--------------|
| Humans read the README | Agents read tool descriptions and schemas |
| Humans browse docs | Agents parse structured metadata |
| Humans file issues | Agents hit error boundaries and need clear error messages |
| Humans install via CLI | Agents install via MCP config, pip, or registry |
| Humans configure via dotfiles | Agents configure via structured JSON/YAML |

This means our standards must cover both the human layer (contributors, maintainers) AND the agent layer (tool descriptions, schema quality, error surfaces).

## What foss-forge IS

- A set of **Claude Code skills** (`/foss-check`, `/foss-init`, `/foss-release`) that any Eidos AGI repo can use
- A set of **templates** for community health files, CI/CD workflows, and agentic metadata
- An **opinionated standard** for what "ready to ship" means for agentic open-source software
- Zero software to maintain — pure knowledge, templates, and skill prompts

## What foss-forge is NOT

- Not a Python package or CLI tool
- Not a linter or CI check (though it informs what CI should check)
- Not a general-purpose FOSS toolkit — it's specifically for agentic software published by Eidos AGI

## The Standard

A package is **foss-forge compliant** when it passes all checks:

### Human Layer (Community Health)
- LICENSE (MIT default)
- README.md with install, usage, and agent integration examples
- CHANGELOG.md (Keep a Changelog)
- CONTRIBUTING.md
- CODE_OF_CONDUCT.md

### Agent Layer (Agentic Quality)
- Tool descriptions are clear, unambiguous, and include usage examples
- Input/output schemas are fully typed with descriptions on every field
- Error messages are actionable (agents can't "see what went wrong" — errors must say what to do)
- MCP server metadata is complete (if applicable)
- Entry points are documented for both human and agent consumption

### Engineering Layer (Ship Quality)
- pyproject.toml with full metadata (hatchling build system)
- CI workflow (lint + test)
- Publish workflow (tag-triggered, trusted publisher, OIDC)
- Tests exist and cover the happy path at minimum
- .gitignore covers Python artifacts

## Success Metric

Every Eidos AGI package on PyPI passes `/foss-check` with an A grade. New packages start from `/foss-init` and never ship without the standard met.

