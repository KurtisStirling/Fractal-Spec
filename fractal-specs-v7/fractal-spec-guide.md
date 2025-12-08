# Fractal Spec Guide (v7)

## 🧠 Fractal Specs — LLM Guide (Terse + Token‑Optimised)
LLMs MUST read this section before doing any work.

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
  thing.md        # SPEC: need for this thing to exist + its design (permanent truth)
  X-plan.md       # One active plan only; forward-looking work happens here
  research.md     # Optional; temporary research informing planning/decisions
  {...files}      # Only files that directly describe/model/explain this thing
  component/      # Meaningful component of the thing; same anatomy recursively
```

### Horizontal vs Vertical Components

Use the `used-by` frontmatter field to signal **horizontal shared services** vs **vertical value-stream components**.

**Vertical vs Horizontal:**
- **Vertical** = End-user facing features or value streams (e.g., checkout, user-profile)
- **Horizontal** = Shared infrastructure/services consumed by multiple components (e.g., data-schema, auth, validation)

**When to use `used-by`:**
Add this field to specs when the component serves multiple consumers, signaling it's a horizontal dependency.

**Example:**

Single app with shared infrastructure:
```
app/
  checkout/
    checkout.md           # used-by: [end users]
  user-profile/
    user-profile.md       # used-by: [end users]
  data-schema/
    data-schema.md        # used-by: [checkout, user-profile, reporting]
```

This signals dependency relationships and helps LLMs understand cross-cutting impact when changes are proposed.

---

## 2.5. Version File

Every repository using Fractal Specs **must** include a `.fractal-specs-version` file in the root directory.

**Purpose:** LLMs read this file to determine which version of Fractal Specs rules to follow.

**Format:** Simple text file containing the version identifier (e.g., `v7`).

**Example:**
```
v7
```

**Why this matters:** As Fractal Specs evolves (v8, v9, etc.), this file ensures LLMs apply the correct rules for your repository, preventing conflicts between versions.

**LLM Requirement:** Before doing any work, read `.fractal-specs-version` from the repository root to confirm which guide version to follow.

---

## 2.6. Navigation Helpers (Optional)

**For large or complex structures, add `index.md` or `map.md` at the repo root.**

**Purpose:**
- Quick orientation for humans exploring the codebase
- Fast overview for LLMs before diving deep
- Roadmap showing major components with clickable links

**When to use:**
- 5+ top-level components
- Complex domain with non-obvious organization
- Onboarding new team members or collaborators

**What to include:**
- Brief one-line descriptions
- Links to major component specs
- Optional: architectural context or layering (vertical vs horizontal)

**Example:**
```
index.md                    # Navigation helper at root
app/
  projects/
    projects.md
  traps/
    traps.md
  data-schema/
    data-schema.md
```

See `navigation-example.md` for a realistic structure map.

---

## 3. What Goes Where
### Spec (`thing.md`)
A specification describes:
1. **Need** — why this thing exists; demand, rules, expectations
2. **Design** — how this thing currently exists; supply, architecture, behaviour
   - Must **conceptually and logically** represent the (physical) code/reality
   - Can include code snippets where useful
   - Intent: make code easy to understand, not replicate it
3. **Change Log** — trace of evolution
   - **Keep maximum 5 most recent entries** (token efficiency)
   - For older history: add note "See git history for full change log"

### Plan (`*-plan.md`)
- The single active plan for this thing
- Contains roadmap → backlog → tasks
- Completed items move to `Done Appendix`

**When plans are needed:**
- **High-level things**: Almost always have a plan (roadmap/backlog style)
  - Exception: Inactive products with no development may skip formal plans
- **Low-level work**:
  - Simple tasks (bug fixes, minor tweaks): Just converse and execute — no plan needed
  - Complex tasks (refactors, new features, multi-step changes): Create a plan first
- **Heuristic**: If the work requires > 1 hour OR touches multiple files/components OR needs sequencing → plan it

### Research (`research.md`)
- **Temporary** — input for planning, then archived or deleted
- After plan created: archive as `_research-YYYY-MM-DD.md` or delete if captured in plan/spec
- For complex tasks, see **Research → Plan → Implement Workflow** for knowledge compression pattern
- Not always needed — only for non-trivial investigation

### What NOT to Spec
**Don't create separate specs for:**
- **Generated artifacts** — API docs from OpenAPI, build outputs, test coverage reports, compiled assets
- **External dependencies** — Postgres, Redis, AWS S3, third-party SaaS tools

**Why:** These aren't things you're building; they're outputs or external systems. Spec'ing them creates bloat and duplicates documentation that exists elsewhere.

**Instead:** Mention them in the parent thing's **Design** section as architectural choices.

**Examples:**
- ❌ Don't create `/backend/api-docs/api-docs.md` for generated OpenAPI docs
- ✅ Do write in `/backend/backend.md` Design: "API documentation auto-generated from OpenAPI spec at build time"
- ❌ Don't create `/infrastructure/redis/redis.md` for Redis
- ✅ Do write in `/backend/backend.md` Design: "Uses Redis 7.x for session caching and rate limiting"

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

Plans naturally vary in granularity depending on their level in the hierarchy. High-level plans are strategic and scheduler-like, while low-level plans are tactical and task-list-like.

#### Macro-Level Plan Example (Strategic/Scheduler)

**File**: `/trapscan-app/projects/projects-plan.md`

```markdown
# Plan: Projects Q1 2025

## Context
- Subject: trapscan-app/projects/
- Focus: Complete core project management workflows
- Timeframe: Q1 2025

## Objectives
1. Enable users to create and manage projects
2. Support collaborative editing
3. Implement project archival workflow

## Tasks
- [ ] Implement create-project flow — Maria (Jan)
- [ ] Implement edit-project changes — Dev team (Feb)
- [ ] Add archive-project capability — Alex (Mar)
- [ ] Performance optimization pass — TBD (Mar)

## Risks
- Edit-project has UI/UX redesign dependency
- Archive flow needs DB migration strategy
```

**Characteristics**:
- References work areas, not atomic tasks
- Timeframes in weeks/months
- Owners assigned to areas of work
- Each item could spawn its own component with a plan

#### Micro-Level Plan Example (Tactical/Task-List)

**File**: `/trapscan-app/projects/edit-project/edit-project-plan.md`

```markdown
# Plan: Edit Project Implementation

## Context
- Subject: trapscan-app/projects/edit-project/
- Parent plan item: "Implement edit-project changes" (projects-plan.md)
- Current state: Design approved; ready to implement

## Objectives
- Redesigned UI deployed to production
- All edit workflows functional
- Manual testing complete

## Tasks
- [ ] Update edit form component with new field layout
- [ ] Add inline validation for project name field
- [ ] Wire up auto-save behavior
- [ ] Update project detail page to show edit button
- [ ] Manual testing: create → edit → save → verify
- [ ] Update projects.md Design section with new edit flow

## Risks
- Auto-save conflicts if multiple users editing (out of scope for v1)
```

**Characteristics**:
- Concrete, actionable deliverables
- Timeframe in hours/days
- Each task is implementable immediately
- Clear completion criteria

#### Nested Relationship

```
trapscan-app/
  projects/
    projects-plan.md          ← MACRO: "implement edit-project changes"
    projects.md
    edit-project/
      edit-project-plan.md    ← MICRO: specific implementation tasks
      edit-project.md
```

**How they relate**:

1. **Macro plan** (`projects-plan.md`) has one item: "Implement edit-project changes"
2. This spawns a **component** (`edit-project/`) with its own spec and micro plan
3. **Micro plan** (`edit-project-plan.md`) breaks down the work into concrete tasks
4. When all micro tasks complete → archive `edit-project-plan.md`
5. Check off macro plan item "Implement edit-project changes"

**Key insight**: The macro plan item stays open until ALL micro work (including spec updates and deployment) is complete. This maintains alignment between levels.

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

**Do not split when:**

1. **The component is not independently valuable**
   - Example: In a `flowers/` component, creating `stem/` or `petals/` subfolders is wrong — these are not useful in isolation
   - Good split: `flowers/` (independently valuable)
   - Bad splits: `flowers/stem/`, `flowers/petals/` (fragments with no standalone value)

2. **The component would be < 1 hour of work**
   - If the resulting component is trivially small, it belongs as content in the parent spec, not as its own folder
   - Heuristic: If it's less than an hour to implement/define, keep it inline

3. **It's really just an attribute or property**
   - Attributes like color, size, status, labels always stay inside the spec
   - Never create folders for: `color/`, `size/`, `title/`, `enabled/`
   - These are descriptive properties, not components

4. **You're uncertain whether to split**
   - **Ask the user** — splitting is collaborative, not an LLM decision
   - The user understands domain value; when in doubt, propose and confirm

**Remember:** Over-splitting creates navigational friction. When unsure, err toward keeping content together until proven valuable to separate.

---

## 6. Upward Referencing
Components must **not** duplicate anything already defined by their parent thing.

Instead of duplicating parent information, reference it explicitly using markdown links with anchors.

### Why Explicit Links Matter
- **Easier navigation**: Readers (human and LLM) can jump directly to the referenced content
- **Maintainability**: Changes propagate naturally without manual sync
- **Better DX**: No hunting through folder hierarchies to find "the parent" or "shared rules"

### Examples

**Bad: Vague text references**
```markdown
See parent for styling rules.
Refer to the larger component for authentication details.
Check the design of the parent thing for shared configuration.
```

**Good: Explicit markdown links with anchors**
```markdown
See [styling rules](../components.md#styling) for shared visual guidelines.
Authentication follows [the auth flow](../../backend/backend.md#authentication) defined at the backend level.
Uses [shared configuration schema](../app.md#configuration) from the parent app.
```

**Pattern**: Always include:
1. Relative path to the parent/sibling spec
2. Anchor (`#section-name`) pointing to the specific section
3. Brief context about what's being referenced

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

A change is **done** when `spec.Design` accurately reflects production reality.

For code projects:
- Code is merged to main branch AND deployed to production
- The spec's Design section describes the deployed state
- All downstream specs are updated if affected

For non-code projects:
- The thing exists in its intended form
- The spec's Design section describes the current state

**Key distinctions:**
- **Implemented** ≠ Done (code exists but not merged/deployed)
- **Deployed** ≠ Done (reality changed but spec hasn't)
- **Done** = Production reality AND spec.Design are synchronized

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
1. Read this guide  
2. Locate the highest-level active plan  
   - If multiple at the same level: ask the user which to use  
   - If no active plans exist: ask “Create a plan?”  
3. Identify the next plan item  
4. Ask: “Next item is X — proceed?”  
5. Execute only after user confirmation  

---


# 🔻 **LLMs: Do not read below this point. For Human consumption only.**


# **Fractal Specs**

*A consistent documentation model that repeats at every level.*

Fractal Specs is a lightweight organisational skeleton.  
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

Fractal Specs changes *where* you put information, not *what* you document.

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

Fractal Specs shows your organisation in a structured, comprehensible way:

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

Fractal Specs becomes a single map for intent, reality, and delivery:

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

Fractal Specs mirrors the way systems decompose:

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

# End of Fractal Spec Guide (v7)
