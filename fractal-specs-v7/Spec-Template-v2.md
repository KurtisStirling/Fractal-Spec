---
status: draft | approved | implemented
version: 0.1
created: yyyy-mm-dd
last-updated: yyyy-mm-dd
used-by:
  - "[end users] | [other specs]"
---
# [Thing Name]

> One clear sentence: what this thing is (or will be).

---

## Need
<!-- Why this thing should exist or continue to exist. What problem it solves. -->

**Purpose**  
- The core reason this thing exists or is being created.  
- What it makes possible or easier.

**Scope**  
- What this thing includes.  
- What it deliberately does *not* include (avoid feature bloat).

**Requirements / Rules**  
- Important expectations, constraints, or behaviours that must be true.  
- Keep concise—only what actually matters.

**Success Notes (optional)**  
- How you’ll know this thing “works” (informal OK).

---

## Design
<!-- How this thing works or is intended to work. Present or future tense allowed. -->

**Responsibilities**  
- What this thing is responsible for.  
- Clear boundaries: what belongs elsewhere.

**Interfaces**  
- How you (or other components) interact with it.  
- Endpoints, inputs/outputs, major functions, UI elements, contracts.

**Behaviour**  
- Main flows or how this thing responds to inputs.  
- Key edge cases (just the important ones).  
- Use plain English — this is for coordination with an LLM and your future self.

**Data / State (only if relevant)**  
- What data this thing owns or uses.  
- Any important persistence or caching notes.

**Dependencies**  
- Things this relies on (APIs, libraries, other components).  
- Things relying on this (optional).

**Key Decisions**  
- D1 — Summary (what + why)  
- D2 — …

(Keep decisions lightweight; 1–2 bullet points each.)

---

## Change Log
<!--
Brief notes capturing meaningful Need or Design changes. Include rationale if needed.
Keep maximum 5 most recent entries. For older history: "See git history for full change log"
-->

### v0.1.0 — YYYY-MM-DD
- Created initial spec.
