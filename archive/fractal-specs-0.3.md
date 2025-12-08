# **Fractal Specs**

*A consistent documentation model that repeats at every level.*

Fractal Specs is a lightweight skeleton organising your documentation: a simple repeating structure where each folder represents a subject, acting as a *microcosm* of the level above it and a *macrocosm* of the levels within it. It gives you only the context relevant at that layer, making it easy for both humans and AI to understand the system without noise or overload. It is not a methodology but a skeleton—just enough structure to organise your work while leaving you completely free in how you write, design, and deliver inside it.

Fractal Specs imposes no semantics. You decide what each subject represents—whether a business capability, a product area, a subsystem, a feature, or a single UI detail. Subjects inherit context from their macrocosm and provide context to their microcosms. All of your existing documentation—business cases, delivery plans, architecture diagrams, API references, code examples—all have a place within this system. The predictability lowers cognitive load and makes navigation intuitive, no matter where someone enters the hierarchy.

All forward-looking work in Fractal Specs—strategy, objectives, roadmaps, backlogs, sprints, development tasks—collapses into a single concept: **planning**. Plans live at every level: aspirational in macrocosms, concrete and actionable in microcosms. This emerges from the work itself, not from rules imposed by the framework. Requirements represent ongoing **demand** (what must remain true), Design represents current **supply** (how the system currently meets that demand), and Plans describe how supply will evolve. There is no central roadmap or to-do list—**the plan at the subject is where the work is done**. Fractal Specs enforces only the *function* of each file—never the form.

The payoff: it changes *where* you put things, not *what* you document. The same kinds of content live in the same place at every level, so navigation stays consistent without heavyweight rules.

---

# **Summary of Breakthroughs (agentic overlay)**

* **RPI generalisation** — The Research → Plan → Implement loop is a universal, agent-friendly framing for change, not just coding. Each subject is a small RPI loop.
* **Dual-truth architecture** — Requirements/Design are permanent truths (demand/supply now). Plan/Research are temporary scaffolding that expire when promoted.
* **Fractal structure** — Every layer uses the same anatomy; subjects are microcosms and macrocosms simultaneously.
* **Draft → Promote workflow** — Work is complete only when reality (code) and current truth (Design/Requirements) are updated to match.
* **Minimal semantics** — Enforce the function of each file, never its format. Leave teams free to express content how they like.
* **LLM-friendly** — Predictable, local context boundaries make AI collaboration safer and more reliable.

---

# **Research > PIan > Implement Agentic Workflow 

* **Permanent truth** — `Requirements.md` (demand) and `Design.md` (supply) are the authoritative, durable statements of intent and reality at this subject. Some very small subjects may carry only a Design if demand is self-evident.
* **Temporary truth** — `work/Plan.md` and any `work/Research.md` are scaffolding that should be promoted or discarded. Plans are where the work is done, but they are not the record of truth.
* **RPI loop** — Research (understand current reality and options) → Plan (decide intent and sequencing) → Implement (change the system) → Promote (update Design/Requirements; retire obsolete plan/research). Treat this as an agentic overlay: the subject itself is the boundary for local RPI cycles.
* **Done definition** — A change is done when the implementation is shipped and Design/Requirements reflect the as-built system. Plans and research notes should be cleaned up or archived after promotion.
* **Research discipline** — Keep research lightweight. When researching code, follow the stance from `stolen-commands-RPI/research_codebase.md`: document what exists (paths, flows, decisions) without critique; prefer direct evidence over speculation.

---

# **Optional defaults / add-ons (format is free; function is fixed)**

Fractal Specs mandates only *what each file does*, never how it is formatted. If you want ready-made patterns, these are opt-in “sensible defaults”:

* **Requirements defaults (optional)** — Capture demand however you like. A helpful pattern is `What / Why / Status / Priority`, with a compact HTML-wrapped changelog if you want traceability.
* **Design defaults (optional)** — Stick to current truth. Optional helpers: a small YAML frontmatter (`created`, `last-updated`, `version`, `used-by`) and an HTML-wrapped changelog for drift tracking.
* **Planning defaults (optional)** — Keep Plan.md as the single backlog/roadmap/task list at that subject; avoid parallel backlogs elsewhere.
* **Research defaults (optional)** — Keep raw input and analysis in `work/Research.md` or scratch files; expire them after promotion.

---

# **Audience Guides**

## **For Business & Leadership**

Fractal Specs shows your organisation in a structured, comprehensible way:

* **Requirements** show the enduring needs and reasons for the system’s existence.
* **Design** shows how it works today.
* **Plan** shows what will happen next and why.

Your contributions fit cleanly:

* Strategic goals → *Requirements*
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

# **Work execution & optionality**

* **Mandatory core** — Every subject should have a Design as the current truth; a Requirements file is strongly recommended for demand, but tiny technical substructures may rely on an implied demand and just carry a Design.
* **Optional scaffolding** — work/Plan, work/Research, Resources (collateral), and Components are all optional; use them when they add clarity. If you do create them, keep Plans and Research temporary and promote or archive after use.
* **Execution boundary** — The subject is the unit of work. Research and planning happen locally; implementation updates supply; promotion updates permanent truth.
* **Validation aids** — Stable collateral (diagrams, ERDs, test run-sheets/tools) can live alongside the subject as an add-on folder; think of it as embedding rich context a Markdown file cannot hold.

---

# **File & folder naming**

* **Core files (Title Case):** `Design.md`, `Requirements.md` (permanent), `Plan.md`, `Research.md` (temporary), and `Supporting-Files/`. These are the model’s anchor files—keep them easy to spot. If you must rename (e.g., Demand/Supply, Problem/Solution), keep the function and be consistent within the subject.
* **work/**: keep lowercase to signal temporariness. The files inside stay Title Case (e.g., `Plan.md`, `Research.md`).
* **Other files/folders:** pick a convention and stick to it; kebab-case is the sensible default (e.g., `billing-sequence.png`, `auth-flow.md`). A noun plus qualifier works well (`auth-flow`, `billing-sequence`, `orders-erd`).
* **Supporting-Files/**: keep Title Case; it should hold distilled, referenced collateral that explains the current Design, not a dumping ground. You can rename it if your org insists, but preserve its role.
* **Multiple Requirements files are fine:** each subject has its own scoped `Requirements.md`; the path disambiguates (e.g., `Billing/Requirements.md` vs `Admin/Requirements.md`).

---

# **Fractal Specs, Described Using Fractal Specs**

*A fully recursive, self-describing meta-model.*

```
Fractal-Specs/
  Requirements.md
  Design.md
  work/
    Plan.md
  Components/
    Structure/
      Requirements.md
      Design.md
    Semantics/
      Requirements.md
      Design.md
    Files/
      Requirements.md
      Design.md
    Behaviour/
      Requirements.md
      Design.md
    Planning-System/
      Requirements.md
      Design.md
```

---

## **Fractal-Specs/Requirements.md**

*The enduring demand placed on the documentation model.*

R01 — Provide a predictable, repeating structure at every level.
R02 — Impose no semantics on hierarchy.
R03 — Remain lightweight and minimal.
R04 — Cleanly separate demand (Requirements), supply (Design), and future intent (Plan).
R05 — Preserve enduring intent and rationale.
R06 — Prevent Chesterton’s Fence failures.
R07 — Enable scoped reasoning for humans and AI.
R08 — Support infinite recursion.
R09 — Avoid prescribing workflow or ceremony.
R10 — Unify all forward-looking work into planning.
R11 — “Plan is where the work is done”; no centralised backlog.

---

## **Fractal-Specs/Design.md**

*How Fractal Specs currently satisfies the above demand (current supply).*

D01 — Recursive folder anatomy implemented (Requirements, Design, Plan, Subcomponents).
D02 — Meaning-free hierarchy implemented.
D03 — Requirements implemented as present-tense demand.
D04 — Design implemented as present-tense supply.
D05 — Unified Plan.md implemented; Backlog removed.
D06 — AI-friendly local context boundaries in place.
D07 — Decomposition shown via component folders.
D08 — Plans serve as the execution zone at each subject.

---

## **Fractal-Specs/work/Plan.md**

*How supply will evolve to better meet demand.*

### **High-Level Plan**

* Add diagrams illustrating microcosm/macrocosm relationships.
* Publish a starter repository template.
* Write onboarding guidance for teams adopting the model.

### **Expanded Micro-Level Example (demonstrating deeper nesting)**

* Structure Component → Add examples for a single UI control as a subject.
* Planning-System Component → Show Plan decomposition (e.g., roadmap item → task).
* Files Component → Add examples of alternative file forms (lists, prose, diagrams).

---

# **Component Breakdown**

Each major concept of Fractal Specs is itself a subject with its own demand (Requirements) and supply (Design).

---

## **Components/Structure/Requirements.md**

R01 — Define minimal files: Requirements, Design, Plan.
R02 — Support optional Plan.
R03 — Ensure recursion at any depth.
R04 — Allow arbitrary decomposition granularity.

---

## **Components/Structure/Design.md**

D01 — Implemented subject anatomy:

```
Subject/
  Requirements.md
  Design.md
  work/
    Plan.md
  Subcomponents/
```

D02 — Works across all scales (system → feature → UI element).

---

## **Components/Semantics/Requirements.md**

R01 — Never enforce meaning on a folder level.
R02 — Permit different interpretations for business, PMs, developers.
R03 — Allow re-labelling or grouping without structural change.

---

## **Components/Semantics/Design.md**

D01 — Meaning-free hierarchy implemented.
D02 — Examples show user-defined semantics at all levels.

---

## **Components/Files/Requirements.md**

R01 — Requirements.md must capture ongoing demand.
R02 — Design.md must capture current supply.
R03 — Plan.md must express forward-looking work.
R04 — All file formats must remain unrestricted.

---

## **Components/Files/Design.md**

D01 — Requirements capture enduring needs.
D02 — Design reflects real, current behaviour.
D03 — Plan is unified planning mechanism.
D04 — Function enforced; form unconstrained.

---

## **Components/Behaviour/Requirements.md**

R01 — Support lifecycle: demand → planning → supply update.
R02 — Maintain local reasoning at each subject.
R03 — Allow partial updates without global rewrite.
R04 — Roll up completion from microcosms to macrocosms.

---

## **Components/Behaviour/Design.md**

D01 — Lifecycle implemented through Requirements → Plan → Design updates.
D02 — Demonstrated through this meta-model.

---

## **Components/Planning-System/Requirements.md**

R01 — Future work must be captured solely through Plan.md.
R02 — Plans must nest fractally.
R03 — Support both high-level strategic and low-level tactical planning.
R04 — Avoid enforcing workflow.

---

## **Components/Planning-System/Design.md**

D01 — Unified Plan.md implemented.
D02 — Backlog removed.
D03 — Demonstrated through nested Plans in this meta-model.

---

# **Supporting-Files folder (stable collateral)**

Use `Supporting-Files/` for durable artefacts that help explain current supply. Contents might include org charts, diagrams, ERDs, schemas, UI mocks, data contracts, or even living validation aids such as test run-sheets. Rules of thumb:

* Reference items from Design; if they are not referenced, archive them.
* Keep drafts, noisy notes, and experiments in `work/` instead.
* Treat anything here as part of current truth: update or delete if it drifts.

---

# **Positioning / Related Work**

Fractal Specs sits in the space of documentation and architecture modelling but differs significantly from established models:

### **C4 Model**

Focuses on layered architectural **diagrams** (Context → Container → Component → Code).
Not recursive at the file level; does not provide a universal documentation skeleton; no supply/demand framing.

### **arc42**

A large, structured **architecture documentation template**.
Heavyweight, fixed sections, non-fractal, not semantic-agnostic.

### **4+1 View Model**

Uses multiple simultaneous architectural views (Logical, Development, Process, Physical + Scenarios).
Powerful for architecture, but not a recursive documentation model and does not define file roles or hierarchy anatomy.

### **Agile Documentation / “Just Enough Documentation”**

Guides *how much* to document, not *how* to structure documentation.
Does not define supply/demand, fractal recursion, or unified planning.

### **Component Libraries (e.g., fractal.build)**

Documentation tooling for UI components; unrelated to systemic documentation skeletons.

**Fractal Specs is distinct** in combining:

* a recursive skeleton,
* semantic freedom,
* the supply/demand interpretation of Requirements/Design,
* a unified planning mechanism,
* and a strict “enforce function, not form” philosophy.

No widely known model matches this combination.

---

# **FAQ**

### **What makes it “fractal”?**

The same tiny anatomy—Requirements, Design, Plan—recurs at every level.
Each subject is a microcosm of its parent and a macrocosm of its children.

### **Why is this a skeleton and not a methodology?**

Only the folder structure and file roles are fixed.
How you express content is entirely up to you.

### **How does the Requirements vs Design split work?**

Requirements = demand (ongoing needs, reasons, behaviours).
Design = supply (current implementation meeting that demand).
Plan = how supply will evolve.

### **Does it impose semantics or workflow?**

No.
You decide what each subject represents and how planning is done.

### **How does planning work here?**

There is no central backlog.
Each subject’s Plan.md is **where the work is done**.
Plans nest and roll upward naturally.

### **How large or small should a subject be?**

Any size.
A whole product can be a subject; a single interface control can be a subject.

### **Is this heavy or complex?**

No—extremely light.
Function is enforced, form is unconstrained.

# Anatomy

Subject/
├─ Design.md              ← Supply: what exists now (current reality) — mandatory
├─ Requirements.md        ← Demand: what must remain true — recommended; may be implicit for tiny technical substructures
├─ work/ (optional)       ← Where work happens; temporary; ephemeral
│   ├─ Plan.md            ← Future intent (roadmap → backlog → tasks)
│   ├─ Research.md        ← Notes, analysis, spikes
│   ├─ Experiments.md     ← Trial designs, prototypes, scratch thinking
│   └─ ...                ← Any other temporary scratch files
├─ Supporting-Files/ (optional) ← Stable collateral (org charts, diagrams, schemas, validation aids) referenced by Design
├─ component-a/ (optional)← Child subject representing a sub-structure, with folder structure the same as this one; a microcosm.
└─ component-b/ (optional)


## Tree Diagram

Subject/   ← A unit of meaning (product, feature, service, UI, etc.)
│
├─ Design.md         ← Supply (qualitative; required)
│   - How it currently works
│   - Architecture, flows, data, decisions
│
├─ Requirements.md   ← Demand (qualitative; recommended)
│   - What this subject must provide
│   - Why it exists; ongoing needs and constraints
│
└─ work/ (optional)
    └─ Plan.md       ← Change / Work (optional but recommended when change is active)
        - Future intent for this subject
        - Roadmap items, backlog, tasks
        - "The plan at this subject is where the work is done."

(Optionally)
Subject/
└─ Components/
    ├─ Component-A/
    ├─ Component-B/
    └─ Component-C/
        (each is a Subject with the same anatomy)

## Skeleton Anatomy Diagram

Project Documentation (using Fractal Specs)
└─ Product/                           (Subject)
   ├─ Requirements.md                 (Demand: what must remain true)
   ├─ Design.md                       (Supply: what exists now)
   ├─ work/ (optional)
   │   └─ Plan.md                     (Future intent; where the work is done)
   ├─ Supporting-Files/ (optional)           (Collateral referenced by Design)
   └─ Components/                     (Components = parts of this subject)
       ├─ Onboarding/                 (Component = Subject)
       │   ├─ Requirements.md
       │   ├─ Design.md
       │   ├─ work/ (optional)
       │   │   └─ Plan.md
       │   ├─ Supporting-Files/ (optional)
       │   └─ Components/
       │       └─ ...
       ├─ Billing/
       │   ├─ Requirements.md
       │   ├─ Design.md
       │   ├─ work/ (optional)
       │   │   └─ Plan.md
       │   └─ Supporting-Files/ (optional)
       └─ Admin-Portal/
           ├─ Requirements.md
           ├─ Design.md
           ├─ work/ (optional)
           │   └─ Plan.md
           └─ Supporting-Files/ (optional)

## Micro ↔ Macrocosm Zoom (Business-Level Example)

[ Macrocosm: Organisation ]
┌───────────────────────────────────────────────┐
│ Subject: Organisation                          │
│  - Requirements (org-wide demand: mission,     │
│                  compliance, revenue goals)    │
│  - Design (current operating model:            │
│            structure, systems, org chart)      │
│  - Plan (strategic initiatives; multi-year     │
│           goals; transformation programmes)    │
└───────────────────┬─────────────────────────────┘
                    │ Components (departments)
                    ▼
        [ Subject: Operations Dept ]        [ Subject: Finance Dept ]
        ┌────────────────────────────┐      ┌────────────────────────────┐
        │ - Requirements (Ops demand:│      │ - Requirements (Finance     │
        │    service levels,         │      │    demand: reporting, audit │
        │    consistency, workflows) │      │    accuracy, budgeting)     │
        │ - Design (current teams,   │      │ - Design (current systems,  │
        │    processes, tools)       │      │    charts, controls)        │
        │ - Plan (Ops improvements,  │      │ - Plan (forecasting,        │
        │    automation, team        │      │    optimisation, tooling)   │
        │    restructuring)          │      └───────────────┬─────────────┘
        └───────────────┬────────────┘                      │ Components
                        │                                    ▼
                        │                          [ Subject: Payroll Team ]
                        ▼                          ┌────────────────────────┐
         [ Subject: Clinical Services ]            │ - Requirements         │
         ┌────────────────────────────┐            │ - Design               │
         │ - Requirements (clinical    │           │ - Plan                 │
         │    standards, KPIs, safety)│           └────────────────────────┘
         │ - Design (current service  │
         │    delivery, staffing,     │
         │    pathways, tools)        │
         │ - Plan (new models of care,│
         │    capacity planning,      │
         │    governance upgrades)    │
         └─────────────┬──────────────┘
                       │ Components (teams)
                       ▼
      [ Subject: Physiotherapy Team ]     [ Subject: Nursing Team ]
      ┌───────────────────────────────┐   ┌───────────────────────────────┐
      │ - Requirements (care demand,  │   │ - Requirements (care ratios,  │
      │    skill mix, coverage)       │   │    standards, patient safety) │
      │ - Design (current staff,      │   │ - Design (current shift model,│
      │    scheduling, treatment      │   │    workflows, systems)        │
      │    pathways, tools)           │   │ - Plan (training, rostering   │
      │ - Plan (new pathways, tooling │   │    improvements, process       │
      │    upgrades, training)        │   │    refinement)                 │
      └───────────────────────────────┘   └───────────────────────────────┘


# "What goes where?" decision tree


                                ┌────────────────────────────┐
                                │  START: I have content     │
                                │  related to this subject.  │
                                └───────────────┬────────────┘
                                                │
                     ┌──────────────────────────┴──────────────────────────┐
                     │                                                     │
     ┌───────────────▼───────────────┐                     ┌───────────────▼───────────────┐
     │Q1: Is it only historical,     │                     │Q2: Is it raw, noisy,          │
     │obsolete, or no longer true?   │                     │undistilled, or mixed-topic    │
     │(e.g. past plans, expired      │                     │input? (e.g. meeting notes,    │
     │constraints, old project scope)│                     │dumped tickets, unrefined text)│
     └───────────────┬───────────────┘                     └───────────────┬───────────────┘
                     │Yes                                              Yes │
                     ▼                                                   ▼
         ┌───────────────────────┐                         ┌──────────────────────────┐
         │ OFF-RAMP: Archive or  │                         │ Put in work/ as          │
         │ keep outside Fractal  │                         │ Research/Scratch input:  │
         │ Specs skeleton.       │                         │   work/Research.md       │
         └───────────────────────┘                         │   work/Scratch.md        │
                     │                                     └───────────────┬──────────┘
                     │No                                                  No │
                     └───────────────────────────────────────────────────────┘
                                                │
                                                ▼
                            ┌───────────────────┴────────────────────┐
                            │Q3: Is it describing what SHOULD be     │
                            │true, independent of implementation?    │
                            │(needs, rules, constraints, behaviour,  │
                            │reasons, expectations, outcomes)        │
                            └───────────────────┬────────────────────┘
                                                │Yes
                                                ▼
                                  ┌──────────────────────────┐
                                  │ Put in Requirements.md   │
                                  │ (Demand: what must       │
                                  │ remain true now)         │
                                  └───────────┬──────────────┘
                                              │No
                                              ▼
                          ┌───────────────────┴─────────────────────┐
                          │Q4: Is it describing what IS currently   │
                          │true about this subject?                 │
                          │(current behaviour, structure, rules,    │
                          │decisions, models at a human-readable    │
                          │level – not line-by-line code)           │
                          └───────────────────┬─────────────────────┘
                                              │Yes
                                              ▼
                                ┌───────────────────────────────┐
                                │ Put in Design.md              │
                                │ (Supply: how the subject      │
                                │ currently meets demand)       │
                                └───────────────┬───────────────┘
                                                │No
                                                ▼
                      ┌─────────────────────────┴────────────────────────┐
                      │Q5: Is it about future work or change?            │
                      │(intent, options, decisions-to-make, priorities,  │
                      │tasks, roadmaps, sequencing, "what we plan to do")│
                      └─────────────────────────┬────────────────────────┘
                                                │Yes
                                                ▼
                              ┌──────────────────────────────────────┐
                              │ Put in work/Plan.md                 │
                              │ (Work: future intent; the plan at   │
                              │ this subject is where the work is   │
                              │ done)                               │
                              └───────────────────┬──────────────────┘
                                                  │No
                                                  ▼
                     ┌────────────────────────────┴──────────────────────────┐
                     │Q6: Does it primarily help explain or illustrate       │
                     │the subject, without itself being demand/supply/plan?  │
                     │(diagrams, UI mocks, data models, examples, references)│
                     └────────────────────────────┬──────────────────────────┘
                                                  │Yes
                                                  ▼
                                    ┌──────────────────────────────┐
                                    │ Put in Resources/            │
                                    │ (Collateral: supporting      │
                                    │ material the subject refers  │
                                    │ to, but is not itself truth) │
                                    └────────────────┬─────────────┘
                                                     │No
                                                     ▼
         ┌───────────────────────────────────────────┴────────────────────────────────┐
         │Q7: Does it actually describe something that deserves its OWN subject?       │
         │(a distinct area with its own demands, supply, and work: a department,      │
         │product, service, subsystem, team, or module)                               │
         └───────────────────────────────┬────────────────────────────────────────────┘
                                         │Yes
                                         ▼
                         ┌────────────────────────────────────────────┐
                         │ Create a new Component under Components/   │
                         │ and give THAT new subject its own:         │
                         │   Requirements.md, Design.md, work/Plan.md │
                         └───────────────────────────────┬────────────┘
                                                         │No
                                                         ▼
                         ┌────────────────────────────────────────────────┐
                         │ OFF-RAMP: This content likely belongs in code, │
                         │ tooling (e.g. Jira, Git), or an external/      │
                         │ legacy area, not inside the Fractal Specs      │
                         │ skeleton for this subject.                     │
                         └────────────────────────────────────────────────┘


# "How do I know what subjects to make?" / "how do I know when to split a folder?" decision tree
