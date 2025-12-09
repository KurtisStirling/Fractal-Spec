# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Repository Overview

This is a **documentation-only repository** defining Fractal Spec — a compositional, recursive documentation model for humans and LLMs. There is no code to build, test, or run. The repository *is* the specification itself.

---

## Development Workflow

**No build/test pipeline exists.** Workflows are manual:
1. Edit Markdown files
2. Review diffs: `git diff`
3. Validate by reading rendered Markdown for structure and clarity
4. Commit with present-tense messages (e.g., "Add multi-level plan guidance")

---

## Required Reading Before Any Work

**CRITICAL**: Before doing any work in this repository, read these files in order:

1. **`fractal-spec/fractal-spec-guide.md`** — Complete specification (version recorded in frontmatter; sections 1-9 are LLM-focused, terse and token-optimized)
2. **`AGENTS.md`** — Repository-specific agent behavior guidelines

Do not skip this. The guide defines the entire fractal model you'll be working within.

---

## Repository Architecture

### High-Level Structure

```
fractal-spec/
  README.md
  fractal-spec-guide.md          # Core specification document (version in frontmatter)
  commands/                      # Reusable LLM commands
  spec-template.md               # Template for creating specs
```

### Fractal Spec Core Concept

**Every folder represents a thing.** Child folders are meaningful components of that thing. The structure repeats fractally at every level.

**Folder anatomy (repeating pattern):**
```
thing/
  thing.md        # Spec: Need + Design + Change Log
  *-plan.md       # Optional: one active plan
  research.md     # Optional: temporary research
  component/      # Component folders follow same anatomy
```

**Key distinctions:**
- **Spec** = permanent truth (Need + Design)
- **Plan** = temporary forward-looking work
- **Research** = temporary investigation

**When plans are needed:**
- High-level things: almost always (roadmap/backlog style)
- Low-level work: only if > 1 hour OR multiple files OR needs sequencing
- Simple tasks (bug fixes): just converse and execute

---

## Commands Available

The `fractal-spec/commands/` directory contains reusable LLM command specifications:

- **`verify-requirements.md`** — Structured interrogation to extract verified Need section
- **`verify-design.md`** — Structured interrogation to extract verified Design section
- **`analyse-structure.md`** — Analyze and optimize folder hierarchy
- **`create-plan.md`** — Create subject-level plans
- **`research-code.md`** — Document what exists using parallel sub-agents

When invoked, follow each command's workflow precisely. They define step-by-step protocols.

---

## Key Principles from AGENTS.md

**Working expectation:** Present options, pros/cons, tradeoffs, and a recommendation, then align before executing changes.

**Preserve existing edits:** Do not revert unrelated changes.

**Function over form:** Enforce purpose, not formatting.

**Markdown style:**
- Clear headings, short paragraphs
- ASCII by default
- Fenced code blocks for examples
- Inline code for file paths

**Commit guidelines:**
- Present tense, concise summaries
- Describe intent and scope
- Include relevant file paths touched

---

## Special Files to Maintain

**`fractal-spec-guide.md`** — Sections 1-9 are LLM-focused and must remain terse/token-optimized. Sections after "Do not read below this point" are human-focused and can be more verbose. Version lives in the frontmatter.

**`spec-template.md`** — Template with frontmatter for creating new specs. Keep consistent with guide.

**Change logs** — Keep maximum 5 most recent entries in specs. For older history, refer to git.

---

## Architecture Patterns

### Horizontal vs Vertical Components

Use `used-by` frontmatter to signal dependencies:
- **Vertical** = end-user features (e.g., checkout, user-profile)
- **Horizontal** = shared infrastructure consumed by multiple components (e.g., data-schema, auth)

### Splitting Rules

Split into components **only when independently valuable.**

**Do NOT split:**
- Attributes (color, size, status) — these stay in the spec
- Non-valuable fragments (< 1 hour of work)
- When uncertain — ask the user first (collaborative, not LLM decision)

### Upward Referencing

Always use explicit markdown links with anchors:
```markdown
See [styling rules](../components.md#styling) for shared guidelines.
```

Never use vague references like "See parent for styling rules."

---

## Working with Plans

**Multi-level pattern:**
- **High-level plans** (macro): scheduler-like, longer-lived, reference work areas
- **Low-level plans** (micro): task-list-like, shorter-lived, concrete deliverables

**Lifecycle:**
1. High-level plan has item: "implement feature-x"
2. Create `feature-x/` component with its own plan
3. Complete low-level tasks
4. Archive low-level plan
5. Check off high-level item

**Done = spec.Design matches production reality**

---

## What NOT to Create

Don't create separate specs for:
- Generated artifacts (API docs, build outputs)
- External dependencies (Postgres, Redis, AWS)

Instead, mention these in the parent thing's Design section as architectural choices.

---

## Navigation

For large structures (5+ top-level components), consider adding `index.md` at root with:
- Brief component descriptions
- Links to major specs
- Architectural context (vertical vs horizontal)

See `navigation-example.md` for reference.
