---
framework: Lightspec
version: 1
created: 2025-12-04
last_updated: 2025-12-04
author: Kurtis Papple
---
<!-- [IMMUTABLE] DO NOT EDIT -->

Lightspec is a light-weight framework for spec-driven development with Claude Code. Purposely terse for max context using min tokens. 

This constitution defines how we spec, test, execute, and document. 

---

## All Projects Produce Output

Every project produces output (code, docs, plans, systems). Define it in GOALS.md before starting.

Start with a domain spec; add more (tests, technical docs) as complexity grows. Framework scales personal → enterprise.

---

## Core Principles

1. **Token-optimized for LLMs** - Minimal token usage while maintaining clarity
2. **Self-guiding structure** - Discoverable, just-in-time information, relying on recognition over recall
3. **Everything documented** - All material decisions and context written down
4. **Traceability** - Every requirement has an origin, every change has a reason

## Framework Characteristics

**Universal**: Works from personal to enterprise without modification
**Scalable**: Start simple, scale when pain appears
**Comprehensive**: No obvious gaps, no over-engineering
**Immutable**: Base framework never changes; projects extend only
**Game-framed**: GOALS.md & RULES.md answer "what is the game are we playing?"
**Requirements-handling**: Global must-have requirements → RULES.md. Feature requirements → specs/ (with priorities and AC). These are the source of truth.

---

## LLM Expectations

When working with this framework:

- Verify before assuming
- Ask when requirements unclear
- Share options with rationale
- Challenge assumptions
- Work methodically: propose → confirm → execute

---

## File Structure and Descriptions

```
/
  .claude/
    CLAUDE.md  # LLM bootloader

  constitution/
    CONSTITUTION.md   # (this doc) - Framework structure, principles, workflow
    GOALS.md  # Mission + current objective (living doc)
    RULES.md  # Global Rules of the "game" (living doc)
    DECISIONS.md  # Decision log: why this path? (living doc)

  specs/  # WHAT the product features should be and WHY
    README.md  # explains specs and template use
    SPEC-TEMPLATE.md
    {topic}/                  # Optional
    {descriptive-name}.md  # spec instance, uses template (living docs)

  tests/  # HOW to verify: scenarios, coverage
    README.md # explains tests and template use
    TEST-TEMPLATE.md
    {descriptive-name}.md # tests instance, uses template (living docs)

  technical/  # HOW to implement e.g. patterns, architecture, APIs
    README.md # explains technical and example usage
    # Organize as needed

  roadmap/
    ROADMAP.md  # Now/Next/Later backlog (living doc)
    inbox/  # raw input material for processing
    plans/  # Optional detailed plans to keep backlog lean
    done/
      done.md  # completed ROADMAP items moved here for archival
      [completed plans]

  src/
  tests/
```


---

## Daily LLM Usage

Each session: read .claude/, GOALS, RULES, scan DECISIONS; then read relevant spec/test/technical/roadmap files.

Recognition over recall: structure guides you to information when needed.

---

## Naming Conventions

- **Files**: `descriptive-kebab-case.md` (e.g., `user-authentication.md`)
- **Directories**: `lowercase-kebab-case/` (e.g., `specs/`)
- **IDs**: Simple numeric in frontmatter (e.g., `id: 42`)
- **Rule references**: `R1`, `R2`, etc.

---
## Non-editable markings

  <!-- [IMMUTABLE] DO NOT EDIT -->
  [content stays immutable until...]

  <!-- [EDITABLE] CUSTOMIZE BELOW -->
  [content stays editable until...]

  <!-- [IMMUTABLE] -->
  [content stays immutable for rest of file]

  Only opening tags - they mark transitions, not closures. 

---

## Scaling Guidance

Start minimum; scale when pain appears:

- **Tiny**: One spec + AC
- **Small**: Few specs + basic roadmap
- **Medium**: Specs + tests + patterns
- **Large**: Many artifacts, organized folders

Framework doesn't change - just usage depth.

