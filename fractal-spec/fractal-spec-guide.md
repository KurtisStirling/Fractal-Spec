---
version: "1"
---
# Fractal Spec Guide (v1)

## LLM Guide 
LLMs MUST read this section before doing any work.

**Quick reference** — Read sections as needed:
- **1-4, 9** — Core model (read first)
- **2.5** — Version checking
- **2.6** — Navigation helpers
- **3.5** — Multi-level plans
- **5** — When to split components
- **6** — Referencing parent specs
- **6.5** — Exploratory work
- **7** — Definition of Done
- **8** — Behavioral rules
- **10** — Spec template

---

## 1. Core Concept
- Every folder represents **a thing** (some thing we are documenting).
- Child folders are **meaningful components of that thing**.
- Structure repeats fractally: **thing → components → deeper components → atomic components**.
- An **atomic component** is the smallest independently valuable unit and **must have a spec file**.

---

## 2. Anatomy of Every Folder

```
thing/
  thing.md        # SPEC: need + design (permanent truth)
  X-plan.md       # One active plan; forward-looking work
  research.md     # Optional; temporary research
  {...files}      # Files directly describing this thing
  component/      # Meaningful component; same anatomy recursively
```

### Horizontal vs Vertical Components

Use `used-by` frontmatter to signal dependencies.

- **Vertical** = End-user features (checkout, user-profile)
- **Horizontal** = Shared infrastructure consumed by multiple components (data-schema, auth)

**Example:**
```
app/
  checkout/
    checkout.md           # used-by: [end users]
  data-schema/
    data-schema.md        # used-by: [checkout, user-profile, reporting]
```

Signals cross-cutting impact when changes are proposed.

---

## 2.5. Version Compliance

Check the guide's frontmatter or title for the version (e.g., `v1`).

Different versions may have different rules. Confirm version before starting work.

---

## 2.6. Navigation Helpers (Optional)

For 5+ top-level components, add `index.md` at root with:
- One-line component descriptions
- Links to major specs
- Optional: architectural context (vertical vs horizontal)

**Example:**
```markdown
# Project Navigation

### [Projects](./app/projects/projects.md)
End-user feature for project management.

### [Data Schema](./app/data-schema/data-schema.md)
Shared data models. Used by projects and traps.
```

---

## 3. What Goes Where
### Spec (`thing-name.md`)
1. **Need** — why this exists; demand, rules, expectations
2. **Design** — how this works; supply, architecture, behaviour
   - Must conceptually represent code/reality, not replicate it
   - Code snippets OK where useful
3. **Change Log** — max 5 recent entries; refer to git for older history

### Plan (`*-plan.md`)
- Single active plan for this thing
- Roadmap → backlog → tasks
- Completed items → Done Appendix

**When to plan:**
- **High-level**: Almost always (exception: inactive products)
- **Low-level**: Complex work only (refactors, features, multi-file changes)
- **Heuristics**: Plan if work takes >1 hour OR touches multiple files OR needs sequencing OR ≥50k tokens to execute

### Research (`research.md`)
- Temporary input for planning
- Archive as `_research-YYYY-MM-DD.md` or delete after use
- Only for non-trivial investigation

### What NOT to Spec
Don't spec generated artifacts (API docs, build outputs) or external dependencies (Postgres, Redis, AWS).

**Instead:** Mention in parent's Design section.

Example: ✅ `/backend/backend.md` Design: "Uses Redis 7.x for caching" (not ❌ `/redis/redis.md`)

---

## 3.5. Multi-Level Plan Strategy

### Pattern: Scheduler vs Task-List

Plans naturally exist at multiple levels simultaneously:

**High-level plans** (scheduler-like):
- Longer-lived
- Strategic sequencing
- Items reference work areas, not atomic tasks
- Example: "implement edit-project changes"

**Low-level plans** (task-list-like):
- Shorter-lived
- Tactical execution
- Concrete deliverables
- Example: "redesign edit fields UI", "re-write code", "manually test"

### Concrete Example

```
projects/
  projects-plan.md          # High-level: "implement edit-project changes" ← ONE ITEM
  projects.md
  edit-project/
    edit-project-plan.md    # Low-level: specific tasks (redesign, code, test)
    edit-project.md
```

**Lifecycle:**
1. High-level plan item: "implement edit-project changes"
2. Create `edit-project/` folder with its own plan
3. Execute low-level tasks (redesign → code → test)
4. Archive/delete `edit-project-plan.md` when complete
5. Check off high-level item

### Plan Management

**Suggestion**: Try to work on one plan per level at a time for focus.

**Why this helps**: You cannot actually execute multiple things simultaneously at that level of abstraction.

- At the `projects/` level: working on `edit-project` OR `create-project` provides better focus
- At the `edit-project/` level: working on UI redesign OR code rewrite sequentially

**Flexibility**: If multiple concurrent plans at the same level are genuinely useful (e.g., parallel bug fixes + feature work), use them. The suggestion is for focus, not restriction.

**Nested work is fine**: You can work on `projects/edit-project/` (low-level) while that's the active item in `projects/projects-plan.md` (high-level). The focus suggestion applies horizontally, not vertically.

### Granularity Examples: Macro vs Micro

#### Macro (Strategic)
```markdown
# Plan: Projects Q1 2025
## Tasks
- [ ] Implement create-project flow — Maria (Jan)
- [ ] Implement edit-project changes — Dev team (Feb)
- [ ] Add archive-project capability — Alex (Mar)
```
References work areas, not atomic tasks. Weeks/months timeframe.

#### Micro (Tactical)
```markdown
# Plan: Edit Project Implementation
## Tasks
- [ ] Update edit form component with new field layout
- [ ] Add inline validation for project name field
- [ ] Wire up auto-save behavior
- [ ] Manual testing: create → edit → save → verify
```
Concrete deliverables. Hours/days timeframe.

#### Nested Relationship
```
projects/
  projects-plan.md          ← MACRO: "implement edit-project changes"
  edit-project/
    edit-project-plan.md    ← MICRO: specific tasks
```

Macro item spawns component with micro plan. Complete micro → archive micro plan → check off macro item.

---

## 4. Folder Purity
A folder may contain ONLY:
- spec  
- one active plan  
- research  
- files directly describing this thing  
- folders for meaningful components  

Nothing else.

---

## 5. Splitting Rules (Decomposition)
Split a thing into components **only when each component is independently valuable**.

Do **not** split into attributes (e.g., colour, fields, small behavioural details).
Attributes belong **inside** the spec.

Stop splitting when further decomposition would produce non-valuable fragments → atomic component.

### When NOT to Split: Anti-Patterns

**Do not split if:**

1. **Not independently valuable** — `flowers/stem/` is wrong; stem isn't useful alone
2. **< 1 hour of work** — Keep trivially small things inline
3. **Just an attribute** — Never create `color/`, `size/`, `status/` folders
4. **Uncertain** — Ask the user; splitting is collaborative

When unsure, keep content together until proven valuable to separate.

---

## 6. Upward Referencing
Components must not duplicate parent information. Use explicit markdown links with anchors.

**Bad:**
```markdown
See parent for styling rules.
```

**Good:**
```markdown
See [styling rules](../components.md#styling) for shared guidelines.
```

**Pattern:** Relative path + anchor + brief context

---

## 6.5. Lightweight Exploration

Full fractal structure is not always needed:

- **Quick questions** or small tasks: use direct conversation with Claude — no documentation required.
- **Substantial experiments or spikes**: create `spike/` or `experiment/` component at the appropriate level.
  - Example: `trapscan-app/spike/` alongside `/projects` and `/traps`
  - May contain lighter specs or just `research.md` — follow anatomy where it adds value.
  - Use for technical feasibility studies, proof-of-concept work, or evaluating alternatives.
- When complete: promote findings to relevant specs, then archive or delete the spike component.

---

## 7. Lifecycle
1. Define Need
2. Research (optional)
3. Plan
4. Finalise Design
5. Approve
6. Implement
7. Promote (update spec + archive plan/research)

### Definition of "Done"

**Done** = spec.Design accurately reflects production reality.

- Code projects: merged + deployed + spec updated
- Implemented ≠ Done; Deployed ≠ Done; Both synchronized = Done

---

## 8. LLM Behavioural Requirements
- Do not assume — ask when unclear  
- Always check existing specs and plans  
- Do not invent structure; follow the anatomy strictly  
- Update the correct thing’s spec when truth changes  
- Put forward-looking work in that thing’s plan  
- Maintain folder purity  
- Work locally unless told otherwise  

---

## 9. LLM Startup Protocol

**First interaction:** Read Sections 1-4 and 9 minimum. Other sections as needed.

**Then:**
1. Find highest-level active plan
   - If multiple at same level: ask which to use
   - If none exist: ask "Create a plan?"
2. Identify next plan item
3. Ask: "Next item is X — proceed?"
4. Execute only after confirmation

**STOP at Section 10. Do NOT read past the 🔻 marker.**

---

## 10. Spec Template

Use `spec-template.md` when creating new specs. It includes minimal required sections plus optional subsections you can add as needed.

---


# 🔻 **LLMs: Do not read below this point. For Human consumption only.**


# **Fractal Spec**

*A consistent documentation model that repeats at every level.*

Fractal Spec is a lightweight organisational skeleton.  
Each folder represents **a thing**, and any child folders represent **meaningful components of that thing**.  
Open a component folder and the same pattern repeats — a microcosm.

The model defines **anatomy, not semantics**.  
Users decide what each level means in their domain.

This guarantees:

- predictable navigation  
- cognitive ease  
- applicability across business, product, engineering, research, planning, and creative work  

Because the structure mirrors what it describes, there is no need for centralised monolithic documents.  
All information lives **exactly where it applies**.

Every folder contains a **spec** describing:

> **the need for this thing to exist, and its design.**

Forward-looking work lives in **one active plan** per folder.  
High-level things have roadmap-like plans; deeper things have more task-like plans.  
Design decisions always live in the spec of the thing they affect.

Fractal Spec changes *where* you put information, not *what* you document.

---

# Research → Plan → Implement (RPI) Workflow

### Permanent truth
Specs hold the durable truth:  
- **Need**  
- **Design**  
- **Change Log**

### Temporary truth
Plans and research are scaffolding:
- ephemeral  
- promote or discard after use  

### RPI loop
1. **Research** — understand reality  
2. **Plan** — decide intent + sequencing  
3. **Implement** — change the thing  
4. **Promote** — update spec + retire plan/research  

A change is *done* when the spec matches reality.

---

# What's in it for you?

## **For Business & Leadership**

Fractal Spec shows your organisation in a structured, comprehensible way:

* **Requirements** show the enduring needs and reasons for the system’s existence.
* **Design** shows how it works today.
* **Plan** shows what will happen next and why.

Your contributions fit cleanly:

* Strategic goals → *Requirements* (direction reinforces the need)
* Operational processes, constraints → *Design*
* Roadmaps, commitments → *Plan*

This creates alignment without heavy governance or documentation overhead.

---

## **For Product Managers**

Fractal Spec becomes a single map for intent, reality, and delivery:

* **Requirements** = what “good” looks like
* **Design** = what exists
* **Plan** = roadmap → backlog → tasks

Your usual outputs translate directly:

* Roadmaps & prioritisation → *Plan*
* Acceptance criteria → *Requirements*
* Discovery notes → *work/Research.md*

You don’t maintain multiple backlogs; **the plan at the relevant subject is where the work is done.**

---

## **For Developers & Engineers**

Fractal Spec mirrors the way systems decompose:

* **Requirements** capture demand: behaviours, constraints, edge cases, invariants.
* **Design** captures supply: architecture, data models, flows, decisions.
* **Plan** is where implementation work is expressed and broken down.

Your artefacts map naturally:

* Diagrams, schemas → *Design*
* Edge cases, expected behaviours → *Requirements*
* Refactors & implementation tasks → *Plan*

It keeps intent separate from implementation while avoiding documentation sprawl.

---

# Core Principles
- **Token efficient** for LLMs  
- **Predictable**: identical structure everywhere  
- **Traceable**: Change Logs show evolution  
- **Local**: work lives where it applies  
- **Fractal**: each folder a microcosm  

---

# Examples

## Example A: Button
```
button/
  button.md
```
Attributes belong inside the spec:
- colour  
- typeface  
- border radius  
- states  
- variants

Split only if independently valuable (e.g., `button-group/`).

---

## Example B: Holiday Planning
```
holiday/
  flights/
  accommodation/
  car-hire/
  itinerary/
  budget/
```
Each is independently valuable → valid components.

---

## Example C: Post Office Services
```
post-office/
  postal-services/
  moneygram/
  cash-withdrawals/
  e-top-ups/
  car-tax/
  foreign-currency/
```
Each is a standalone service → component.

---

## Example D: Forest Ecosystem
```
forest/
  trees/
    branches/
    trunks/
    roots/
  animals/
  soil/
  streams/
  seasonal-cycles/
```


---

# End of Fractal Spec Guide (v1)
