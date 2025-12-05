# Technical Documentation

**Read when:** Creating implementation docs or need guidance on patterns/ADRs/technical structure.

Implementation guidance: patterns, architecture, APIs, data models, standards, integrations.

## What Belongs Here

**Implementation patterns** - Reusable solutions to recurring technical problems
**Architecture decisions** - System design choices and rationale (ADRs)
**API specifications** - Endpoint definitions, contracts, schemas
**Data models** - Database schemas, entity relationships
**Technical standards** - Coding conventions, technology constraints
**Integration guides** - How to work with external systems

Anything that helps implement the specifications in `specs/`.

## When to Document

**Document when:** Repeat challenge (pattern), significant architecture choice, shared API, major alternative trade-off.

**Don't:** One-offs, standard framework patterns, trivial/obvious.

## How to Document

No prescribed format. Be consistent; reference specs (#ID); update when specs change.

**Common patterns for organization:**
```
technical/
  patterns/
    offline-sync.md
    auth-flow.md
  architecture/
    system-overview.md
    deployment.md
  adr/
    001-choice-of-database.md
    002-api-versioning-strategy.md
  api/
    rest-endpoints.md
    graphql-schema.md
```

## Common Formats

**Pattern:**
```markdown
# [Pattern Name]
Problem | Solution | When to Use | Implementation | Trade-offs | Related (#IDs)
```

**ADR (optional, for complex technical decisions):**
```markdown
# ADR-NNN: [Title]
Status | Date | Decision (see DECISIONS.md D#)
Context | Considered Options | Rationale | Consequences | References
```

**Decision workflow:** All significant decisions → DECISIONS.md. Complex technical → optional ADR with reference.

**Organization:**
```
technical/
  patterns/[name].md
  adr/NNN-[name].md
  api/[name].md
```

---

## For LLMs

Check existing docs; be consistent; link specs (#ID); explain why; use same format; create structure if missing.
