# 🌿 **FRACTAL SPEC v5**

*A compositional, recursive documentation model for humans and LLMs.*

---

# =========================================================

# 1. SUBJECTS & COMPONENTS — CORE MODEL

# =========================================================

### 1.1 Subject

Every folder in the structure represents a **subject**.
A subject is simply whatever that folder is about — a product, feature, deliverable, concept, project area, planning unit, or artefact.

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
last-updated: yyyy-mm-dd
used-by:
  - end-users: [...]
  - specs: [...]
```

Status of the subject is reflected here.
`used-by` distinguishes **vertical** (serving users) vs **horizontal** (shared resource) subjects.

---

### 3.2 Required Sections

```
# Requirements
# Design
# Change Log
```

These sections define ideal behaviour, current behaviour, and the evolution of the subject.

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

## 4.5 RULE 5 — One Active Plan

Each subject may have many plans in history, but only **one active plan** at a time.

All others must be:

* archived
* renamed
* or placed into a Done Appendix

This keeps execution unambiguous.

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

Exactly one active plan per subject.
Archived plans allowed.

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

**LLMs MUST follow these rules:**

1. Every folder is a subject.
2. Only split subjects when components would be **independently valuable**.
3. Never create child subjects for attributes — keep them inside the spec.
4. Leaf/atomic subjects must have a spec.
5. Only one active plan per subject.
6. Always reference parent specs for shared truths.
7. Use the spec lifecycle: Requirements → Research → Plan → Design → Implement → Promote.
8. Maintain folder purity: no extra folders except components.

---

# =========================================================

# 10. HUMAN README (DEEP EXPLANATIONS + EXAMPLES)

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

# =========================================================

# 11. DECISION TREE FOR SPLITTING (PLAINTEXT)

# =========================================================

```
START
 |
 |-- Does this subject feel larger, more complex, or overloaded compared to other specs?
 |         |
 |         |-- NO --> Keep as a single subject.
 |
 |-- YES
       |
       |-- Can it be split into 2+ parts that are independently valuable/useful on it's own (not rely on other components/doesn't need to be used in conjunction with other components to be used)?
       |         |
       |         |-- NO --> Do not split; treat differences as attributes.
       |
       |
       |-- Split into components.

```

---

