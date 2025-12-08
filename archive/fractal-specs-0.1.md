# Microcosm Fractal Specification Model (Draft)

## Summary of Breakthroughs

You developed a recursive, minimal, and truth-aligned documentation + execution framework derived from the RPI (Research → Plan → Implement) workflow used for complex brownfield development. The key breakthroughs are:

1. **RPI Generalisation** – You realised RPI isn't just a coding workflow but a universal system-engineering cycle.  
2. **Dual-Truth Architecture** – Requirements represent *future truth*; Design represents *current truth*.  
3. **Fractal Structure** – Every level of a system, from product to component, uses the same structure.  
4. **Permanent vs Temporary Truth** – Requirements and Design are permanent; Research and Plan are temporary.  
5. **Draft → Promote Workflow** – Work is complete only when code *and* Design.md are updated to reflect reality.  
6. **Minimal Semantics** – No epics, stories, tickets, modules—just recursive subjects with the same simple anatomy.  
7. **LLM-Friendly** – The structure is predictable, local, and truth-based, enabling safe, reliable AI collaboration.

---

## Core Structure

Each subject (folder) contains:

```
Subject/
  Requirements.md   ← permanent future truth
  Design.md         ← permanent current truth (specification)
  design-assets/    ← permanent diagrams, models, structural artefacts referenced by Design.md
  work/
    Research.md     ← compressed learning informing planning
    Plan.md         ← temporary sequencing and draft designs
  ComponentA/
  ComponentB/
```

---

## Requirements.md

Distilled desired outcomes including:

- problems → desired outcomes  
- use cases  
- jobs to be done  
- constraints  
- personas  
- non-functional requirements  
- business needs  

Each requirement has:

- **What** (desired outcome)  
- **Why** (value/rationale)  
- **Status** (Met/Unmet)  
- **Priority** (optional)

Requirements are *the only permanent future intent*.

Include a compact changelog at the bottom, wrapped in HTML to signal LLMs to skip unless asked:

```html
<details>
  <summary>Changelog (expand if needed)</summary>
  <ul>
    <li>2025-02-01: Added X, removed Y</li>
  </ul>
</details>
```
Keep entries terse (token-efficient) and use it for removals/deferrals instead of statuses.

---

## Design.md

The authoritative **system specification** including:

- system behaviour  
- architecture  
- flows  
- APIs  
- data models  
- UI structure  
- design decisions and rationale (large design decisions must be captured)  
- references to collateral  

Includes minimal frontmatter:

```yaml
---
created: 2025-01-01
last-updated: 2025-02-01
version: 1.0
used-by:
  - Mobile-App
  - Reports-Service
---
```

Design.md is always updated during **promotion**.

Append a compact changelog, also HTML-wrapped for opt-in reading by LLMs (same pattern as Requirements.md).

---

## design-assets/

Permanent design-linked artefacts referenced from Design.md, such as:

- architecture diagrams  
- ERDs  
- sequence diagrams  
- UI mockups  
- schemas  

Rules:

- Must be referenced from Design.md (otherwise delete or move to work/).
- Not for drafts; only truth-bearing, up-to-date artefacts that explain or visualise the current design.
- Requirements.md should stay distilled—no attachments or papertrails there.

---

## work/

A temporary workspace for executing change.

You may include any structure you find useful.

Two artefacts are formally defined:

### **Research.md**
Compressed learning in four quadrants:

1. Internal technology knowledge  
2. Internal domain knowledge  
3. External technology research  
4. External domain research  

### **Plan.md**
Contains:

- draft design ideas  
- sequencing  
- implementation steps  
- decisions to make  

### Work Completion Rule

**Work is considered complete only when:**

- the implementation is done  
- the permanent Design.md reflects the true as-built system  
- Requirements.md statuses are updated  

Plans themselves are “complete” when written—  
**work** is complete only when *truth is updated*.

---

## Naming Considerations

Keywords your naming should evoke:

- **Microcosm**  
- **Fractal**  
- **Recursive**  
- **Research → Plan → Implement (RPI)**  
- **Requirements & Design**  
- **Truth-based documentation**  

Suggested name family:  
**Microcosm Fractal Specification Model (MFSM)**  
**Fractal RPI Framework**  
**Recursive Specification Model**

---

## Summary

This model unifies:

- requirements capture  
- design specification  
- planning and research  
- implementation workflow  
- brownfield comprehension  
- LLM collaboration  
- documentation architecture  

…into a *single recursive structure* that scales from entire products to individual components.

It creates a predictable environment for humans and AI to reason reliably, promotes truth alignment, avoids semantic bloat, and ensures implementation never drifts from design.
