# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

**tax-prep** is a Claude Code skill that acts as a tax season co-pilot. It orchestrates preparing materials for a CPA or self-filing (TurboTax export): situation interview, account discovery, document collection/parsing, reconciliation, and package generation. Designed as an open-source MIT-licensed repo for Claude Code and Cowork.

## Architecture

### Pure Knowledge Skill (Zero Scripts)
This skill has no pre-built Python scripts. Claude's native tools handle all execution:
- PDF parsing → Read tool (vision/PDF support)
- CSV parsing → Read tool
- Web search → WebSearch tool (Claude Code only)
- Reconciliation → Claude reads JSON + CSV, applies thinking from SKILL.md
- TXF export → Write tool (text format)
- CPA package → Primary: single markdown document (`cpa-package.md`). Secondary: CSV files. Enhancement: xlsx via inline Python if openpyxl available

ALL intelligence lives in **SKILL.md** (workflow engine) + **references/** (knowledge base).

### Fluid Five-Phase Workflow
Phases are a logical framework, not a rigid sequence. Users move fluidly between them — uploading a document mid-interview, adding accounts during reconciliation, etc. State files are the source of truth.
1. **Situation Interview** — Conversational profiling. Reads `tax-data-sources.md` for baseline rates, WebSearch to verify in Code. Output: `profile.json`
2. **Account Discovery** — Maps accounts to expected tax documents using `document-matrix.md`. Accepts Monarch CSV, manual entry, or prior-year carryforward. Output: `accounts.json`
3. **Document Collection** — Ongoing. Reads PDFs (including multi-page CPA returns), extracts fields, presents to user for confirmation before saving. Property-type-aware rental prompts. Tracks estimated payments as first-class items. Updates `accounts.json`
4. **Reconciliation** — Completeness check, Monarch cross-reference, YoY comparison, gap detection per `common-gaps.md`. Output: `reconciliation.json`
5. **CPA Package / TurboTax Export** — Single markdown doc (primary), CSV files (secondary), xlsx (enhancement), .txf for TurboTax import. Includes CPA cover letter, rough tax estimate (with disclaimer), and session notes integration.

### Session Continuity
`session-notes.json` tracks corrections, clarifications, CPA notes, and decisions across sessions. Append-only. Read on resume to recall prior context.

### Key Directories
- `SKILL.md` — Core workflow engine (pure XML structure, ~220 lines)
- `references/` — On-demand knowledge base, loaded progressively by phase
- `references/state-guides/` — Per-state tax knowledge (NJ, NY, CA, CT)
- `evals/` — Synthetic test cases
- `state/` — **Gitignored.** Runtime state at `~/.tax-prep/{year}/`

### Environment Detection
- Bash available → Claude Code (full capabilities: WebSearch, inline Python for xlsx)
- Bash unavailable → Cowork (CSV/markdown output, reference-file rates only)

### Data Separation (Hard Rule)
- **Repo (public):** Generic references, synthetic test data only
- **Local only (gitignored):** All personal data in `~/.tax-prep/{year}/`
- Zero personal data in committed files

### Schema Versioning
All JSON state files include `"schema_version": "1.0"` for future migration compatibility.

### State Persistence
All workflow state lives in `~/.tax-prep/{year}/`. Prior year data enables YoY comparison and carryforward.

## Design Principles

- **Process, not tools** — each phase produces artifacts the next phase consumes
- **Completeness principle** — actively check for gaps rather than trusting the user's memory
- **One question at a time** — conversational, not form-dump
- **Confirm before saving** — always present extracted values to user before writing to state
- **Prior year awareness** — load last year as baseline, ask "what changed?"
- **Cowork-first** — primary output is a single markdown document; CSV and xlsx are secondary
- **Fluid phases** — phases guide suggestions, not gate actions; any action can happen at any time
