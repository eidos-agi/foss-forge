---
id: "GUARD-002"
type: "guardrail"
title: "Agent-first standards"
status: "active"
date: "2026-03-22"
---

## Rule
Every standard in foss-forge must address the agent consumer, not just the human contributor. If a check only matters to humans and has no agentic dimension, it doesn't belong here — use a generic FOSS checklist instead.

## Why
The world has plenty of FOSS checklists for human-facing software. foss-forge exists specifically because agentic software has different quality requirements: tool descriptions matter more than CLI help text, schemas matter more than man pages, error messages must be machine-actionable not human-readable.

## Violation Examples
- Adding checks for documentation website quality
- Requiring human-facing CLI help text standards
- Checking for human UX patterns (color output, progress bars, etc.)
- Ignoring tool description quality while checking README quality
