# FRACTAL SPEC v6

---

# =========================================================

# 1. SUBJECTS & COMPONENTS — CORE MODEL

# =========================================================

### 1.1 Subject

Every folder in the structure represents a **subject**.
A subject is whatever that folder is about — a product, feature, deliverable, concept, project area, planning unit, or artefact.

A subject owns:

* requirements
* design
* change log
* plans
* supporting files
* components (child subjects)

There is **no special name for the root**. It is simply the top-level subject.

---

### 1.2 Components

A folder may contain child folders.
Each child folder is a:

> **component of the parent subject**

This recursion continues indefinitely:
subject → components → sub-components → deeper components → …

---

### 1.3 Atomic Subject (Atomic Component)

A subject is **atomic** when:

* splitting it would produce items that are *not independently valuable*
* the subject is the smallest independently useful unit
* it has no sub-components
* it must have a specification file

This is the bottom-most level of decomposition.

---

# =========================================================

# 2. FOLDER STRUCTURE RULES

# =========================================================

A subject folder may contain:

* `subject-name.md` — **specification file**
  (mandatory unless this is a pure grouping subject)
* `*-plan.md` — **at most one active plan**, with optional archived plans
* `research.md` — optional, temporary
* Additional files directly related to this subject
* Child subject folders (components)

No other folder types are allowed.

---

# =========================================================

# 3. SPECIFICATION FILE

# =========================================================

Each spec file must include:

---

### 3.1 Front Matter

```
status: draft | approved | implemented
version: x.y
created: yyyy-mm-dd
last-updated: yyyy-mm-dd
used-by:
  - (end users "vertical" or specs "horizontal")
  - ...
```

Status of the subject is reflected here.
`used-by` distinguishes **vertical** (serving users) vs **horizontal** (shared resource) subjects.

---

### 3.2 Required Sections (function of each)

```
# Requirements   ← Demand: what must remain true now; reasons, rules, outcomes.
# Design         ← Supply: how the subject currently meets that demand; present-tense reality.
# Change Log     ← Trace of evolution; link approvals and promotions.
```

These sections define ideal behaviour, current behaviour, and the evolution of the subject. Keep function fixed; form is free.

### 3.5 Change Log format

Use dated entries that capture the change, rationale, and any notes/links for traceability.

```
v2 - 2025-06-15

Changes: Added "Remember me" checkbox requirement; Removed SMS verification (replaced with email-only)

Rationale: User feedback requested persistent sessions. SMS costs prohibitive for current user volume.

Notes: See DECISIONS.md D42 for authentication strategy decision. Updated test spec accordingly.
```

---

### 3.3 When Spec Files Are Mandatory

A spec **must** exist when:

* The subject is **atomic**
* The subject contains global requirements or design shared by its components
* The subject has distinct behaviour, constraints, or design meaningful to document

### 3.4 When Spec Files Are Optional

A spec may be omitted only when:

* The subject exists solely to group components
* The subject adds no global requirements or design
* All meaningful behaviour exists in its children

---

# =========================================================

# 4. SPLITTING & ATOMICITY

# =========================================================

This section defines *when to split a subject into components* and *when not to*.

This is one of the most important parts of the model.

---

## 4.1 RULE 1 — Independently-Valuable Rule

Split a subject into components **only if each resulting component is independently valuable**.

A component is independently valuable when:

* It produces a meaningful outcome
* It can be understood as a standalone offering
* It provides utility on its own
* It can be reasoned about, designed, and tested separately
* It is something you would name in a “menu” of capabilities

If the pieces are **not** independently valuable, they are attributes, not components.

---

## 4.2 RULE 2 — Do Not Split Into Attributes

Attributes belong **inside the subject’s spec**, not as components.

Attributes include:

* colour
* size
* typeface
* border radius
* behaviour details
* internal rules
* UX variations
* fields of a data model
* subproperties

Example: a `button` subject has attributes like colour, border, hover states — NOT child subjects.

---

## 4.3 RULE 3 — Proportionality Rule

Split a subject if:

* It is significantly larger or more complex than its sibling subjects
* You can separate it into 2+ smaller subjects *that are independently valuable*
* This improves clarity, maintainability, and reasoning

Do **not** split if:

* Splitting would only produce fragments that depend on each other to be useful
* The result is uneven, confusing, or forces unnatural boundaries

---

## 4.4 RULE 4 — Atomic Rule

Stop splitting when:

* Any further split produces units that are **not independently valuable**
* The subject is complete enough to be delivered or reasoned about
* All additional detail would express only attributes, not behaviour
* The subject is conceptually whole

Atomic subjects **must** have a spec file.

---

## 4.5 RULE 5 — One Active Plan (where work is done)

Each subject may have many plans in history, but only **one active plan** at a time. Planning is still **where the work is done** for that subject.

All other plans must be:

* archived
* renamed
* or placed into a Done Appendix

You may name the active plan for clarity (e.g., `2024-platform-plan.md`), but the hard rule remains: one live plan per subject.

---

## 4.6 RULE 6 — Upward Referencing

Child subjects must **not** duplicate global requirements or design.

They reference the parent:

```
See parent subject for shared data model and constraints.
```

---

# =========================================================

# 5. SPEC EVOLUTION LIFECYCLE

# =========================================================

Each subject follows the same lifecycle:

1. **Requirements (draft)**
2. **Optional research** → `research.md`
3. **Planning** → create `*-plan.md`
4. **Design finalisation**
5. **Approval**
6. **Implementation & testing**
7. **Promotion to implemented**

---

# =========================================================

# 6. PLAN FILES

# =========================================================

### 6.1 Naming

Must end in:

`-plan.md`

### 6.2 One Active Plan

Exactly one active plan per subject. Plans are where the work is done for that subject; everything forward-looking lives here.

### 6.3 Short-Lived Plans

Delete or archive after use.

### 6.4 Long-Lived Plans

Move completed items to a “Done Appendix”:

```
## Done Appendix
<!-- LLM: Do not read -->
```

---

# =========================================================

# 7. RESEARCH FILE

# =========================================================

* Optional
* Temporary
* Feeding into planning
* Must be deleted or archived once obsolete

---

# =========================================================

# 8. RECURSION & MICRO-COSMIC RULE

# =========================================================

Every subject is a microcosm of the entire model:

* recursive
* identical structure
* predictable
* scalable
* domain-independent

---

# =========================================================

# 9. LLM README (TERSE OPERATING MODE)

# =========================================================

### 9.1 Overview

* Compositional, recursive documentation skeleton. Every project produces output (code, docs, plans, systems); keep it inside the relevant subject.

### 9.2 Core principles (token-optimised)

* Token-optimised for LLMs — distil; avoid raw, verbose dumps.
* Self-guiding structure — predictable, consistent, right-time-right-place info.
* Traceability — maintain change/decision logs for evolution evidence.

### 9.3 Ways of working (LLM behaviour)

* Don't trust; verify with the user instead of assuming.
* Ask when requirements are unclear.
* Share options with pros/cons and a recommendation plus rationale.
* Challenge assumptions; user has strong PM/BA skills but is not a developer.
* Work methodically: propose → confirm → execute.

### 9.4 Operational rules

1. Every folder is a subject.
2. Only split subjects when components would be **independently valuable**.
3. Never create child subjects for attributes — keep them inside the spec.
4. Leaf/atomic subjects must have a spec.
5. Only one active plan per subject; plan is where work is done.
6. Always reference parent specs for shared truths.
7. Use the spec lifecycle: Requirements → Research → Plan → Design → Implement → Promote.
8. Maintain folder purity: no extra folders except components.

---

# =========================================================

# 10. HUMAN README (EXPLANATIONS + EXAMPLES)

# =========================================================

### 10.1 Overview

*A compositional, recursive documentation model for humans and LLMs.*

Fractal Specs is a lightweight skeleton: every subject owns demand (Requirements), supply (Design), and a single active plan where the work is done. Components mirror parents, giving predictable navigation without imposing semantics or heavy ceremony. Every project produces output (code, docs, plans, systems); keep it inside the relevant subject.

### 10.2 Core principles (expanded for humans)

* Token-optimised for LLMs — keep specs distilled and intentional; remove raw dumps.
* Self-guiding structure — predictable, consistent, discoverable; place info where it is needed at the right time.
* Traceability — use Change Logs and decision references to show why/when things changed.

### 10.3 Ways of working (LLM expectations)

* Don't trust; verify with the user instead of assuming.
* Ask when requirements are unclear.
* Share options with pros/cons and a recommendation with rationale.
* Challenge assumptions — assume the user is a strong PM/BA but not a developer.
* Work methodically: propose → confirm → execute.

## For Business & Leadership

* Requirements show enduring needs and reasons.
* Design shows how it works today.
* Plan shows what will happen next (one live plan per subject).

## For Product Managers

* Requirements = “what good looks like.”
* Design = current reality.
* Plan = roadmap → backlog → tasks in one place at the subject.

## For Developers & Engineers

* Requirements capture demand (behaviours, constraints, edge cases).
* Design captures supply (architecture, data, flows, decisions).
* Plan is the execution zone: implementation work, sequencing, and Done appendices for history.

---

# =========================================================

# 11. EXAMPLES (KEPT FROM V5)

# =========================================================

## Example A: **Button Component**

```
button/
  button.md
```

Attributes (inside spec):

* colour
* typeface
* border radius
* hover states
* variants (primary, danger, ghost)

These are *not* components because none are independently valuable.

Only if `button.md` becomes enormous AND there exist natural standalone offerings (e.g. `button-group`, `split-button`) would splitting make sense.

---

## Example B: **Holiday Planning**

```
holiday/
  flights/
  accommodation/
  car-hire/
  itinerary/
  budget/
```

Each is independently valuable:

* You can book flights without a car hire
* You can budget before itinerary
* Each can be delivered separately

---

## Example C: **Post Office Services**

```
post-office/
  postal-services/
  moneygram/
  cash-withdrawals/
  e-top-ups/
  car-tax/
  foreign-currency/
```

Each service is independently valuable → components.

---

## Example D: **Forest Ecosystem**

```
forest/
  trees/
  animals/
  soil/
  streams/
  air/
  seasonal-cycles/
```

Zoom in:

```
tree/
  roots/
  trunk/
  branches/
  leaves/
```

But:

* leaf colour
* leaf surface
* leaf veins
  are **attributes**, not child subjects.

---
