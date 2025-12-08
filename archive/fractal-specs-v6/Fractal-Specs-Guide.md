LLM opening instructions live in `README.md` (LLM section).  
Read that first for startup protocol.

---

# 1. THINGS & COMPONENTS — CORE MODEL

**Every folder represents a real “thing.”  
The specification in that folder describes the need for this thing to exist, and its design.**

Child folders represent **meaningful components of the thing**.  
This pattern repeats recursively:  
a thing may contain components, which are themselves things with their own components.

The smallest independently valuable parts of the structure are **atomic components**, and they **must have their own specification**.

---

### 1.1 Thing

Every folder represents a **thing**: a product, feature, deliverable, concept, area of responsibility, physical artefact, planning unit, or anything else.

A thing owns:

- its Need (demand)
- its Design (current supply)
- its Change Log (its evolution)
- its Plan (how it will evolve next)
- any supporting files that describe it
- any meaningful components (child folders)

There is **no special name for the root**. It is simply the top-level thing.

---

### 1.2 Components

A folder may contain child folders.  
Each child folder is:

> **a meaningful component of the larger thing.**

This compositional recursion repeats indefinitely:

**thing → components → deeper components → atomic components**

---

### 1.3 Atomic Components

A component is **atomic** when:

- splitting it produces items that are _not independently valuable_
    
- it is the smallest independently useful part of the thing
    
- it contains no components
    
- it **must have its own specification file**
    

This is the bottom-most level of decomposition.

---

# 2. FOLDER STRUCTURE RULES

The documentation structure should **mirror the real-world compositional structure** of whatever is being documented.

A folder representing a thing may contain:

- `[thing-name].md` — **specification file**  
    (mandatory unless this is a pure grouping folder)
    
- `*-plan.md` — **at most one active plan**, with optional archived plans
    
- `research.md` — optional, temporary
    
- Additional files directly describing or modelling this thing
    
- Child folders representing components of this thing
    

No other folder types are allowed.

---

# 3. SPECIFICATION FILE

Each specification must adhere to the canonical definition:

> **A specification describes the need for a thing to exist, and its design.**

---

### 3.1 Front Matter

`status: draft | approved | implemented version: x.y created: yyyy-mm-dd last-updated: yyyy-mm-dd used-by:   - (end users "vertical" or other things/components "horizontal")   - ...`

`used-by` distinguishes between:

- **vertical things** used by end users
    
- **horizontal things** used by other components or systems
    

---

### 3.2 Required Sections

`# The Need for This Thing to Exist   ← Demand: what must remain true; reasons, constraints, outcomes. # Design                             ← Supply: how this thing currently meets that need; present-tense reality. # Change Log                         ← Trace of evolution; link decisions, promotions, and approvals.`

These sections define **purpose**, **current reality**, and **evolution**.  
Function is fixed; form is free.

---

### 3.3 Change Log Format

Use dated entries capturing the change, rationale, and references.

`v2 - 2025-06-15 Changes: Added "Remember me" checkbox; removed SMS verification (replaced with email-only)  Rationale: User feedback requested persistent sessions. SMS cost too high.  Notes: See DECISIONS.md D42 for authentication strategy. Updated tests accordingly.`

---

### 3.4 When Specifications Are Mandatory

A spec **must** exist when:

- The thing is an **atomic component**
    
- The thing contains global / shared requirements or design used by its components
    
- The thing has distinct behaviour, constraints, rules, or design worth documenting
    

---

### 3.5 When Specifications Are Optional

A spec may be omitted **only when**:

- The folder purely groups components
    
- The folder has no global requirements or design
    
- All meaningful behaviour lives exclusively in its components
    

---

# 4. SPLITTING & ATOMICITY

This section defines when to decompose a thing into components, and when not to.  
This is one of the most important parts of the model.

---

## 4.1 RULE 1 — Independently-Valuable Rule

Split a thing into components **only if each resulting component is independently valuable**.

A component is independently valuable when it:

- produces a meaningful outcome
    
- is a standalone offering or capability
    
- provides utility on its own
    
- can be reasoned about, designed, and tested separately
    
- is something you'd name in a menu of capabilities
    

If it fails this test → it is an attribute, not a component.

---

## 4.2 RULE 2 — Do Not Split Into Attributes

Attributes belong **inside the specification**, not as components.

Examples of attributes:

- colour
    
- size
    
- typography
    
- border radius
    
- behaviour details
    
- states and variations
    
- internal rules
    
- fields of a data model
    
- low-level design properties
    

Example:  
A `button` has colour, border radius, and variants — these are attributes, not components.

---

## 4.3 RULE 3 — Proportionality Rule

Split a thing if:

- its specification becomes significantly larger or more complex than its siblings
    
- it can be divided into two or more **independently valuable** components
    
- doing so improves clarity, maintainability, or reasoning
    

Do **not** split when:

- splitting produces fragments that depend on each other
    
- the resulting components wouldn’t be independently valuable
    
- the split forces unnatural boundaries
    

---

## 4.4 RULE 4 — Atomic Rule

Stop splitting when:

- further splitting yields fragments that are not independently valuable
    
- the thing is coherent and complete enough on its own
    
- remaining detail expresses only attributes, not meaningful behaviour
    

Atomic components **must** have a specification.

---

## 4.5 RULE 5 — One Active Plan (where work happens)

A thing may have many historical plans, but only **one active plan** at a time.

Plans are where forward-looking work happens for that thing.

All other plans must be:

- archived
    
- renamed
    
- moved into a Done Appendix
    

Naming the plan is optional (e.g., `2024-platform-plan.md`).

---

## 4.6 RULE 6 — Upward Referencing

Components must **not** duplicate design or requirements expressed by a larger thing.

They must reference rather than restate:

`See the design of the larger thing for shared models and constraints.`

---

# 5. SPEC EVOLUTION LIFECYCLE

Each thing follows the same lifecycle:

1. **Need definition (draft)**
    
2. **Optional research** → `research.md`
    
3. **Plan** → create `*-plan.md`
    
4. **Design finalisation**
    
5. **Approval**
    
6. **Implementation & testing**
    
7. **Promotion to implemented**
    

---

# 6. PLAN FILES

### 6.1 Naming

Plan files must end in `-plan.md`.

### 6.2 One Active Plan

Exactly one active plan per thing.

### 6.3 Short-Lived Plans

Archive or delete after completion.

### 6.4 Long-Lived Plans

Completed items move to a “Done Appendix”:

`## Done Appendix <!-- LLM: Do not read -->`

---

# 7. RESEARCH FILE

`research.md` is:

- optional
    
- temporary
    
- intended to support planning
    
- deleted or archived once obsolete
    

---

# 8. RECURSION & MICRO-COSMIC RULE

Every thing is a microcosm of the entire model:

- recursive
    
- identical structure
    
- predictable
    
- scalable
    
- domain-independent
    

The same anatomy applies at every level.