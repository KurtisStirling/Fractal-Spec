# Meta Requirements and Design

## Requirements

- **What**: Keep meta guidance lightweight and token-efficient; capture only enduring rules that shape how project docs operate.  
  **Why**: Ensures LLM-friendly, low-bloat governance.

- **What**: Preserve “function over form”: the model defines what each file/folder does; teams may choose formats and even rename files if the function stays the same and is consistent within a subject.  
  **Why**: Avoids prescription while keeping discoverability.

- **What**: Core files are `Design.md` and `Requirements.md` (permanent truth) plus `Plan.md` and `Research.md` (temporary scaffolding). Each subject may optionally have `Supporting-Files/` for referenced collateral.  
  **Why**: Maintains the dual-truth split and a single place for durable collateral.

- **What**: `Supporting-Files/` holds distilled, referenced artefacts (org charts, diagrams, ERDs, specs, validation aids) tied to current Design; drafts and noise stay in `work/`.  
  **Why**: Keeps truth-bearing collateral discoverable and clean.

- **What**: Naming conventions: Title Case for core files; lowercase `work/`; Title Case `Supporting-Files/`; kebab-case is the sensible default for everything else, but any consistent convention per subject is acceptable.  
  **Why**: Speeds navigation and keeps contexts predictable for humans and LLMs.

- **What**: Multiple `Requirements.md` (and other core files) across subjects are expected; paths provide scope.  
  **Why**: Encourages recursion without naming collisions.

- **What**: Optional defaults (e.g., changelogs, YAML frontmatter, What/Why/Status/ Priority) may be offered as add-ons but are never mandated.  
  **Why**: Provides inspiration without enforcing form.

<details>
  <summary>Changelog (expand if needed)</summary>
  <ul>
    <li>2025-02-01: Initial meta requirements captured.</li>
    <li>2025-02-01: Added requirements for LLM bootloader, token-efficiency rationale, flexible syntax guidance, process usage rules, research scope, naming, and versioning.</li>
    <li>2025-02-??: Updated for function-over-form, core file set, Supporting-Files collateral, naming defaults, and optional add-ons.</li>
  </ul>
</details>

## Design

```yaml
---
created: 2025-02-01
last-updated: 2025-02-02
version: 0.2
used-by:
  - Microcosm-Fractal-Spec-Model
---
```

- Document anatomy remains RPI-fractal: `Design.md` and `Requirements.md` as permanent truth; `work/` with `Plan.md` and `Research.md` as temporary scaffolding; optional `Supporting-Files/` for durable referenced collateral.  
- Function over form: formats, statuses, and frontmatter are optional defaults; teams may rename core files if functions remain clear and consistent within a subject.  
- `Supporting-Files/` is the home for referenced, up-to-date artefacts (org charts, diagrams, ERDs, specs, validation aids); drafts stay in `work/`.  
- Naming conventions: Title Case for core files and `Supporting-Files/`; lowercase `work/`; kebab-case recommended for other files, but any consistent subject-level convention is acceptable.  
- Major design decisions should be captured in Design; Requirements remain distilled intent. Changelogs/frontmatter remain optional add-ons for teams that want traceability.

### Design Decisions

- **Function over form**: Only the roles of files/folders are mandated; expressions and names may vary if functions stay intact and consistent.  
- **Core files**: Permanent (Design, Requirements) and temporary (Plan, Research) are the anchor set for each subject.  
- **Collateral location**: `Supporting-Files/` is the default home for durable, referenced artefacts; drafts stay in `work/`.  
- **Naming defaults**: Title Case for core files, lowercase `work/`, Title Case `Supporting-Files/`; kebab-case recommended elsewhere.  
- **Scoped duplication**: Multiple `Requirements.md` instances are expected across subjects; paths provide disambiguation.

<details>
  <summary>Changelog (expand if needed)</summary>
  <ul>
    <li>2025-02-01: Initial meta design and decisions recorded.</li>
    <li>2025-02-02: Updated collateral naming, function-over-form stance, core file set, naming defaults, and scoped duplication guidance.</li>
  </ul>
</details>
