---
id: "GUARD-001"
type: "guardrail"
title: "No software — skills and templates only"
status: "active"
date: "2026-03-22"
---

## Rule
foss-forge must never become a Python package, CLI tool, or any installable software. It is a collection of Claude Code skills and file templates. Nothing more.

## Why
Software requires maintenance. Skills are just knowledge — they evolve with the agent and never break. The moment foss-forge becomes a package, it becomes another thing that needs to pass its own standards, creates circular dependencies, and adds maintenance burden.

## Violation Examples
- Adding a `pyproject.toml` with a build system
- Creating a `setup.py` or `setup.cfg`
- Writing Python scripts that need to be installed or executed
- Publishing foss-forge to PyPI
