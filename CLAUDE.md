# CLAUDE.md — foss-forge

> Open-source standards toolkit for agentic software. Skills and templates, not software.

## What This Is

foss-forge is a set of Claude Code skills and file templates that enforce a standard for publishing great FOSS — specifically **agentic software** (MCP servers, agent SDKs, AI tools). Software that agents use, not software that humans use.

There is no code here. No CLI. No package. Just knowledge.

## Skills

| Skill | What It Does |
|-------|-------------|
| `/foss-check` | Audit a repo against FOSS standards — community health, agentic quality, engineering, deps, security |
| `/foss-init` | Scaffold missing community health files from templates — LICENSE, CHANGELOG, CONTRIBUTING, etc. |
| `/foss-release` | Guided release: version bump, changelog, tag, push, PyPI publish |
| `/foss-launch` | Marketing playbook: README optimization, badges, star history, launch channels, phased timeline |
| `/foss-demo` | Assess demo needs, generate simple demos or delegate to demo-forge |

## Templates

All templates live in `templates/` with `{{VARIABLE}}` substitution:

| Template | Generates |
|----------|-----------|
| `LICENSE.tmpl` | MIT license |
| `CHANGELOG.md.tmpl` | Keep a Changelog format |
| `CONTRIBUTING.md.tmpl` | Contributor guide with agentic software guidance |
| `CODE_OF_CONDUCT.md.tmpl` | Contributor Covenant v2.0 |
| `SECURITY.md.tmpl` | Vulnerability reporting policy |
| `gitignore.tmpl` | Python + IDE + OS ignores |
| `ci.yml.tmpl` | GitHub Actions CI (lint + test, Python matrix) |
| `publish.yml.tmpl` | GitHub Actions PyPI publish (trusted publisher, OIDC) |

## Using These Skills in Other Repos

To use foss-forge skills in any Eidos AGI project, the skills reference templates at `~/repos-eidos-agi/foss-forge/templates/`. The skills themselves can be copied or symlinked into any project's `.claude/skills/` directory.

## Guardrails

1. **No software.** This repo must never become a Python package or installable tool.
2. **Agent-first standards.** Every check must address the agent consumer, not just human contributors.
3. **Never overwrite.** `/foss-init` only creates missing files, never replaces existing ones.

## Related Forges

- **forge-forge** — meta-forge for creating and managing forges (`/forge-init`, `/forge-audit`, `/forge-catalog`)
- **demo-forge** — AI-generated demos (GIFs, SVGs, screenshots, diagrams, social cards)
- **test-forge** — testing standards and test generation
