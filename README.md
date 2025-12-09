# Fractal Spec

Reference repo for the Fractal Spec v1 documentation set. It provides the guide, template, and LLM commands you can drop into any project to organize docs fractally (each folder is a "thing" with its own spec and optional plan/research).

## Quick start
- Read `fractal-spec/fractal-spec-guide.md` (Sections 1–4 at minimum).
- Copy `fractal-spec/` into your project: `cp -r fractal-spec/ /path/to/your-repo/`.
- Add the snippet from `fractal-spec/README.md` to your project's `CLAUDE.md` so LLMs follow the spec.
- Create your first spec from `fractal-spec/spec-template.md`, keeping one spec per folder.

## Repo layout
- `fractal-spec/` — Fractal Spec guide, template, and reusable commands.
- `future-enhancments/` — Notes for potential future additions.
- `CLAUDE.md` — Guidance for LLM collaborators working in this repo.
- `Plan.md.md` — Scratch planning notes.

## Updating this repo
- Keep changes to the spec isolated under `fractal-spec/`.
- Ignore local Obsidian state; `.obsidian/` is gitignored and should stay untracked.
