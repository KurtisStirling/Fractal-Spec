## Fractal Specs

This repo uses a documentation model called Fractal Specs - A compositional, recursive, universally applicable documentation model for humans and LLMs.

``` yaml
[thing-name]/                           # Folder represents a thing we want to document
  [thing-name].md                       # Specification: the need for this thing to exist, and its design
  [active-plan].md                      # Optional: the one active plan for how we will change or evolve this thing
  [other.files]                         # Any supporting file that helps model, describe, or explain this thing (e.g., diagrams, models, maps, images, test plans)
  [component-thing-name]/               # A meaningful component of this thing. Component folders follow the same anatomy (fractal) and there may be multiple.

```

Fractal Specs is a **simple repeating structure**:  
each folder represents a real _thing_, and any folders inside it represent _meaningful components_ of that thing.  
Open any folder, and the same pattern repeats — a microcosm.  
No semantics are enforced; the model defines **anatomy only**.  
Users decide what each level represents in their domain.

This guarantees:

- navigation is consistent no matter where you start
- the hierarchy mirrors the structure of the real-world thing
- cognitive load drops because the rules are identical everywhere
- the model works for business, design, engineering, documentation, planning, governance, and creative work

Every folder contains a **spec file** that describes:

> **the need for this thing to exist, and its design.**

Forward-looking work (roadmaps, tasks, experiments, improvements) lives in **optional plan files**, one active plan per folder.  
High-level folders naturally have roadmap-like plans; deeper folders have more task-oriented plans.  
Design decisions belong in the spec file of the thing they affect.

No centralised monolithic documents are required — every piece of documentation lives in the folder it applies to.  
This keeps information local, contextual, and easy for both humans and LLMs to work with.

---

## LLM behavioural expectations

- Don't assume; always verify.
- Ask when requirements are unclear.
- Offer options with pros/cons and a recommended choice.
- Challenge assumptions; user has strong PM/BA skills but is not a developer.
- Work methodically: **propose → confirm → execute**.

---

## LLM startup protocol

1. **Read `Fractal-Specs-Guide.md`** to understand the full rules.
2. **Locate the highest-level active plan** (`*-plan.md`).
    - If more than one exists at the same level, ask the user which one to follow.
    - If no plans exist, say: _“No active plans found. Should we create one?”_
3. **Identify the next item in that plan** and restate it:
    > “According to `{plan-name}`, the next item is `{task}`. Should we work on this?”
4. Proceed only after user confirmation or redirection.

### LLM behavioural expectations

* Don't trust; verify with the user instead of assuming.
* Ask when requirements are unclear.
* Share options with pros/cons and a recommendation plus rationale.
* Challenge assumptions; user has strong PM/BA skills but is not a developer.
* Work methodically: propose → confirm → execute.

### LLM startup protocol:

1) Read `Fractal-Specs-Guide.md` to understand the full rules of the documentation model  
2) Find the highest-level active plan (`*-plan.md`). If multiple at the same level, ask the user which to use.  (if no plans exist say "No plans, make one?")
3) Identify the next item in that plan and restate: “According to {plan}, the next item is {next to do}, should we work on this?”  
4) Proceed only after user confirmation or redirection.



<!-- LLMs: Do not read this section. Verbose human explanation follows -->

# **Fractal Specs**

_A consistent documentation model whose structure repeats at every level._

Fractal Specs is a lightweight skeleton for organising documentation.  
Each folder represents **a real thing**, and any folders inside it represent **meaningful components of that thing**.  
Open any component folder and the pattern repeats — a microcosm of the whole.

The model enforces **no semantics**.  
It defines **anatomy only**.  
Users decide what each level represents in their own domain.

This creates:

- consistent navigation no matter where work begins
    
- predictable organisation for humans and LLMs
    
- reduced cognitive load
    
- applicability from high-level strategy down to deep technical design
    

The hierarchy mirrors the _real-world composition_ of whatever is being documented.  
Because of this, Fractal Specs eliminates the need for centralised monolithic documents — all content lives **exactly where it applies**.

Every folder contains a **spec file** describing:

> **the need for this thing to exist, and its design.**

Forward-looking work (ideas, objectives, roadmaps, tasks, spikes) lives in **optional plan files**, with **one active plan per folder**.  
High-level plans tend to be roadmap-like; deeper plans tend to be smaller and implementation-focused.  
Design decisions always live in the spec file of the thing they affect.

Fractal Specs does not change _what_ you document — only _where you put it_.  
This predictability keeps the entire system lightweight without losing rigour.

---

# **Research → Plan → Implement (RPI) agentic workflow**

Fractal Specs is intentionally compatible with an RPI loop.  
The folder representing a thing becomes the boundary for that loop.

### **Permanent truth**

The spec file is the durable record of truth:

- **Need** (enduring demand, purpose, expectations)
    
- **Design** (current supply, architecture, behaviour, constraints)
    

Some very small components may naturally have only a Design section.

### **Temporary truth**

Active plans and research notes are scaffolding:

- Plans = intent + sequencing
    
- Research = exploration + evidence-gathering
    

Both should eventually be promoted into the spec or discarded.

### **RPI cycle**

1. **Research** — understand the current reality and possible approaches
    
2. **Plan** — decide intent and sequencing
    
3. **Implement** — change the system or thing
    
4. **Promote** — update the spec so it reflects the as-built truth
    

Plans and research are ephemeral; the spec is permanent.

### **Definition of Done**

A change is _done_ when:

- the system/thing has been updated, and
    
- the spec’s Design and/or Need sections reflect the new reality.
    

The plan item and its research should then be archived or removed.

### **Research discipline**

Research should be lightweight and evidence-based.  
When researching code, model reality without critique or speculation.  
Document what _is_.

---

# **Role-based interpretation**

## For Business & Leadership

- **Need** = enduring purpose and value
    
- **Design** = how it works today
    
- **Plan** = one actionable page showing what happens next
    

## For Product Managers

- **Need** = “what good looks like”
    
- **Design** = current behaviour
    
- **Plan** = roadmap → backlog → tasks in one place
    

## For Developers & Engineers

- **Need** = functional and non-functional demand
    
- **Design** = architecture, flows, decisions, current truth
    
- **Plan** = the execution zone (work items, sequencing, Done appendix)
    

---

# **Core principles**

- **Token-optimised for LLMs**: keep specs distilled; avoid raw dumps
    
- **Self-guiding structure**: predictable, consistent, local
    
- **Traceability**: decisions live in the spec where they apply
    
- **Fractal composition**: the anatomy is identical at every level
    
- **Context containment**: work is scoped to the folder you’re in
    

---

# **Examples**

These examples show how the “thing → components” model applies across domains.

---

## Example A: Button Component

`button/   button.md`

Attributes inside the spec:

- colour
    
- typeface
    
- border radius
    
- hover states
    
- variants (primary, danger, ghost)
    

These are **attributes**, not components, because none are independently valuable.

Splitting is appropriate **only** when:

- the spec becomes excessively large, and
    
- there are natural standalone sub-components (e.g., `button-group/`, `split-button/`).
    

---

## Example B: Holiday Planning

`holiday/   flights/   accommodation/   car-hire/   itinerary/   budget/`

Each is independently valuable:

- You can book flights without car hire
    
- You can budget without an itinerary
    
- Each can be designed and delivered separately
    

This is a perfect natural fractal decomposition.

---

## Example C: Post Office Services

`post-office/   postal-services/   moneygram/   cash-withdrawals/   e-top-ups/   car-tax/   foreign-currency/`

Each service is:

- a meaningful, independently valuable capability
    
- a natural component
    
- appropriate to have its own specification
    

---

## Example D: Forest Ecosystem

`forest/   trees/   animals/   soil/   streams/   air/   seasonal-cycles/`

Zoom deeper:

`tree/   roots/   trunk/   branches/   leaves/`

But aspects of leaves such as:

- colour
    
- surface texture
    
- vein structure
    

…are **attributes** of the leaf, not standalone components.  
They belong inside the leaf’s spec.

---
