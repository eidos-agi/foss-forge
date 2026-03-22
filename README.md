# foss-forge

Open-source standards for agentic software. Built for AI tools that AI agents use.

## What is this?

A set of [Claude Code](https://claude.ai/claude-code) skills and templates that enforce a quality standard for publishing open-source agentic software — MCP servers, agent SDKs, and AI tools.

No code. No CLI. No package to install. Just knowledge that agents use to ship better software.

## Why?

The agentic software ecosystem is young. Most open-source MCP servers and AI tools ship without the basics: no license, no changelog, no tests, no publish pipeline. Tool descriptions are vague. Schemas are untyped. Error messages say "failed" instead of what to do next.

Agents are the primary consumers of agentic software. They deserve the same quality standards that human-facing software gets — plus standards specific to how agents discover, understand, and use tools.

## Skills

| Skill | What |
|-------|------|
| `/foss-check` | Audit a repo: community health, agentic quality, package metadata, deps, CI/CD, security |
| `/foss-init` | Scaffold missing files from templates (LICENSE, CHANGELOG, CONTRIBUTING, CI workflows, etc.) |
| `/foss-release` | Guided release: bump version, update changelog, tag, push, verify PyPI publish |
| `/foss-launch` | Marketing playbook: README optimization, badges, star history, launch channels, timeline |
| `/foss-demo` | Demo assessment and generation — delegates to demo-forge for production content |

## The Standard

A package is **foss-forge compliant** when it passes `/foss-check` with an A grade across three layers:

### Human Layer (contributors)
LICENSE, README, CHANGELOG, CONTRIBUTING, CODE_OF_CONDUCT, SECURITY

### Agent Layer (consumers)
- Tool descriptions explain *when* to use each tool, not just *what* it does
- Every parameter has a type and description
- Error messages are actionable — agents can't "see what went wrong"
- MCP config examples in README

### Engineering Layer (shipping)
- Full `pyproject.toml` metadata (hatchling, classifiers, keywords, URLs)
- CI workflow (lint + test matrix)
- Publish workflow (tag-triggered, trusted publisher)
- ≤5 direct dependencies

## Usage

Clone this repo alongside your projects:

```bash
git clone https://github.com/eidos-agi/foss-forge.git ~/repos-eidos-agi/foss-forge
```

Then in any project, copy or symlink the skills you need:

```bash
cp ~/repos-eidos-agi/foss-forge/.claude/skills/foss-*.md .claude/skills/
```

Now `/foss-check`, `/foss-init`, `/foss-release`, `/foss-launch`, and `/foss-demo` are available in that project.

## Part of the Forge Ecosystem

- [forge-forge](https://github.com/eidos-agi/forge-forge) — the meta-forge (create and manage forges)
- [foss-forge](https://github.com/eidos-agi/foss-forge) — this repo
- [demo-forge](https://github.com/eidos-agi/demo-forge) — AI-generated demo content
- [security-forge](https://github.com/eidos-agi/security-forge) — security auditing and agentic threat modeling
- [test-forge](https://github.com/eidos-agi/test-forge) — testing standards

## License

MIT — [Eidos AGI](https://github.com/eidos-agi)
