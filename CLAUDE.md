# CLAUDE.md

## HALSER Documentation

This repository contains the user-facing documentation for HALSER, published at https://docs.hatlabs.fi/halser.

## Build Commands

```bash
uv sync                          # Install dependencies
uv run mkdocs serve              # Local dev server at http://127.0.0.1:8000
uv run mkdocs build --strict     # Production build (fails on warnings)
```

## Content Guidelines

- HALSER is a development board — documentation should reflect that custom firmware is the expected path
- The default firmware is a convenience for quick evaluation, not the primary feature
- Use MkDocs Material admonitions (`!!! tip`, `!!! warning`, `!!! note`) for callouts
- Mark missing content with HTML comments: `<!-- TODO: description -->`
- Images go in the same directory as the markdown file that references them
- Use relative paths for cross-references between pages

## Structure

- `getting-started/` — Hardware setup (power, enclosures)
- `usage/` — Serial interface wiring and device connection
- `hardware/` — Technical reference (connectors, GPIO, specs)
- `software/` — Firmware development (custom and default)
- `appendices/` — Design files, revisions, errata, resources
