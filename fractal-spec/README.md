# Fractal Spec

Compositional, recursive documentation model for humans and LLMs.

## Setup

**1. Copy this folder to your repo**
```bash
cp -r fractal-spec/ /path/to/your-repo/
```

**2. Add to your CLAUDE.md**

Add this to your project's `CLAUDE.md` file to make Claude Code aware of Fractal Spec:

```markdown
## Fractal Spec

This repo uses Fractal Spec for documentation.

**Before any work:** Read `fractal-spec/fractal-spec-guide.md` (Sections 1-4 minimum).

**Key principles:**
- Every folder = a thing
- Child folders = meaningful components of that thing
- Each thing has: `thing.md` (spec), optional `*-plan.md`, optional `research.md`
```

**3. Start documenting**

Create your first spec using `spec-template.md` as a starting point.

---

## What's in this folder

- **fractal-spec-guide.md** — Complete specification and LLM guide
- **spec-template.md** — Template for creating new specs
- **commands/** — Reusable LLM commands for requirements verification, design verification, structure analysis, and planning

---

For full documentation, see `fractal-spec-guide.md`.
