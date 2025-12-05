# Lightspec

Lightweight spec-driven development for LLM-powered teams.

## What’s in this repo
- `lightspec/` — the product you copy into projects (constitution, templates, roadmap, technical/tests/specs, .claude).
- `Lightspec-development/` — meta context and decisions for building the framework (not needed by consumers).

## Quick start
1) Copy `lightspec/` into your project root (or download the release asset).
2) Read `lightspec/constitution/CONSTITUTION.md`.
3) Set your mission/objective in `lightspec/constitution/GOALS.md`.
4) Add project rules starting at R4 in `lightspec/constitution/RULES.md`.
5) Create your first spec from `lightspec/specs/SPEC-TEMPLATE.md`, then its test spec from `lightspec/tests/TEST-TEMPLATE.md`.

## Releases
- Public version is recorded in `lightspec/constitution/CONSTITUTION.md` frontmatter.
- GitHub releases include a ZIP of the `lightspec/` folder for easy download.

## Structure (product)
- `constitution/` — CONSTITUTION.md, GOALS.md, RULES.md, DECISIONS.md
- `specs/` — SPEC-TEMPLATE.md + README
- `tests/` — TEST-TEMPLATE.md + README
- `technical/` — README
- `roadmap/` — ROADMAP.md
- `.claude/` — LLM bootloader

## Notes
- The framework is immutable; projects extend via context rules (R4+) and their own specs/tests.
- Use the templates as-is; guidance lives in the READMEs for token efficiency.
