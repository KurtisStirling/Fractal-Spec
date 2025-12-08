# Fractal Specs / Design

- Subject anatomy: `Design.md` and `Requirements.md` as permanent truth; optional `work/` with `Plan.md` and `Research.md` as temporary scaffolding; optional `Supporting-Files/` for durable referenced collateral; optional child subjects (components/parts) as sibling folders using the same anatomy.
- Function over form: only the role of each file/folder is fixed. Teams may choose formats and even rename files if the function stays the same and is consistent within a subject.
- Core files (Title Case): `Design.md`, `Requirements.md` (permanent), `Plan.md`, `Research.md` (temporary), `Supporting-Files/` (collateral). `work/` stays lowercase to signal temporary. Other files default to kebab-case but any consistent convention per subject is acceptable. A noun plus qualifier works well (e.g., `auth-flow.md`, `billing-sequence.png`).
- Dual-truth: Requirements/Design are permanent; Plan/Research are temporary and should be promoted or archived after use. Done = implementation shipped and Design/Requirements updated.
- Planning: Plans live locally in each subject; no central backlog. Plan is where the work is done.
- Collateral: `Supporting-Files/` holds distilled, referenced artefacts (org charts, diagrams, ERDs, specs, validation aids) tied to Design. Drafts/noise live in `work/`.
- Child subjects (components/parts): Skeleton, Semantics, Files, Behaviour, User-Guide are defined as sibling folders here to illustrate recursion. An example RPI loop lives under `work/RPI/` to show temporary scaffolding. Plan/Research file guidance lives under `work/Plan-files` and `work/Research-files`.
- Navigation payoff: content types live in the same place at every level, reducing cognitive load for humans and AI.
- Payoff: it changes where you put things, not what you document—consistent navigation without heavyweight rules.

## Summary of Breakthroughs (agentic overlay)

* RPI generalisation — The Research → Plan → Implement loop is a universal, agent-friendly framing for change, not just coding. Each subject is a small RPI loop.  
* Dual-truth architecture — Requirements/Design are permanent truths (demand/supply now). Plan/Research are temporary scaffolding that expire when promoted.  
* Fractal structure — Every layer uses the same anatomy; subjects are microcosms and macrocosms simultaneously.  
* Draft → Promote workflow — Work is complete only when reality (code) and current truth (Design/Requirements) are updated to match.  
* Minimal semantics — Enforce the function of each file, never its format. Leave teams free to express content how they like.  
* LLM-friendly — Predictable, local context boundaries make AI collaboration safer and more reliable.

## Agentic RPI overlay & truth model

* Permanent truth — `Requirements.md` (demand) and `Design.md` (supply) are the authoritative, durable statements of intent and reality at this subject. Some very small subjects may carry only a Design if demand is self-evident.  
* Temporary truth — `work/Plan.md` and any `work/Research.md` are scaffolding that should be promoted or discarded. Plans are where the work is done, but they are not the record of truth.  
* RPI loop — Research (understand current reality and options) → Plan (decide intent and sequencing) → Implement (change the system) → Promote (update Design/Requirements; retire obsolete plan/research). Treat this as an agentic overlay: the subject itself is the boundary for local RPI cycles.  
* Done definition — A change is done when the implementation is shipped and Design/Requirements reflect the as-built system. Plans and research notes should be cleaned up or archived after promotion.  
* Research discipline — Keep research lightweight. When researching code, follow the stance from `stolen-commands-RPI/research_codebase.md`: document what exists (paths, flows, decisions) without critique; prefer direct evidence over speculation.

## Optional defaults / add-ons (format is free; function is fixed)

Fractal Specs mandates only what each file does, never how it is formatted. If you want ready-made patterns, these are opt-in “sensible defaults”:

* Requirements defaults (optional) — Capture demand however you like. A helpful pattern is `What / Why / Status / Priority`, with a compact HTML-wrapped changelog if you want traceability.  
* Design defaults (optional) — Stick to current truth. Optional helpers: a small YAML frontmatter (`created`, `last-updated`, `version`, `used-by`) and an HTML-wrapped changelog for drift tracking.  
* Planning defaults (optional) — Keep Plan.md as the single backlog/roadmap/task list at that subject; avoid parallel backlogs elsewhere.  
* Research defaults (optional) — Keep raw input and analysis in `work/Research.md` or scratch files; expire them after promotion.

## Work execution & optionality

* Mandatory core — Every subject should have a Design as the current truth; a Requirements file is strongly recommended for demand, but tiny technical substructures may rely on an implied demand and just carry a Design.  
* Optional scaffolding — `work/Plan`, `work/Research`, `Supporting-Files`, and child subjects are all optional; use them when they add clarity. If you do create them, keep Plans and Research temporary and promote or archive after use.  
* Execution boundary — The subject is the unit of work. Research and planning happen locally; implementation updates supply; promotion updates permanent truth.  
* Validation aids — Stable collateral (diagrams, ERDs, test run-sheets/tools) can live alongside the subject as an add-on folder; think of it as embedding rich context a Markdown file cannot hold.

## References

- `Skeleton/Design.md` — anatomy reference and decomposition.  
- `User-Guide/Design.md` — FAQ, audience guides, and decision trees.  
- `Supporting-Files/Positioning.md` — related work comparisons.
