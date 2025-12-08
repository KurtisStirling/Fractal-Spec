# Repository Guidelines

## Project Structure & Module Organization
- Root contains versioned specs: `fractal-specs-0.1.md`, `fractal-specs-0.2.md`, `fractal-specs-0.3.md`.
- Supporting RPI agent notes live under `stolen-commands-RPI/` (e.g., `research_codebase.md`).
- No build artifacts or generated outputs; this repo is documentation-only.

## Build, Test, and Development Commands
- No build or test pipeline is defined. Workflows are manual: edit Markdown, then review diffs (`git diff`) and render in a Markdown viewer if desired.
- Keep changes minimal and reversible; avoid introducing tooling or lockfiles without discussion.

## Coding Style & Naming Conventions
- Markdown-first; prefer clear headings and short paragraphs.
- ASCII characters by default; only introduce non-ASCII when essential.
- Use fenced code blocks for examples. Inline code for file paths (e.g., `fractal-specs-0.3.md`).
- Keep section titles descriptive and concise; avoid decorative phrasing.

## Testing Guidelines
- No automated tests. Validate by reading the rendered Markdown for structure, broken lists, and clarity.
- When adding examples (paths, commands), ensure they are runnable or clearly illustrative.

## Commit & Pull Request Guidelines
- Commit messages: use present tense and concise summaries (e.g., “Add agentic overlay section”).
- PRs should:
  - Describe the intent and scope of the doc change.
  - Note any deviations from established patterns (e.g., new folder names).
  - Include relevant file paths touched.

## Agent-Specific Instructions
- Preserve existing user edits; do not revert unrelated changes.
- Avoid adding prescription-heavy templates unless clearly marked as optional defaults.
- Respect sandbox constraints; avoid destructive commands.
- When editing specs, keep “function over form” philosophy: enforce purpose, not formatting.
- Working expectation: do not run ahead on decisions—present options, pros/cons, tradeoffs, and a recommendation, then align before executing changes.
