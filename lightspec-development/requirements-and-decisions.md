---
created: 2025-12-02
last_updated: 2025-12-03
---

# Requirements and Decisions for Constitution Framework

## Requirements

### Origin

**Requested by:** Kurtis Papple
**Date:** 2025-12-02
**Context:** Need for a lightweight, comprehensive LLM workflow model that embeds spec and test-driven development principles. Multiple previous attempts in other repos became messy and confusing.

**Original request:** Create a universal framework (like the Scrum Guide) that provides immutable rules for how work is specified, tested, executed, and documented. Must work from personal projects to enterprise software.

### Primary Output

- Copy-pasteable folder/file structure to start new projects
- Primary file: `CONSTITUTION.md`
- Must contain YAML frontmatter: created date, version number, updated date, author (Kurtis Papple), project name
- First content line must read: "This Constitution defines the immutable rules, roles, and processes that govern how all work is specified, tested, executed, and documented."

### Framework Characteristics

#### Universal & Immutable
- Like the Scrum Guide: doesn't change per project
- Provides immutable rules that teams implement in their own way
- Projects can add extensions but cannot contradict the base framework

#### Scalable
- Works from personal projects through to enterprise software
- Base model is small but designed for all contexts and sizes
- "Start simple, scale when pain appears" philosophy

#### Comprehensive Yet Lightweight
- Not missing any obviously-needed parts
- Small base model
- No over-engineering

#### LLM-Optimized (KEY CHALLENGE)
- LLMs must understand the framework in minimal tokens
- This is the primary technical challenge
- Must be readable/understandable with minimal token usage

### Game Framing

Framework must answer:

1. **"What is the goal of the game?"**
   - Vision
   - Mission
   - Current objectives ("what's important now?")

2. **"What are the rules of the game?"**
   - Non-negotiable global rules
   - Law, standards, definition of done
   - UX principles, documentation rules
   - Project-specific rules

### Workflow Model

Must embed:
- Spec-driven development
- Test-driven development
- Spec → Test → Task → Code flow

### Structure Requirements

#### CONSTITUTION.md must have:
- Clear [IMMUTABLE] sections (framework that never changes)
- Clear [PROJECT-SPECIFIC] sections (where projects edit)
- Single file containing both framework and rules (not split across multiple files)
- Clear boundaries preventing accidental framework modification

#### Universal Rules:
- Default rules that ALWAYS apply to all projects
- Projects add their own rules on top

#### Supporting artifacts:
- Must include templates for specs, tests, patterns
- Clear folder structure
- File naming conventions

### Process Requirements

**Methodical approach required:**
- Planning and breaking down tasks
- Cannot rush ahead
- Cannot try to do too much at once
- Must not forget decisions
- Must not over-engineer
- Must consider holistic product and UX

### Business Rules

1. **Immutability Rule**: [IMMUTABLE] sections cannot be modified by projects
2. **Extension Rule**: Projects can only add rules in [PROJECT-SPECIFIC] sections, never contradict base rules
3. **Single Source Rule**: All rules must be in CONSTITUTION.md, not split across files
4. **Token Efficiency Rule**: Framework must prioritize minimal token usage for LLM comprehension
5. **Scalability Rule**: Framework must work at all scales without modification
6. **Completeness Rule**: Framework must not be missing obviously-needed parts
7. **Appropriate Prescriptiveness Rule**: Framework should not be overly prescriptive where flexibility is appropriate

### Acceptance Criteria

#### Framework Quality
- [ ] Framework is comprehensive (no obvious gaps)
- [ ] Framework is lightweight (minimal base size)
- [ ] Framework scales from personal to enterprise without changes
- [ ] Framework is optimized for LLM token efficiency

#### Structure Quality
- [ ] Clear [IMMUTABLE] and [CONTEXT-SPECIFIC] markers throughout
- [ ] Single CONSTITUTION.md file contains framework + rules
- [ ] YAML frontmatter includes all required fields
- [ ] First content line matches required text exactly
- [ ] Game framing structure present (goals + rules)

#### Usability Quality
- [ ] Copy-pasteable folder structure ready
- [ ] Clear instructions on what to edit vs not edit
- [ ] Supporting templates included
- [ ] File naming conventions documented
- [ ] Reading order for LLMs documented

#### Universal Applicability
- [ ] Works for personal projects (wedding planning, home automation)
- [ ] Works for solo dev projects
- [ ] Works for enterprise software
- [ ] No project-specific assumptions in [IMMUTABLE] sections

---

## Decisions

### D1: Single File with Marked Sections (2025-12-02)

**Problem:** Should the constitution be a pure "Scrum Guide" model (immutable, separate RULES.md) or an editable file?

**Options considered:**
1. **Pure "Scrum Guide" model**: CONSTITUTION.md (immutable) + PROJECT-RULES.md (editable)
   - Pro: Clean separation, clear immutability
   - Con: Rules split across 2 files, higher cognitive load, LLM must read both

2. **Living Constitution model**: CONSTITUTION.md contains everything, projects edit it
   - Pro: Single file, low cognitive load
   - Con: Each project has "modified" constitution, harder to update base framework

3. **Hybrid with marked sections**: CONSTITUTION.md with [IMMUTABLE] and [PROJECT-SPECIFIC] sections
   - Pro: Single file, clear boundaries, updateable base framework
   - Con: Requires discipline to only edit marked sections

**Decision:** Option 3 (Hybrid with marked sections)

**Rationale:**
- Single file = minimal cognitive load for both humans and LLMs
- Clear [IMMUTABLE]/[PROJECT-SPECIFIC] markers prevent accidental framework modification
- LLM-optimized: one file to read, clear structure
- Updateable: projects can merge updates to immutable sections when framework improves
- Rules in one place (not split)

**Authority:** Kurtis Papple

**Note:** This decision was reversed in D34 (V5) to pure Scrum Guide model with constitution/ folder.

---

### D2: "Constitution" Over "Workflow Model" (2025-12-02)

**Problem:** What should the primary document be called?

**Options considered:**
1. WORKFLOW-MODEL-[PROJECT].md
2. CONSTITUTION.md

**Decision:** CONSTITUTION.md

**Rationale:**
- "Constitution" better conveys immutability and authority
- Rules naturally belong in a constitution
- Stronger, clearer naming
- Aligns with "game framing" metaphor (constitutions define the rules of the game)

**Authority:** Kurtis Papple (after discussion with ChatGPT)

---

### D3: Rules Inside Constitution (2025-12-02)

**Problem:** Where should rules live - separate RULES.md or inside CONSTITUTION.md?

**Context:** Previous WORKFLOW-MODEL-TEMPLATE.md had separate RULES.md file for visibility and easy reference.

**Decision:** Rules live inside CONSTITUTION.md in a dedicated Rules section

**Rationale:**
- Single file reduces cognitive load
- Rules ARE the point of a constitution (conceptually belong together)
- Avoids "rules in 2 places" problem
- Still maintain clear structure with Universal Rules + Project Rules subsections
- LLM token efficiency: read one file instead of two

**Trade-off accepted:** Slightly longer single file vs. better conceptual coherence

**Authority:** Kurtis Papple

**Note:** This decision was reversed in D33 based on scalability needs.

---

### D4: Game Framing Structure (2025-12-02)

**Problem:** How should the framework be conceptually organized?

**Decision:** Use "game framing" metaphor with Goals + Rules

**Structure:**
- "What is the goal of the game?" → Vision, Mission, Current Objectives
- "What are the rules of the game?" → Universal Rules + Project Rules
- Then move to actual work (Specs, Tasks, Tests)

**Rationale:**
- Intuitive mental model
- Separates stable context (goals, rules) from dynamic work (specs, tasks)
- Aligns with product management best practices (always know the "why")
- Helps LLMs and humans understand context before execution

**Authority:** Kurtis Papple (based on 8+ years product management experience)

---

### D5: Token Optimization as Primary Challenge (2025-12-02)

**Problem:** What is the key technical challenge for this framework?

**Decision:** LLM token efficiency is THE primary challenge

**Implications:**
- Every section must be optimized for minimal tokens while maintaining clarity
- Reading order must be explicitly documented
- "Agent Quickstart" section for sub-250 token context
- Default read budget: ≤300 tokens unless task demands more
- Structure information hierarchy for LLM comprehension

**Rationale:**
- LLMs have zero long-term memory (re-reading costs tokens every time)
- Limited short-term memory (token windows)
- Framework must enable "read as little as possible, to know as much as possible, about what matters now"

**Authority:** Kurtis Papple (explicitly stated as "VERY difficult task" and "key challenge")

---

### D6: Scalability Philosophy (2025-12-02)

**Problem:** How should the framework handle different project sizes?

**Decision:** "Start simple, scale when pain appears"

**Approach:**
- Base model works from personal projects to enterprise
- No features added until they're needed
- Framework provides guidance on when/how to scale
- No project-size assumptions in immutable sections

**Examples:**
- Personal project (wedding planning): uses only what's needed
- Solo dev: minimal overhead
- Enterprise: extensible to teams, compliance

**Rationale:**
- Avoid over-engineering
- Reduce barrier to entry
- Let real-world pain drive evolution
- Most small-to-medium projects work fine with markdown files

**Authority:** Kurtis Papple + inherited from WORKFLOW-MODEL-TEMPLATE.md

---

### D7: Spec-Driven and Test-Driven Development (2025-12-02)

**Problem:** What development methodology should the framework enforce?

**Decision:** Mandatory Spec → Test → Task → Code flow

**Rules:**
- Work begins with a spec
- Before implementation, every spec must produce at least one test
- Tasks are derived from tests/specs
- No implementation without tests
- Code must pass referenced tests

**Rationale:**
- Specifications preserve intent (code alone doesn't)
- "Lossless" documentation enables rebuilding and understanding
- Traceability: know where requirements came from, why they changed
- LLM-friendly: specs provide context across sessions
- Prevents "vibe coding" (chatting with AI with no structure)

**Authority:** Kurtis Papple (based on PM/BA experience, addressing gaps in current spec-driven development approaches)

---

### D8: Requirements Changelog for Traceability (2025-12-02)

**Problem:** How to track the evolution of requirements?

**Decision:** Domain specs must include Requirements Changelog section

**Tracks:**
- What was originally requested vs. what was agreed
- Why requirements changed
- Decision trail and negotiations
- Related rules/specs affected

**Does NOT track:**
- Typo fixes
- Rewording
- Formatting changes
- Minor clarifications

**Rationale:**
- Answers "where did this even come from?"
- Preserves "who asked for it, when did requirements change?"
- Addresses missing pieces in current spec-driven development
- Enables future developers/LLMs to understand decisions

**Authority:** Kurtis Papple (identified as missing piece in spec-driven development based on 8+ years PM/BA experience)

---

### D9: Root-Level Framework Files (2025-12-02)

**Problem:** Should framework files (CONSTITUTION.md, specs/, tasks/, etc.) be in docs/ or at root level?

**Options considered:**
1. **In docs/ folder**: Keeps root clean for product code
   - Pro: Clean root directory
   - Con: Framework feels like "just documentation" rather than operating system

2. **At root level**: Framework files are first-class citizens
   - Pro: Visibility = importance, LLM reads root first
   - Con: More items at root level

**Decision:** Root level

**Rationale:**
- This isn't just documentation - it's the OPERATING SYSTEM for the project
- Constitution, specs, tasks are not "docs about the product" - they ARE the product development system
- Root-level visibility = importance (harder to ignore)
- LLM reads root first - want these visible and prominent
- Still clean (only 4 framework folders: CONSTITUTION.md, specs/, technical/, tasks/)

**Authority:** Kurtis Papple

---

### D68: Public Version Reset to 1 and Single Reference (2025-12-04)

**Problem:** Internal iteration reached `version-7/`, but the first public release should start at version 1. Version strings appeared in multiple docs, causing confusion and token waste.

**Options considered:**
1. Keep visible v7.x branding in output and docs.
2. Show both internal iteration (v7) and public version (v1) across documents.
3. Reset public version to 1 and state it only once in `constitution/CONSTITUTION.md` frontmatter; treat internal folder numbering as development-only.

**Decision:** Option 3 — Public version = 1, recorded only in Constitution frontmatter; remove other version strings from the output.

**Rationale:** Single source of truth, less confusion, fewer tokens, clear split between internal iteration history and the first public release.

**Authority:** Kurtis Papple

### D10: "technical/" Over "implementation/" (2025-12-02)

**Problem:** Should the folder be called "technical/" or "implementation/"?

**Options considered:**
1. **implementation/**: More accurate, clearer intent
2. **technical/**: Industry standard, broader term

**Decision:** technical/

**Rationale:**
- More extensible (can include patterns, architecture, decisions, APIs - not all are "implementation")
- Industry familiarity (common in OSS projects)
- Future-proof for expansion
- `technical/patterns/` is clear enough to understand purpose

**Authority:** Discussed with Kurtis Papple

---

### D11: Folder Structure for Output (2025-12-02)

**Problem:** How to organize this repo to separate framework development from framework output?

**Decision:** Three-folder structure:
- `output/` - Copy-pasteable framework that users take to their projects
- `input-consumed/` - Reference documents already analyzed
- `input-to-consume/` - Reference documents to be analyzed
- `requirements-and-decisions.md` at root - Meta documentation for framework development

**Final output structure:**
```
output/
  CONSTITUTION.md
  specs/
    domain/
      DOMAIN-SPEC-TEMPLATE.md
    tests/
      TEST-SPEC-TEMPLATE.md
  technical/
    patterns/
      PATTERN-TEMPLATE.md
  tasks/
    inbox/
    plans/
    done/
    backlog.md
  README.md
```

**Rationale:**
- Clear separation between "developing the framework" vs "the framework itself"
- "output" is clearer than "template" for what gets copied
- Input folders help track what's been analyzed vs what needs analysis
- Clean, organized approach to framework development

**Authority:** Kurtis Papple

---

### D12: Rules Scope - Global Only (2025-12-02)

**Problem:** Should rules have a `scope:` field for filtering (api, ui, database, etc.)?

**Options considered:**
1. Add `scope:` field like RULES-TEMPLATE.md suggests (api, ui, global, etc.)
2. Keep rules global-only, document local rules in specs

**Decision:** Rules are always global. No scope field.

**Rationale:**
- Rules in Constitution are non-negotiable, cross-cutting requirements
- Local/feature-specific rules belong in domain specs, not Constitution
- Simpler model: Constitution = global rules, Specs = local rules
- Avoids token overhead of scope filtering

**Authority:** Kurtis Papple

---

### D13: SDD Philosophy Integration (2025-12-02)

**Problem:** How much Spec-Driven Development philosophy should be in Constitution?

**Options considered:**
1. Full integration - make SDD mandatory, position as "for AI code generation"
2. Light touch - acknowledge SDD, don't mandate it
3. Modular add-on - separate SDD-GUIDE.md

**Decision:** Light touch (Option 2)

**Rationale:**
- Token optimization already SDD-friendly (wake up with context, execute efficiently)
- Keep framework universal - works with or without AI code generation
- Acknowledge SDD as strong use case without mandating implementation details
- Users doing traditional dev can still benefit from spec → test → code flow

**Authority:** Kurtis Papple

---

### D14: Token Budget vs Comprehensiveness (2025-12-02)

**Problem:** Input files contain valuable content, but implementing all of it creates a document that "burns half your token budget every new conversation."

**Decision:** Ruthlessly optimize for token ROI

**Principles:**
1. **Minimal but comprehensive** - Sensible foundation, not one-size-fits-all behemoth
2. **Positive ROI required** - Every section must justify its token cost
3. **Trust users** - They can extend the framework. Don't over-explain.
4. **Avoid excessive [OPTIONAL] markers** - Users capable of adding their own sections
5. **No "explain like you're 5"** - Assume competent audience

**Implementation:**
- ROI analysis for every proposed section
- Ruthlessly prioritize essential vs nice-to-have
- Prefer terse examples over verbose explanations
- Measure actual token usage of Constitution + templates

**Rationale:**
- Token efficiency is THE primary challenge (D5)
- Previous work (input files) shows risk of over-documentation
- Framework is a foundation, not comprehensive guide to everything
- LLMs re-read context every session - token cost compounds

**Authority:** Kurtis Papple

---

### D15: LLM Working Principles in Constitution (2025-12-02)

**Problem:** Where should LLM working principles (verify before assuming, clarify unclear requirements, one-step-at-a-time) be documented?

**Options considered:**
1. New section in Constitution (~100 tokens)
2. Separate WORKING-WITH-LLMS.md guide
3. README only

**Decision:** Brief section in Constitution (Option 1)

**Rationale:**
- These principles are critical to framework success
- "Verify before assuming" and "Clarify unclear requirements" prevent costly mistakes
- LLMs need to see these principles to follow them
- Keep brief (~100 tokens max) to respect token budget
- Focus on essential principles only: verify, clarify, explain why, challenge assumptions

**Authority:** Kurtis Papple

---

### D16: V3 Holistic Refactoring (2025-12-02)

**Problem:** V2 has accumulated unnecessary sections and explanations that burn tokens without sufficient value.

**Decision:** Ruthless simplification for V3

**Actions:**
1. Remove Scaling Guide (replaced with 2-3 sentences + reference to "don't prematurely optimize")
2. Remove Common Pitfalls (move legitimate concerns inline where relevant)
3. Remove token goal statement (just be efficient, don't explain efficiency)
4. Simplify frontmatter from 12 fields to essential only
5. Resolve redundancy between File Structure tree and Naming Conventions
6. Refactor Workflow section for clarity
7. Unify rules format (no distinction between Universal and Project rules format)
8. Move Definition of Done into Rules section (they ARE rules)

**Rationale:**
- "If framework designed well, pitfalls wouldn't exist"
- "We DO NOT explain to others like they're 5 how to scale"
- "Just make it efficient, don't explain efficiency"
- Every section must earn its token cost

**Authority:** Kurtis Papple

---

### D17: Spec-Driven and Test-Driven Development Are Immutable (2025-12-02)

**Problem:** V2 language suggested SDD/TDD were optional or complementary to framework.

**Decision:** SDD and TDD are PART of the immutable foundation, not optional.

**Rationale:**
- Spec → Test → Task → Code is in [IMMUTABLE] Workflow section
- Cannot say "works equally well with traditional workflows" when workflow is immutable
- Framework IS spec-driven and test-driven by design

**Authority:** Kurtis Papple

---

### D18: Global Rules Only in Constitution (2025-12-02)

**Problem:** V2 had complex criteria for "what qualifies as a rule" with multiple conditions.

**Decision:** Simple truth - A rule goes in Constitution if it's a global rule. That's it.

**Clarification:**
- Global rules include: definition of done, accessibility standards, legal rules, regulations, company rules, technology rules, any non-negotiable global requirement
- Local/feature-specific rules belong in domain specs
- No complex qualification criteria needed

**Rationale:**
- Simpler model is clearer
- Distinction is obvious: global vs local
- Reduces cognitive load and token cost

**Authority:** Kurtis Papple

---

### D19: Remove Roles Section (2025-12-02)

**Problem:** Does the Roles section (Creator/Resolver) add sufficient value to justify its token cost?

**Options considered:**
1. Keep as-is (~50 tokens)
2. Compress into LLM Working Principles (~15 tokens)
3. Remove entirely (saves 50 tokens)

**Decision:** Remove entirely (Option 3)

**Rationale:**
- When working with LLMs, the Creator/Resolver distinction is self-evident
- Workflow already defines work structure without needing role labels
- 50-token cost doesn't justify value added
- Teams needing role clarity can add in [CONTEXT-SPECIFIC] sections

**Authority:** Kurtis Papple (approved recommendations from analysis)

---

### D20: Simple Numeric ID Strategy (2025-12-02)

**Problem:** Should we keep PREFIX-based IDs (USER1, ADMN1) or simplify?

**Options considered:**
1. No IDs at all (maximum simplicity, loses stable references)
2. Simple numeric ID in frontmatter only (recommended)
3. Keep current PREFIX{N} system in filename and frontmatter
4. Prefix in frontmatter only, descriptive filenames

**Decision:** Simple numeric ID in frontmatter only (Option 2)

**Rationale:**
- Saves ~80 tokens vs PREFIX system (no naming table, no prefix mapping, simpler frontmatter)
- Provides stable references even if files renamed
- Self-documenting filenames (`user-login.md` clearer than `USER1-login.md`)
- Can still reference "spec #42" in tasks/code
- Users can add folder structure for topic grouping if needed

**Implementation:**
- Frontmatter: `id: 42`
- Filename: `{descriptive-name}.md`
- Reference: "Implements #42"

**Authority:** Kurtis Papple (approved recommendations from analysis)

---

### D21: Remove Topic Mapping (2025-12-02)

**Problem:** Is Topic Mapping table needed?

**Decision:** Remove entirely

**Rationale:**
- Not needed with simple numeric IDs (D20)
- Saves 40 tokens
- Users can use folder structure for topic organization
- Reduces maintenance burden

**Authority:** Kurtis Papple (approved recommendations from analysis)

---

### D22: Artifact Definitions as Hybrid Table (2025-12-02)

**Problem:** Where should artifact definitions live - Constitution details, templates only, or hybrid?

**Options considered:**
1. Keep detailed descriptions in Constitution (~100+ tokens)
2. Constitution just lists artifacts (~20 tokens)
3. Hybrid table showing artifact + purpose + template (~30 tokens)
4. Remove from Constitution entirely

**Decision:** Hybrid table (Option 3)

**Rationale:**
- ~30 tokens prevents LLM creating wrong artifact types
- Constitution states CONCEPTUALLY what exists (not HOW to fill them)
- Details live in templates (single source of truth)
- Positive token ROI

**Authority:** Kurtis Papple (approved recommendations from analysis)

---

### D23: [CONTEXT-SPECIFIC] Naming (2025-12-02)

**Problem:** What to call non-universal customizable sections?

**Options considered:**
- [PROJECT-SPECIFIC] (current)
- [CUSTOMIZABLE]
- [PROJECT-CONFIG]
- [PROJECT-DEFINED]
- [LOCAL-CONFIG]
- [CONTEXT-SPECIFIC] (Kurtis suggestion)

**Decision:** [CONTEXT-SPECIFIC]

**Rationale:**
- More accurate - varies by context (project/product/business/repo)
- Clearer intent than "project" (which implies software project only)
- Better semantic fit across all use cases

**Authority:** Kurtis Papple

**Note:** This marker was removed in V5 in favor of HTML comment markers and pure Scrum Guide model.

---

### D24: Simplify Frontmatter to 6 Fields (2025-12-02)

**Problem:** V2 had 12 mandatory frontmatter fields, but started with only 4. Is this lightweight?

**Original 4 fields:**
- doc_type (or type)
- version
- created
- last_updated

**Decision:** Reduce to 6 essential fields

**Final schema:**
```yaml
id: 1
type: domain|test|pattern
version: 1
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
status: draft|approved|implemented|retired
```

**Rationale:**
- Removed: doc_type (redundant with type), spec_type (redundant), title (filename is title), domain (folder structure or filename provides this), implemented_date (optional fields bloat schema), depends_on (can be in body if needed), related (can be in body if needed)
- Kept essentials: id (stable reference), type (artifact classification), version (change tracking), created/last_updated (temporal context), status (lifecycle tracking)
- Still comprehensive but much more token-efficient

**Authority:** Kurtis Papple (approved recommendations from analysis)

---

### D25: V3 Holistic Refactoring Complete (2025-12-02)

**Problem:** V2 accumulated unnecessary sections burning tokens without sufficient ROI

**Actions taken:**
1. ✓ Removed Roles section (saves ~50 tokens)
2. ✓ Removed Naming Conventions table (saves ~60 tokens, kept one-line guidance)
3. ✓ Removed Topic Mapping section (saves ~40 tokens)
4. ✓ Removed Common Pitfalls section (saves ~100 tokens)
5. ✓ Removed token goal statement (saves ~10 tokens)
6. ✓ Replaced Scaling Guide with 3 sentences (saves ~100 tokens)
7. ✓ Refactored Artifact Definitions to hybrid table (saves ~70 tokens)
8. ✓ Removed Requirements Changelog details (saves ~60 tokens, kept concept)
9. ✓ Simplified Frontmatter from 12 to 6 fields (saves ~40 tokens)
10. ✓ Removed "Specs are lossless" from Core Principles (rationale, not principle)
11. ✓ Clarified SDD/TDD as immutable foundations (not optional)
12. ✓ Refactored Workflow section (clearer, more concise)
13. ✓ Unified rules format (no YAML vs markdown distinction)
14. ✓ Renamed "Rules" to "Global Rules" with clearer explanation
15. ✓ Moved Definition of Done into Rules as RULE-6
16. ✓ Replaced [PROJECT-SPECIFIC] with [CONTEXT-SPECIFIC] throughout

**Total estimated token savings: ~530+ tokens**

**Result:** V3 is significantly more token-efficient while maintaining all essential functionality

**Authority:** Kurtis Papple

---

### D26: Four Core Components Structure (2025-12-02)

**Problem:** Goals and Global Rules were not prominent enough in V3 structure. Hierarchy didn't reflect importance.

**Decision:** Reorganize into 4 CLEAR core components with prominent naming

**Structure:**
```
## Core Components
  GOALS //
  GLOBAL RULES //
  SPECIFICATIONS //
  ROADMAP //
```

**Rationale:**
- GOALS and GLOBAL RULES answer "what game are we playing?"
- SPECIFICATIONS are the "blueprints" (what to build and why)
- ROADMAP is hybrid backlog/roadmap (execution tracker)
- // suffix creates visual consistency and signals importance
- All caps makes components unmissable
- Game analogy positioned as rationale within Goals section (not structure)

**Authority:** Kurtis Papple

---

### D27: Terse Component Descriptions (2025-12-02)

**Problem:** Components needed brief, clear descriptions without over-explanation

**Decision:** Use terse (brief, concise) descriptions for each component

**SPECIFICATIONS:**
"Specifications capture WHAT needs to be built and WHY, preserving intent that code alone cannot. They enable anyone (human or LLM) to understand requirements without reverse-engineering implementation."

**ROADMAP:**
"The roadmap is a hybrid backlog and roadmap—tracking what work exists, what's prioritized now, and what's coming next. It bridges high-level objectives to concrete tasks."

**Rationale:**
- Token efficiency (core principle #3)
- Matches terse style used elsewhere in framework
- Provides just enough context without over-explaining

**Authority:** Kurtis Papple (approved recommendations)

---

### D28: tasks/ → task-mgmt/ Folder Rename (2025-12-02)

**Problem:** Folder name "tasks/" didn't reflect hybrid backlog/roadmap nature

**Decision:** Rename to task-mgmt/ (task management)

**Rationale:**
- "task-mgmt" better describes purpose (managing work, not just tasks)
- Accommodates roadmap, backlog, planning, and archival functions
- Clearer than generic "tasks" folder

**Authority:** Kurtis Papple

**Note:** This decision was updated in D34 (V5) to use "roadmap/" for consistency with folder/file naming convention.

---

### D29: ROADMAP-TEMPLATE.md Created (2025-12-02)

**Problem:** Need template to capture implementation detail for hybrid backlog/roadmap

**Decision:** Create ROADMAP-TEMPLATE.md with Now/Next/Later structure

**Contents:**
- Now/Next/Later explanation
- Task format specification
- How to move tasks between sections
- Inbox processing workflow
- When to create plans

**Rationale:**
- Templates provide consistent structure
- Documents best practices for roadmap maintenance
- Explains relationship between roadmap, inbox, and plans

**Authority:** Kurtis Papple

**Note:** This was revised in D32 to make ROADMAP.md a living document instead of a template.

---

### D30: Simplified Rules Format (2025-12-02)

**Problem:** V3 rules format was verbose with separate "Rule:" label

**Decision:** Make rule clause bold and primary, supporting fields indented

**Format:**
```
RULE-N: **[Rule clause as bold statement]**
- Rationale: [Why this is required]
- Authority: [Who/what mandates this]
- Date Added: YYYY-MM-DD
```

**Rationale:**
- Rule clause is most important, should be immediately visible
- Reduces redundancy
- More scannable for LLMs

**Authority:** Kurtis Papple

**Note:** This format was simplified further in V5 to use R-N notation instead of RULE-N.

---

### D31: Version Field in All Templates (2025-12-02)

**Problem:** Templates need version field for consistency with Constitution frontmatter spec

**Decision:** All templates must include version field in frontmatter

**Standard frontmatter (specs and patterns):**
```yaml
---
id: 1
type: domain|test|pattern
version: 1
status: draft|approved|implemented|retired
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
---
```

**ROADMAP frontmatter:**
```yaml
---
type: roadmap
version: 1
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
---
```

**Rationale:**
- Consistency across all framework artifacts
- Enables tracking document evolution
- Aligns with versioning principle (RULE-2)

**Authority:** Kurtis Papple

---

### D32: ROADMAP.md as Living Document, Not Template (2025-12-02)

**Problem:** Should ROADMAP be a template (like specs/patterns) or a living document that users edit directly?

**Options considered:**
1. **ROADMAP-TEMPLATE.md** - Users copy template, create new roadmap files
   - Pro: Consistent with other templates
   - Con: Users never create multiple roadmaps - it's a single living document

2. **ROADMAP.md** - Users copy as-is and edit the [CONTEXT-SPECIFIC] sections
   - Pro: Matches actual usage (single file, not multiple instances)
   - Pro: Parallel with GLOBAL-RULES.md (also living document)
   - Con: Slightly different pattern from spec templates

**Decision:** ROADMAP.md as living document (Option 2)

**Rationale:**
- ROADMAP.md is a single living document, not a "create copies from template" artifact
- Users edit sections (Now/Next/Later), don't create new roadmaps
- Parallel with GLOBAL-RULES.md design (both living documents with usage guides in appendix)
- Usage guide in appendix (read only when needed) follows same pattern as GLOBAL-RULES
- More intuitive: copy framework, immediately have working ROADMAP.md to populate
- Avoids confusion of "why would I create a second roadmap?"

**Implementation:**
- Created task-mgmt/ROADMAP.md with Now/Next/Later sections
- Usage guide moved to Appendix section
- Removed ROADMAP-TEMPLATE.md
- Updated Constitution templates table to show "Template/Location" column
- Added note: "ROADMAP.md and GLOBAL-RULES.md are living documents (not templates)"

**Authority:** Kurtis Papple

---

### D33: Separate GLOBAL-RULES.md File (2025-12-02)

**Problem:** Should rules live inline in CONSTITUTION.md (D3) or in separate GLOBAL-RULES.md?

**Context:** D3 originally decided rules inside Constitution for single-file simplicity. However, rules can grow large with context-specific additions.

**Options considered:**
1. **Keep rules inline** (maintain D3)
   - Pro: Single file for all framework content
   - Con: V3 had 6 rules inline; if rules grow to 20+, that's 1,000+ tokens in Constitution

2. **Separate GLOBAL-RULES.md** for all rules (Universal + Context-Specific)
   - Pro: Scalability - rules can grow without bloating Constitution
   - Pro: Parallel with ROADMAP.md (both living documents)
   - Pro: Token efficiency - LLMs read rules file only (200 tokens vs 1,500+ with inline)
   - Con: Two files instead of one

3. **Hybrid** - Universal in Constitution, Context-Specific in separate file
   - Pro: Framework rules visible in Constitution
   - Con: Rules split across two locations (higher cognitive load)

**Decision:** Separate GLOBAL-RULES.md (Option 2)

**Rationale:**
- Scalability: Context-specific rules could grow to 20+ in enterprise projects
- Token efficiency: Constitution drops from 1,650 to 1,150 tokens
- Clean separation: Constitution = framework structure, GLOBAL-RULES = requirements
- Rules as compact list (~200 tokens) with appendix for context (~300 tokens, rarely read)
- All rules in one place (not split between Constitution and separate file)
- Explicit LLM workflow: "Read GLOBAL-RULES.md every session"

**This reverses D3** based on real-world token analysis and scalability needs.

**Authority:** Kurtis Papple

---

### D34: V5 Constitution Folder Structure (2025-12-03)

**Problem:** V4 still had [CONTEXT-SPECIFIC] markers in CONSTITUTION.md. Should V5 adopt pure "Scrum Guide" model?

**Decision:** Yes - create constitution/ folder with fully separated concerns

**Structure:**
```
constitution/
  CONSTITUTION.md    # 100% immutable
  GOALS.md           # 100% user-editable (soft template)
  GLOBAL-RULES.md    # Universal (immutable) + Context-Specific (editable)
```

**Rationale:**
- Pure Scrum Guide model - framework never changes per project
- Remove all [CONTEXT-SPECIFIC] markers from CONSTITUTION.md
- Clearer mental model: constitution/ = "the rules of the game"
- Simpler user instructions: "Edit GOALS.md and add rules to GLOBAL-RULES.md"
- Token savings: ~80 tokens (no marker explanations)
- Folder/file name duplication normal in software (src/src.rs, react/react.js)

**This completes the evolution from D1 → D33 → D34**

**Authority:** Kurtis Papple

---

### D35: Immutability Markers as HTML Comments (2025-12-03)

**Problem:** How to clearly mark what's editable vs immutable across all framework files?

**Options considered:**
1. HTML comment markers only
2. Frontmatter + HTML comments
3. Explicit section dividers
4. HTML-style tags `<IMMUTABLE>`

**Decision:** HTML comment markers (Option 1)

**Format:**
```markdown
<!-- [IMMUTABLE] DO NOT EDIT -->
Framework content
<!-- [EDITABLE] CUSTOMIZE BELOW -->
User content
```

**Rationale:**
- Clear for humans editing (visible in source)
- Hidden when rendered (clean display in Obsidian/GitHub)
- Standard practice (HTML comments universally supported)
- Paired markers create clear boundaries
- Short and efficient (~70 chars total)
- No frontmatter needed (markers don't change)

**Usage:**
- constitution/CONSTITUTION.md: [IMMUTABLE] at top only (100% immutable)
- constitution/GLOBAL-RULES.md: [IMMUTABLE] at top, [EDITABLE] before Context-Specific Rules, [IMMUTABLE] for Appendix
- .claude/CLAUDE.md: [IMMUTABLE] at top, [EDITABLE] before Project-Specific Context
- constitution/GOALS.md: No markers (100% soft template)
- Templates: No markers (R4 enforces structure)

**Authority:** Kurtis Papple

---

### D36: Templates in Directories (Not Centralized) (2025-12-03)

**Problem:** Should templates live in their usage directories or in a centralized templates/ folder?

**Options considered:**
1. **Templates in directories** - Template lives where it's used
2. **Centralized templates/ folder** - All templates in one place

**Decision:** Templates in directories (Option 1)

**Rationale:**
- Supports "discoverable structure" principle (find template where you need it)
- Recognition over recall (see template in directory, use it)
- Just-in-time instruction (template + README together)
- Token efficiency (LLM reads directory once, gets template + examples)
- Self-contained directories
- Only 3 templates (not enough to justify centralization)

**Authority:** Kurtis Papple

---

### D37: Template Guidance in README Files (2025-12-03)

**Problem:** Template appendices get duplicated in every spec instance. How to avoid this?

**Decision:** Remove appendices from templates, create README.md in each directory

**Structure:**
```
specs/domain/
  README.md                # How to use domain specs + template
  DOMAIN-SPEC-TEMPLATE.md  # Clean template (no appendix)
  user-login.md            # Instance (no guidance)
```

**Rationale:**
- Zero duplication (guidance in one place)
- Token-efficient (LLM reads README once, not per-spec)
- Cleaner specs (just content, no meta-documentation)
- Standard practice (READMEs explain directories)
- Just-in-time instruction (read when in directory)

**Applied to:**
- specs/domain/README.md
- specs/tests/README.md
- technical/patterns/README.md

**Authority:** Kurtis Papple

---

### D38: Test Specs Optional with Guidance in README (2025-12-03)

**Problem:** Are test specs always needed, or only for certain outputs?

**Decision:** Test specs primarily for code; guidance in specs/tests/README.md

**R3 remains:** "No implementation without corresponding test specifications."

**Constitution Workflow section:**
```
Domain Spec → Test Spec → Tasks → Implementation

Test specs define verification steps, required primarily for coding. For simple
outputs, acceptance criteria in domain specs can suffice (see specs/tests/README.md
for guidance).
```

**README.md explains:**
- Always for code (unit tests, test cases)
- Optional for simple deliverables (AC might be sufficient)
- Useful for complex deliverables (verification checklists)

**Rationale:**
- Keeps Constitution sharp (doesn't over-explain)
- Honors "discoverable, just-in-time" principle
- Guidance where it's needed (when creating test specs)
- Maintains R3 as strong rule
- LLM/user judgment determines when test spec needed

**Authority:** Kurtis Papple

---

### D39: Core Principles Reprioritized (2025-12-03)

**Problem:** Core Principles in V4 weren't prioritized by importance and included table-stakes items

**Decision:** Rewrite based on Framework Characteristics, split into Principles + Characteristics

**Core Principles (what matters most):**
1. Token-optimized for LLMs
2. Self-guiding structure (discoverable, just-in-time, recognition over recall)
3. Everything documented
4. Traceability

**Framework Characteristics (how it works):**
- Universal: Works personal → enterprise
- Scalable: Start simple, scale when pain
- Comprehensive: No gaps, no over-engineering
- Immutable: Base framework never changes

**Rationale:**
- Removed "Single source of truth" (table stakes, not distinctive)
- Prioritized by importance (token optimization = PRIMARY challenge)
- Self-guiding principle captures discoverable/JIT/recognition concepts
- Characteristics describe the framework, principles describe values

**Authority:** Kurtis Papple

---

### D40: Framework Renamed to TGSA (2025-12-03)

**Problem:** "Constitution Framework" is generic. Need distinctive, memorable name.

**Decision:** TGSA Framework v5.0

**TGSA:**
- **T**oken-efficient
- **G**ame-framed
- **S**pec-driven
- **A**gentic-workflow

**Rationale:**
- Captures all four key characteristics
- Memorable acronym
- Positions framework clearly (for LLM-driven development)
- "Agentic" signals AI/LLM optimization

**Authority:** Kurtis Papple

---

### D41: task-mgmt/ → roadmap/ Folder Rename (2025-12-03)

**Problem:** Folder naming inconsistent with constitution/CONSTITUTION.md pattern

**Decision:** Rename task-mgmt/ to roadmap/

**Rationale:**
- Matches naming convention: constitution/CONSTITUTION.md, roadmap/ROADMAP.md
- Clearer (folder contains ROADMAP.md as primary file)
- Simpler mental model
- Consistency across framework

**This updates D28**

**Authority:** Kurtis Papple

---

### D42: How TGSA Handles Requirements (2025-12-03)

**Problem:** Users familiar with traditional requirements docs need to understand TGSA approach

**Decision:** Add "How TGSA Handles Requirements" section to Constitution

**Explanation:**
- **Global requirements** (cross-cutting, non-negotiable) → GLOBAL-RULES.md
- **Feature-specific requirements** (must-have, should-have, nice-to-have) → Domain specs
- Traditional "requirements doc" replaced by these two mechanisms

**Rationale:**
- Answers "where did the requirements doc go?"
- Clarifies distinction between global vs local requirements
- Positions domain specs as requirement containers (not just feature descriptions)
- Token-efficient (~60 tokens)

**Authority:** Kurtis Papple

---

### D43: ROADMAP vs LLM Task Lists Distinction (2025-12-03)

**Problem:** Users and LLMs might confuse ROADMAP.md with ephemeral LLM task tracking

**Decision:** Document the distinction in Constitution

**ROADMAP.md:**
- Persistent backlog across sessions
- All work (past/present/future)
- Strategic planning + history
- Read when planning what to work on next

**LLM task lists:**
- Ephemeral (this session only)
- Current task breakdown
- Tactical execution tracking
- Lives in conversation memory, not files

**Rationale:**
- Clarifies they serve different purposes (not redundant)
- Helps LLMs understand when to use each
- Prevents confusion about "where should I track tasks?"
- Token-efficient (~80 tokens)

**Authority:** Kurtis Papple

---

### D44: All Projects Produce Output Philosophy (2025-12-03)

**Problem:** Framework needs to explain why specs/structure matter even for simple projects

**Decision:** Add "All Projects Produce Output" section to Constitution opening

**Content:**
```
Every project produces deliverable output: code, systems, documents, plans, or reports.
Define your output in constitution/GOALS.md before starting work.

Work begins with domain specifications describing what to build and why. Simple projects
might have one domain spec, complex projects have many—including test specs and technical
patterns. The framework scales from personal projects to enterprise software.
```

**Rationale:**
- Sets mindset: all work produces something concrete
- Explains why methodical approach matters
- Addresses "is this overkill for small projects?" concern
- Shows natural scaling (1 spec → many specs)
- Token-efficient (~70 tokens)

**Authority:** Kurtis Papple

---

### D45: .claude/ Directory for LLM Context (2025-12-03)

**Problem:** Where should CLAUDE.md live in the framework structure?

**Decision:** Create .claude/ directory at root

**Structure:**
```
.claude/
  CLAUDE.md    # LLM bootloader and project context
```

**Rationale:**
- Standard practice (similar to .github/, .vscode/)
- Keeps LLM-related config together
- Clear signal (dot-prefix = tool configuration)
- Extensible (can add other LLM tool configs later)
- Clean root directory

**CLAUDE.md serves as "bootloader":**
- Points LLMs to constitution/ on wake-up
- Contains project-specific context (tech stack, conventions, gotchas)
- Immutable framework section + editable project section

**Authority:** Kurtis Papple

---

### D46: GLOBAL-RULES.md → RULES.md Rename (2025-12-03)

**Problem:** Should rules file be called GLOBAL-RULES.md or simply RULES.md?

**Decision:** Rename to RULES.md

**Rationale:**
- Folder context (`constitution/`) already signals "global"
- Simpler, cleaner: `constitution/RULES.md` vs `constitution/GLOBAL-RULES.md`
- Saves tokens (every reference to the file is shorter)
- Consistent with constitution/GOALS.md pattern (not constitution/GLOBAL-GOALS.md)
- Still disambiguates from local rules (which live in specs as documented)

**Token savings:** ~5-10 tokens across all references

**Authority:** Kurtis Papple

---

### D47: Core Components Formatting and Duplication Fix (2025-12-03)

**Problem:** Core Components intro had formatting inconsistency and some explanatory duplication

**Decision:** Simplified to numbered list format

**Changes:**
```markdown
This framework has five essential components:

1. **CONSTITUTION** (this document)
2. **GOALS** and **RULES** (answer: "what game are we playing?")
3. **SPECIFICATIONS** (blueprints: what to build and why)
4. **ROADMAP** (execution: what's prioritized and what's next)
```

**Rationale:**
- Consistent formatting (numbered list throughout)
- Removes duplication (brief descriptions don't repeat detailed sections below)
- Preserves game-framing analogy (critical differentiator from other spec-driven frameworks)
- GOALS and RULES mentioned together to introduce "what game are we playing?" concept
- Token-efficient while maintaining clarity

**Important note:** There ARE 5 components (CONSTITUTION, GOALS, RULES, SPECIFICATIONS, ROADMAP). GOALS and RULES are mentioned together in intro specifically to introduce the game-framing analogy, which is THE key differentiator explaining why these artifacts are needed.

**Authority:** Kurtis Papple

---

### D48: Remove Origin Sections from Templates (2025-12-03)

**Problem:** Origin sections duplicate information already captured in Requirements Changelog v1 entry.

**Options considered:**
1. Keep both Origin and Changelog
2. Remove Origin, rely on Changelog v1
3. Remove Changelog, keep Origin

**Decision:** Remove Origin sections, enhance Changelog v1 (Option 2)

**Rationale:**
- Changelog v1 already captures: who requested, why, when, what was decided
- Origin section creates redundancy (two places for same info)
- Token waste: 40 tokens × N specs = significant at scale
- Maintenance burden: two places to keep in sync
- Changelog is better positioned ("read when you need context")
- Aligns with R12 (single source of truth)
- R6 requirement was "imagined" - artifact from rejected REQUEST → SPEC pattern

**Token savings:** -40 per spec × N specs

**Authority:** Kurtis Papple

---

### D49: R6 Revision - Focus on Evolution Tracking (2025-12-03)

**Problem:** R6 mandated "Origin section capturing who requested, why, and when" but this language came from an abandoned REQUEST → SPEC pattern idea.

**Original R6:**
> All specs must include Origin section capturing who requested, why, and when.

**New R6:**
> All specs must track their evolution in Requirements Changelog starting with v1.

**Rationale:**
- Removes "CYA traceability" language (who/why/when artifact from REQUEST → SPEC)
- Focuses on actual framework need: tracking evolution over time
- Requirements Changelog v1 naturally captures initial context
- Simpler, clearer rule
- Doesn't mandate redundant sections
- Emphasizes evolution (the real value) over point-in-time origin

**Authority:** Kurtis Papple

---

### D50: done/ Folder Structure for Archive (2025-12-03)

**Problem:** How to handle completed work when both task entries (from ROADMAP.md) and plan files (from plans/) need archiving?

**Options considered:**
1. **Hybrid (done.md + done/ folder)** - Two locations for "done"
   - Pro: Matches different archival needs
   - Con: Confusing - "where does done stuff go?"

2. **All-folder structure** - Every completed task becomes a file
   - Pro: Consistent
   - Con: Overhead, violates "start simple" principle

3. **done/ folder with done.md inside** - Single location for all completed work
   - Pro: Single source of truth (R12), discoverable, flexible
   - Pro: Scales naturally (start with done.md, accumulate plans over time)
   - Pro: No overhead (tasks don't become files unless they're plans)
   - Con: Slight nesting but reasonable trade-off

4. **Flat with archive/ folder** - Use "archive" instead of "done"
   - Pro: "archive" might be clearer
   - Con: "done" better signals completion in agile context

**Decision:** Option 3 (done/ folder with done.md inside)

**Structure:**
```
roadmap/
  ROADMAP.md          # Active work (Now/Next/Later)
  inbox/              # Raw inputs to process
  plans/              # Active plans for complex work
  done/
    done.md           # Completed task entries from ROADMAP.md
    [plan-name].md    # Completed plan files moved here
```

**How it works:**
- Simple tasks: Listed in ROADMAP.md → cut/paste to `done/done.md` when complete
- Complex work: Create `plans/[name].md` → reference in ROADMAP.md → move to `done/` when complete
- Single location principle: All completed work lives in `done/`

**Rationale:**
- Aligns with R12 (single source of truth) - one location for completed work
- Self-guiding structure - "Where's completed work?" → "In done/ folder"
- Not over-prescriptive - no mandated plan format, just guidance
- Scales naturally - start simple, add plans when needed
- Token-efficient - simpler explanation (~70 token savings in ROADMAP.md appendix)
- Research-backed: Archive > delete per industry best practices (Atlassian, Everhour)
- Common pattern: done.md file is standard in markdown-based task management

**Token impact:** ~70 tokens saved by removing prescriptive plan format and simplifying done/ explanation

**Authority:** Kurtis Papple

**Research sources:**
- Atlassian: Backlog Refinement best practices
- Everhour: Backlog Refinement 2025
- Markdown task management patterns (pankajpipada.com, tasks.md)

---

### D51: Clarify "Specifications" Terminology and Folder Structure (2025-12-03)

**Problem:** Framework grouped three conceptually different artifacts under "SPECIFICATIONS" folder, causing confusion about what "specs" means. Test specs had "Requirements Changelog" section that didn't make sense (tests track coverage, not requirements). Pattern templates were prescriptive when patterns emerge organically.

**Context from research:**
- Industry SDD (Spec-Driven Development): "Specifications" = domain/feature requirements (WHAT to build)
- Test specifications = verification artifacts (HOW to verify), NOT requirements documents
- GitHub Spec-Kit: "Specifications become the primary artifact. Code becomes its expression."
- Patterns emerge over time from recurring technical challenges, shouldn't be templated upfront

**Options considered:**

1. **Keep current confusing structure** - specs/domain/, specs/tests/, technical/patterns/ all called "specs"
   - Con: Semantically inaccurate, test specs don't have "requirements"

2. **Long descriptive names** - specifications/, verification/, implementation/
   - Pro: Conceptually accurate
   - Con: Verbose folder names, against "token efficiency" principle

3. **Short names with conceptual clarity in docs** - specs/, tests/, technical/
   - Pro: Industry-standard short names, token-efficient
   - Pro: Documentation explains conceptual meaning
   - Pro: Clear separation of concerns

**Decision:** Option 3 (Short names with conceptual clarity)

**Final structure:**
```
specs/                    # Specifications (WHAT/WHY) - requirements
  SPEC-TEMPLATE.md
  README.md
  [feature-name].md

tests/                    # Verification (HOW to verify)
  TEST-TEMPLATE.md
  README.md
  [feature-name]-tests.md

technical/                # Implementation guidance (HOW to implement)
  README.md
  # Users organize as needed: patterns/, architecture/, adr/, api/
```

**Changes made:**
1. Renamed `specs/domain/` → `specs/` (specifications)
2. Renamed `specs/tests/` → `tests/` (verification)
3. Removed `technical/patterns/` prescriptive structure
4. Removed PATTERN-TEMPLATE.md from core framework
5. Created `technical/README.md` with guidance (not template)
6. Renamed `DOMAIN-SPEC-TEMPLATE.md` → `SPEC-TEMPLATE.md`
7. Renamed `TEST-SPEC-TEMPLATE.md` → `TEST-TEMPLATE.md`

**Rationale:**
- **Industry-aligned:** "Specs" = domain requirements in SDD terminology
- **Semantically accurate:** Specs contain requirements; tests contain coverage decisions
- **Token-efficient:** Shorter folder names, less explanation needed
- **Not over-prescriptive:** Patterns emerge organically, no mandated format
- **Clear separation:** Three distinct artifact types with clear purposes
- **LLM-friendly:** Guidance examples in technical/README emphasize consistency

**Token impact:** Net savings ~550 tokens (removed pattern template + prescriptive structure)

**Authority:** Kurtis Papple

**Research sources:**
- Spec-Driven Development (marmelab.com, Ministry of Testing)
- GitHub Spec-Kit SDD explanation (input-consumed/)
- Test specification terminology (lambdatest.com)

---

### D52: Revise R6 to Apply Only to Specifications (2025-12-03)

**Problem:** R6 mandated "All specs must track their evolution in Requirements Changelog" but test specs don't track "requirements"—they track test coverage decisions.

**Original R6:** "All specs must track their evolution in Requirements Changelog starting with v1."

**New R6:** "All specifications must track their evolution in Requirements Changelog starting with v1."

**R6 Appendix clarification added:**
> "Specifications in specs/ track requirements evolution over time; v1 entry captures initial context (who requested, why, what was decided); subsequent entries document how requirements evolved. Test specifications track test coverage decisions, not requirements—they don't need this section."

**Changes made:**
1. Removed "Requirements Changelog" section from TEST-TEMPLATE.md
2. Updated tests/README.md to remove changelog references
3. Updated R6 rule text and appendix

**Rationale:**
- Only specifications (specs/) contain requirements that evolve
- Test specs track coverage decisions, not requirements evolution
- Semantically accurate after clarifying "specs" terminology (D51)
- Reduces confusion and unnecessary documentation
- Token savings: ~60 tokens per test spec

**Token impact:** -60 tokens per test spec created

**Authority:** Kurtis Papple

---

**End of Decisions Log**

All decisions documented through V5 development (2025-12-02 to 2025-12-03).

---

## V6 Decisions (2025-12-04)

### D53: Rules Changelog for Global Tracking (2025-12-04)

**Problem:** V5 tracked spec evolution (Requirements Changelog per R6) but NOT global rule evolution. Asymmetry: low-impact changes (per-spec) tracked, high-impact changes (global rules) not tracked.

**Options considered:**
1. **Keep current** - No global tracking
2. **Add Rules Changelog** - Version-based tracking in RULES.md
3. **Separate decision log** - ADRs only
4. **Hybrid** - Rules Changelog + optional ADRs

**Decision:** Option 2 - Add Rules Changelog to RULES.md

**Implementation:**
- Renamed "Appendix: Rule Context" → "Rules Changelog"
- Version-based organization (v1, v2, v3...)
- v1 documents the Universal Rules baseline (R1-R3 after D71)
- Future versions track Added/Modified/Removed Context-Specific Rules
- Template provided for future entries

**Rationale:**
- Creates parallel structure: Global rules (Rules Changelog) ↔ Local requirements (spec Changelog)
- High-impact changes (global rules affecting entire project) now documented
- Maintains single source of truth (R12) - rules and their history in one file
- Token-efficient (read only when investigating rule changes)

**Authority:** Kurtis Papple

---

### D54: Requirements vs Rules Distinction (2025-12-04)

**Problem:** "Business Logic" section overlapped with Requirements. ChatGPT identified semantic distinction: Requirements = desired outcomes, Rules = governing constraints.

**Analysis:**
- Requirements: "Users can log in with email/password" (capability, outcome)
- Rules: "Password must be 12+ characters" (constraint, condition)
- Business Logic contained BOTH, creating confusion

**Options considered:**
1. **Keep separate sections** - Requirements + Business Logic
2. **Merge completely** - Single Requirements section
3. **Separate semantically** - Requirements (outcomes) + Rules (constraints)

**Decision:** Option 3 - Separate Requirements from Rules

**Implementation:**
- Requirements section: Must have / Should have / Nice to have (MoSCoW)
- Rules section: Constraints and conditions governing feature behavior
- Eliminated "Business Logic" term (not applicable to personal projects)
- Clear distinction in template guidance

**Rationale:**
- Semantically accurate: requirements ≠ rules (different functions)
- Requirements = goals, Rules = guardrails
- Matches industry distinction (requirements engineering vs. business rules)
- Parallels RULES.md structure (global rules ↔ local rules in specs)
- Clearer mental model for both humans and LLMs

**Authority:** Kurtis Papple (insight from ChatGPT semantic analysis)

---

### D55: "Changelog" over "Requirements Changelog" (2025-12-04)

**Problem:** "Requirements Changelog" is verbose. Context (it's in a spec) makes "requirements" redundant.

**Decision:** Simplify to "Changelog"

**Rationale:**
- Conciseness: saves ~13 chars per use
- Context clarity: obviously tracking that spec's evolution
- Cleaner: less visual noise in templates
- Applies to all artifact types (specs, tests, rules)

**Token impact:** ~13 chars per spec/test × N documents = significant savings at scale

**Authority:** Kurtis Papple

---

### D56: "Rules" over "Local Rules" (2025-12-04)

**Problem:** "Local Rules" was meant to parallel "Global Rules" but context makes "Local" redundant.

**Decision:** Use "Rules" in spec templates (not "Local Rules")

**Rationale:**
- Context clarity: it's in a spec, obviously feature-specific
- Simpler language
- Saves ~6 chars per use

**Authority:** Kurtis Papple

---

### D57: R4 Revised for Template Flexibility (2025-12-04)

**Problem:** R4 stated "Templates define required structure and fields. Follow templates as written." This conflicted with D7 principle of "not overly prescriptive where flexibility is appropriate."

**Original R4:** "Templates define required structure and fields. Follow templates as written."

**New R4:** "Templates provide structure and guidance. Sections marked [REQUIRED] must be included."

**Rationale:**
- Acknowledges templates as guidance, not rigid mandates
- [REQUIRED] markers make mandatory sections explicit
- Allows omitting optional sections (e.g., Rules if no constraints, User Flow if not helpful)
- Balances structure (framework compliance) with flexibility (adapt to feature needs)

**Authority:** Kurtis Papple

---

### D58: [REQUIRED] Markers over Asterisk Notation (2025-12-04)

**Problem:** How to indicate mandatory sections - `*` or `[REQUIRED]`?

**Options considered:**
1. **Asterisk (*)** - Minimal (1 char), needs explanation (~25 chars)
2. **[REQUIRED]** - Self-documenting (10 chars), no explanation needed

**Token analysis:**
- Single template: [REQUIRED] wins (20 chars vs 27 chars with explanation)
- Framework-wide (4 uses): Asterisk saves ~11 chars (~2 tokens)

**Decision:** Use [REQUIRED]

**Rationale:**
- Self-documenting (no legend needed)
- Instantly clear to humans and LLMs
- Better for accessibility (screen readers, search, grep)
- Token savings negligible (~2 tokens framework-wide)
- Intuition > 2 tokens

**Authority:** Kurtis Papple

---

### D59: Remove 'framework' Field from Frontmatter (2025-12-04)

**Problem:** Every spec had `framework: TGSA v6.0` in frontmatter. This is project-level info (same for ALL specs), not document-level.

**Analysis:**
- `framework: TGSA v6.0` - Project-level (declared in CONSTITUTION.md)
- `version: 1` - Document-level (tracks THIS spec's evolution)

**Decision:** Remove `framework:` field from all per-document templates

**Implementation:**
- Kept in CONSTITUTION.md frontmatter (project-level declaration)
- Removed from SPEC-TEMPLATE.md, TEST-TEMPLATE.md, RULES.md, GOALS.md, ROADMAP.md

**Rationale:**
- Eliminates redundancy (~15 chars per spec)
- Project-level info stays at project level (single source of truth)
- Token savings: ~15 chars × 50+ specs = ~750+ chars saved

**Token impact:** Significant savings at scale

**Authority:** Kurtis Papple

---

### D60: Unified Changelog Format (2025-12-04)

**Problem:** Three different changelog formats existed:
- Rules Changelog: Added/Modified/Removed + Rationale + Authority + Impact
- Spec Changelog: Initial Request + Requirements + Decisions + Related
- Test Changelog: Initial Coverage + Related Spec + Decisions

**Options considered:**
1. **Unified format** - Same fields across all changelogs
2. **Artifact-specific** - Different fields per type (current state)
3. **Hybrid** - Base required fields + optional artifact-specific

**Decision:** Unified format with Changes + Rationale + Notes

**Format:**
```markdown
### vN - YYYY-MM-DD

**Changes:** [What changed]

**Rationale:** [Why it changed]

**Notes:** [Optional - any additional context: source, impact, decisions, related artifacts, etc.]
```

**Rationale:**
- Consistency across all artifact types (lower cognitive load)
- "Changes" = flexible (works for rules, requirements, test coverage)
- "Rationale" = captures "why" universally
- "Notes" = catch-all signals "add more context if relevant" without being prescriptive
- Forces good practice (separate what from why)
- Reinforces parallel structure (Rules Changelog ↔ Spec Changelog ↔ Test Changelog)

**Applied to:**
- RULES.md Rules Changelog
- SPEC-TEMPLATE.md Changelog
- TEST-TEMPLATE.md Changelog

**Token impact:** Slight reduction (simpler format, less prescribed fields)

**Authority:** Kurtis Papple

---

**End of V6 Decisions Log**

All decisions documented through V6 development (2025-12-04).

---

## V7 Decisions (2025-12-04)

### D61: Self-Review Checklists in Templates (2025-12-04)

**Problem:** LLM-generated specs/tests may lack quality validation, ambiguities may go unresolved, and completeness may not be verified before finalization.

**Options considered:**
1. **Appendix to CONSTITUTION + checklists** - Comprehensive guidance (~350-400 tokens)
2. **Enhanced LLM Working Expectations + checklists** - Expand existing section (~330 tokens)
3. **Minimal checklists only** - Add compact self-review sections to templates (~175 tokens)

**Decision:** Option 3 - Minimal checklists only

**Implementation:**
- Add "Self-Review" section to SPEC-TEMPLATE.md with 6-item checklist (~90 tokens)
- Add "Self-Review" section to TEST-TEMPLATE.md with 5-item checklist (~85 tokens)
- No new appendix or expansion to CONSTITUTION.md
- Total token cost: ~175 tokens (~2.4% framework increase)

**Rationale:**
- **ROI Analysis:** Checklists provide 80% of value at 20% of token cost
- **Point of Use:** Guidance where it's needed (in templates during creation)
- **Framework Philosophy:** "Start simple, scale when pain appears" - add appendix later if needed
- **Token Efficiency:** Respects R10 (token optimization) and core principle #1
- **Existing Coverage:** "LLM Working Expectations" already covers general approach in CONSTITUTION.md
- **Quality Improvement:** Forces validation without over-explaining

**Checklist Changes:**
- Original proposal referenced undefined "[NEEDS CLARIFICATION]" process
- Revised to "All ambiguities resolved or explicitly documented"
- "Happy path, errors, and edge cases tested" → "Happy path, errors, exceptions and edge cases tested"

**Token impact:** +175 tokens (~2.4% increase) for significant quality improvement

**Authority:** Kurtis Papple

---

### D62: DECISIONS.md as Core Living Document (2025-12-04)

**Problem:** V6 tracked artifact evolution (Spec Changelogs, Rules Changelog, Test Changelogs) but NOT project-level decisions. Gap: no place to capture cross-cutting choices affecting multiple artifacts or the project as a whole (e.g., "PostgreSQL vs MongoDB?", "Mobile-first vs desktop-first?", "API versioning strategy?").

**Context:** In this repo's development, requirements-and-decisions.md decision log has been extremely valuable for tracking framework evolution and keeping development on track.

**Options considered:**
1. **No Decision Log** - Rely on changelogs and optional ADRs only
   - Con: Gap remains, inconsistent (track low-impact changes but not high-impact decisions)
2. **Optional Decision Log** - Add guidance to technical/README.md
   - Con: Optional pattern, less valuable without standardization
3. **Required Decision Log** - Create DECISIONS.md as core living document
   - Pro: Parallel structure (Rules Changelog → DECISIONS.md → Spec Changelogs)
   - Pro: Captures high-impact choices, single source of truth
   - Pro: User-validated (valuable in this repo's development)
4. **Hybrid ADR + Decision Log** - Separate technical vs non-technical
   - Con: Two locations (violates R12), confusing boundary

**Decision:** Option 3 - Create constitution/DECISIONS.md as core living document

**Implementation:**
- New file: `constitution/DECISIONS.md`
- Format: DN: [Title] (Date) with Problem/Options/Decision/Rationale/Notes
- "Notes" field replaces "Authority" (more flexible - can include who decided plus other context)
- Captures ALL cross-cutting project decisions (technical, product, process, prioritization)
- Referenced in Constitution's Core Components and LLM workflow sections

**Rationale:**
- **Parallel Structure:** Rules Changelog (global rules) → DECISIONS.md (global decisions) → Spec Changelogs (local changes)
- **High ROI:** ~250 tokens for significant value (captures high-impact choices that affect entire project)
- **User-Validated:** Extremely valuable in this repo's framework development
- **LLM Value:** Provides decision context across sessions, prevents re-litigating past choices
- **Industry Practice:** Decision logs common in well-managed projects
- **Single Source of Truth:** All project decisions in one place (R12)
- **Scales Naturally:** Simple projects = few decisions; complex projects = comprehensive log
- **Location:** constitution/ folder (governance function alongside goals and rules)

**Differentiation from ADRs:**
- DECISIONS.md = Required single source of truth for ALL project decisions
- ADRs in technical/ = Optional detailed architecture documentation (deep-dives)
- DECISIONS.md is lean format for all decisions; ADRs for complex technical explanations if needed

**Format uses "Notes" not "Authority":**
- More flexible (can include who decided plus other context)
- Less formal (better for personal/small projects)
- Aligns with unified changelog format (D60) using "Notes" as catch-all

**Token impact:** +250 tokens (~3.5% framework increase)

**Authority:** Kurtis Papple

---

### D63: ADR Guidance and Relationship to DECISIONS.md (2025-12-04)

**Problem:** With DECISIONS.md created as single source of truth for project decisions, need to clarify relationship with Architecture Decision Records (ADRs) commonly used in technical/ folder.

**Options considered:**
1. **ADRs only** - Use ADRs in technical/, remove DECISIONS.md
   - Con: ADRs verbose, not LLM-friendly, overkill for simple decisions
2. **DECISIONS.md only** - No ADRs allowed
   - Con: Some teams benefit from detailed architecture documentation
3. **Separate domains** - ADRs for technical, DECISIONS.md for non-technical
   - Con: Confusing boundary, violates R12 (single source of truth)
4. **Layered approach** - DECISIONS.md required (all decisions), ADRs optional (detailed documentation)
   - Pro: Single source of truth maintained, flexibility for complexity
   - Pro: "Start simple, scale when pain appears"

**Decision:** Option 4 - Layered approach with clear guidance

**Implementation:**
- DECISIONS.md = Required lean decision log for ALL significant decisions
- ADRs in technical/adr/ = Optional detailed documentation for complex technical decisions
- ADR references DECISIONS.md entry: "See DECISIONS.md DN for summary"
- DECISIONS.md can reference ADR: "See technical/adr/003-database-choice.md for detailed analysis"
- Add guidance to technical/README.md explaining relationship

**Rationale:**
- Maintains single source of truth (R12) - DECISIONS.md has ALL decisions
- Provides flexibility - teams can add detailed ADRs when valuable
- Not overly prescriptive - guidance states ADRs are optional, doesn't dictate when
- Prevents duplication - ADRs reference DECISIONS.md entries
- LLM-friendly - lean DECISIONS.md for context, detailed ADRs when humans need depth
- Respects "start simple, scale when pain appears" principle

**Guidance is non-prescriptive:**
- States ADRs are optional
- Shows format and workflow
- Does NOT prescribe "when to" or "when not to" create ADRs
- Lets teams decide based on their needs

**Token impact:** +120 tokens in technical/README.md

**Authority:** Kurtis Papple

---

### D64: Test Template Refinement (2025-12-04)

**Problem:** TEST-TEMPLATE.md had several issues compared to refined SPEC-TEMPLATE.md: (1) Changelog still present despite D52 stating it was removed, (2) redundant `validates:` frontmatter field, (3) verbose with 3 scenario examples, (4) Test Coverage wording didn't match "errors, exceptions and edge cases" convention.

**Options considered:**
1. **Minimal fixes** - Fix bugs, update wording, condense examples
   - Pro: Addresses all issues without over-engineering
   - Pro: Net token savings from removing Changelog
2. **Major refactor** - Complete restructure to match SPEC-TEMPLATE quality
   - Con: Risk of over-engineering, more work

**Decision:** Option 1 - Minimal fixes

**Implementation:**
1. Remove `validates: [domain-spec-id]` from frontmatter (redundant with body content)
2. Remove Changelog section entirely (per D52, should have been removed in V6)
3. Update Test Coverage checklist: "Happy path, errors, exceptions and edge cases tested"
4. Remove Scenario 3 example (keep 2 examples instead of 3 for conciseness)
5. Add guidance note after Test Scenarios section
6. Update final instruction to remove Changelog reference

**Rationale:**
- **Fixes V6 bug:** Changelog was supposed to be removed in D52 but remained
- **Reduces redundancy:** validates: field duplicates body content
- **Improves consistency:** Test Coverage wording matches framework convention
- **Token efficiency:** Net -60 tokens from removing Changelog, shorter template
- **Cleaner template:** 2 scenario examples sufficient (users can add more)
- **Better guidance:** Note reminds users to add scenarios as needed

**Token impact:** Net -60 tokens (~0.8% framework reduction)

**Authority:** Kurtis Papple

---

### D65: Spec Changes Process - Edit-in-Place (2025-12-04)

**Problem:** Framework had clear process for NEW features (spec > test > task > code) but no documented process for CHANGES to existing specs. When requirements evolve (add/modify/remove requirements, implement deferred nice-to-haves), how should teams handle it?

**Options considered:**
1. **Edit-in-Place** - Directly edit specs/tests, track in Changelog
   - Pro: Simplest, uses existing mechanisms (Changelog, versioning)
   - Pro: Single source of truth (R12), no merge complexity
   - Pro: Standard practice, token efficient
2. **Delta Specs** - Create change-spec, implement, then merge
   - Con: More overhead, temporary duplication, merge step required
3. **Branch/Version Specs** - Keep multiple versioned files
   - Con: File proliferation, violates R12, complex
4. **Hybrid** - Edit-in-place with optional archive
   - Con: Adds complexity deciding when to archive

**Decision:** Option 1 - Edit-in-Place

**Process:**
1. Edit the spec in place (add/modify/remove requirements)
2. Increment version number in frontmatter (v1 → v2)
3. Add new Changelog entry explaining what changed and why
4. Update tests to reflect changes
5. Create ROADMAP tasks describing implementation delta
6. Implement code changes
7. Mark spec as updated version when complete

**Rationale:**
- **Uses Existing Mechanisms:** Changelog and versioning already designed for evolution tracking
- **R12 Compliance:** Single source of truth maintained (one spec file, not multiple)
- **Simplest Workflow:** No additional steps, files, or merge complexity
- **Token Efficient:** No extra process documentation needed (~80 tokens for guidance only)
- **Standard Practice:** How most teams handle specification evolution
- **Changelog Sufficient:** Captures what/why/when changed plus context
- **Framework Philosophy:** "Start simple, scale when pain appears"
- **Git Integration:** Teams using version control have full history available

**Documentation Added:**
- "Evolving Specifications" section in specs/README.md
- Explains edit-in-place workflow with example
- Shows Changelog v2 format for tracking changes

**Token impact:** +80 tokens in specs/README.md

**Authority:** Kurtis Papple

---

### D66: Framework Renamed to Lightspec (2025-12-04)

**Problem:** TGSA (Token-efficient, Game-framed, Spec-driven, Agentic-workflow) is descriptive but not memorable. Acronym is hard to pronounce ("tee-gee-ess-ay"), sounds technical/corporate, doesn't convey the framework's approachability or key value proposition.

**Options considered:**
1. **Keep TGSA** - Descriptive but unmemorable
2. **Lightspec** - "Light" (lightweight) + "Spec" (specification-driven)
   - Pro: Clear meaning, easy to pronounce, professional, memorable
   - Pro: Conveys core value (lightweight spec framework)
   - Pro: Tagline: "Lightweight spec-driven development for LLM-powered teams"
3. **Specterse** - "Spec" + "terse", sounds like "spectre" (ghost/lightweight)
   - Con: Pronunciation ambiguous, "terse" might sound negative
   - Con: Wordplay might feel forced

**Decision:** Option 2 - Rename to Lightspec

**Tagline:** "Lightweight spec-driven development for LLM-powered teams"

**Implementation:**
- Update all references from "TGSA Framework" to "Lightspec"
- Remove TGSA acronym expansion (no longer needed with clear name)
- Update README.md header and description
- Update CONSTITUTION.md header
- Update CHANGELOG.md
- Keep version numbering: Lightspec v7.0 (internal development history preserved)
- File structure and principles unchanged (only branding)

**Rationale:**
- **Immediately Clear:** Name communicates "lightweight specification framework"
- **Professional:** Sounds like a real product, not an acronym or pun
- **Easy to Say:** "We use Lightspec" flows naturally in conversation
- **Memorable:** Simple, clean, no pronunciation confusion
- **Marketing-friendly:** Tagline clearly positions framework for LLM development
- **Broader Appeal:** Works for personal projects and enterprise teams
- **Token-efficient:** Shorter name saves tokens in every reference

**Branding:**
- Name: Lightspec
- Full tagline: "Lightweight spec-driven development for LLM-powered teams"
- Short tagline: "Lightweight spec-driven development"
- Version: Lightspec v7.0

**Token impact:** Net savings (shorter name than "TGSA Framework" in all references)

**Authority:** Kurtis Papple

---

### D67: Core Components Section Refactor (2025-12-04)

**Problem:** CONSTITUTION.md Core Components section (lines 56-133) had multiple structural issues: (1) Wrong count ("five" but lists 4), (2) DECISIONS.md missing from V7, (3) Inconsistent structure (intro lists 4, details have 7+ subsections), (4) Heavy duplication (~77 lines), (5) Game-framing buried and not reinforced, (6) Workflow misplaced under IMPLEMENTATION subsection, (7) Empty "## CONSTITUTION" header with no body.

**Analysis:**
- Current lists CONSTITUTION, GOALS+RULES, SPECIFICATIONS, ROADMAP as "five" (actually 4)
- Detail subsections include GOALS, RULES, SPECIFICATIONS, VERIFICATION, IMPLEMENTATION GUIDANCE, ROADMAP (6-7 items)
- VERIFICATION and IMPLEMENTATION GUIDANCE not mentioned in intro list
- Game-framing key differentiator ("what game are we playing?") mentioned once but not emphasized
- Workflow embedded under IMPLEMENTATION but applies to entire framework

**Decision:** Restructure Core Components with clear hierarchy and consolidation

**New structure (6 components):**
1. CONSTITUTION (this document)
2. GOALS and RULES answer: "what game are we playing?"
3. DECISIONS track: "why did we choose this path?"
4. SPECIFICATIONS (blueprints: what to build and verify)
5. ROADMAP (execution: what's prioritized and what's next)

**Changes implemented:**
1. Update count to "six essential components"
2. Add DECISIONS as component #3 with game-framing analogy
3. Consolidate SPECIFICATIONS, VERIFICATION, IMPLEMENTATION GUIDANCE into single "Specifications: What to Build and Verify" section
4. Create section header "Goals and Rules: What Game Are We Playing?" reinforcing game-framing
5. Move Workflow to Specifications section (applies to spec/test/implementation flow)
6. Remove empty "## CONSTITUTION" header
7. Condense all subsections (~40% reduction in verbosity)
8. Parallel structure: All subsections follow [Name], [Location], [Brief description]

**Rationale:**
- **Fixes count mismatch:** 6 components accurately listed
- **Adds DECISIONS:** New V7 component included with game-framing analogy
- **Reduces duplication:** Consolidation eliminates verbose repetition
- **Reinforces differentiator:** Game-framing ("what game are we playing?") elevated to section header
- **Logical grouping:** Specifications encompasses what/verify/implement (single concept)
- **Workflow placement:** Belongs in Specifications section, not buried under subsection
- **Token efficiency:** Net -150 tokens despite adding DECISIONS
- **Clearer structure:** Intro list matches detailed subsections (no mystery items appearing later)

**Token impact:** Net -150 tokens (~2% framework reduction)

**Authority:** Kurtis Papple

---

### D68: Optional "user(s)" Field for Spec Dependencies (2025-12-04)

**Problem:** Need a lightweight way to track who/what a spec serves without forcing vertical/horizontal categorization or directory splits.

**Context:** Reviewed vertical-horizontal-spec-argument.md proposing separation of feature specs (vertical) from platform/pattern specs (horizontal). Full implementation would add overhead for small projects.

**Options considered:**
1. **Full vertical/horizontal split** - Separate directories, terminology, templates
   - Pro: Clear separation of concerns
   - Con: Overhead for small projects, premature structure
2. **Optional tagging with `type:` field** - Add `type: vertical|horizontal`
   - Pro: Minimal, optional
   - Con: Introduces terminology that needs explaining
1. **Simple user(s):` field** - Declares who/what the spec serves
   - Pro: Self-documenting, no terminology, flexible
   - Con: Less structured than explicit categorization
4. **No change** - Current structure sufficient
   - Pro: No added complexity
   - Con: Misses opportunity for lightweight dependency tracking

**Decision:** Option 3 - Add optional `user(s):` field to spec frontmatter

**Implementation:**
- Added user(s):` field to SPEC-TEMPLATE.md frontmatter with inline comment
- Added "Users Field and Spec References" section to specs/README.md with examples
- No directory changes, no new terminology, no required fields
- Field accepts: end users, roles ("managers"), or spec IDs (S1, S5, S6)

**Rationale:**
- **Minimal:** Single optional field, ~15 tokens added
- **Flexible:** Works for feature specs (user(s): end users) and shared specs (user(s): S1, S5)
- **Self-documenting:** No need to explain "vertical" vs "horizontal" terminology
- **Implicit categorization:** `user(s): persona = feature; `user(s): S1, S5` = shared pattern
- **Scales naturally:** Optional for small projects, useful at scale
- **Aligns with philosophy:** "Start simple, scale when pain appears"
- **Enables reuse:** Specs can explicitly declare they serve other specs, encouraging reference over duplication

**Examples:**
```yaml
user(s): end users              # Feature spec
user(s): managers, admins       # Role-specific
user(s): S1, S5, S6            # Shared pattern used by other specs
```

**Token impact:** +15 tokens (template), +80 tokens (README guidance)

**Authority:** Kurtis Papple

**Notes:** Considered but rejected full vertical/horizontal directory split from vertical-horizontal-spec-argument.md input document. The user(s):` field captures the essence (who benefits) without adding structural overhead.

---

### D69: Template Format - Bare with Hints (2025-12-04)

**Problem:** Templates contained placeholder text requiring deletion/overwriting (e.g., `[Feature Name]`, `[What and why]`, `[Requirement 1]`), making them not truly "copy-pasteable." Users had to delete content before filling in actual values.

**Options considered:**
1. **Rename templates to guides** - Keep current content, rename to DOMAIN-SPEC-GUIDE.md
   - Pro: No file duplication, single source
   - Con: Not copy-pasteable, extra work for users
2. **Split template + guide files** - Separate bare templates and detailed guide files
   - Pro: True copy-pasteable templates
   - Con: File duplication, maintenance overhead
3. **Move guidance to centralized README** - Bare templates + README guidance sections
   - Pro: Centralized, no duplication
   - Con: Guidance separated from template
4. **Bare template with inline guidance markers** - `[GUIDANCE: ...]` sections to delete
   - Pro: Guidance in context
   - Con: Still requires deletion, not truly bare
5. **Bare with brief hints** - Minimal hints (2-5 words), strip all placeholder examples
   - Pro: Copy-pasteable, hints aid memory without bloat
   - Con: Hints might need deletion (minimal)

**Decision:** Option 5 - Bare templates with brief hints, decentralized README guidance

**Implementation:**
- Updated SPEC-TEMPLATE.md and TEST-TEMPLATE.md to bare format
- Stripped frontmatter examples (`id: S1` → `id:`, `created: YYYY-MM-DD` → `created:`)
- Replaced verbose placeholders with ultra-brief hints:
  - `[Feature Name]` → (empty line after `#`)
  - `[What and why]` → `What and why in 1-2 sentences.`
  - `[Requirement 1]` → `-` (just bullet point)
  - `[Optional]` → `Optional. Step-by-step interaction flow.`
- Added footer: `📖 See README.md for detailed guidance and examples`
- Added complete specification example to specs/README.md (User Login example)
- Confirmed tests/README.md already has complete scenario example
- Confirmed technical/README.md provides pattern/ADR examples (no template needed)

**Rationale:**
- **Truly usable:** Users copy and start typing, hints are helpful or trivially ignored
- **Token-efficient:** ~45% reduction per template (450→250 tokens for SPEC, 400→220 for TEST)
- **Balances bare vs. context:** Structure visible without reading full README every time
- **Decentralized guidance:** Each README owns its domain's examples and instructions
- **Complete examples:** READMEs provide filled-out examples users can reference

**Token impact:**
- SPEC-TEMPLATE.md: 450 → 250 tokens (-45%)
- TEST-TEMPLATE.md: 400 → 220 tokens (-45%)
- specs/README.md: +320 tokens (complete example)
- Net: ~-300 tokens

**Authority:** Kurtis Papple

### D70: Deleted all previous versions and renamed version-7 to version-1 

this is going to be our first release, so no more internal versioning from here on.

### D71: Universal Rules Reduced to 3 (2025-12-04)

**Problem:** R1-R12 list increased token cost and duplicated guidance already present in templates/READMEs. Needed a leaner, higher-signal set for the constitution.

**Options considered:**
1. Keep 12 universal rules and trim wording.
2. Reduce to a minimal core set, move supporting guidance into READMEs/templates.
3. Split into “core” + “extended” rules sections.

**Decision:** Option 2 — reduce to 3 universal rules (immutability, workflow, canonical locations); keep project rules in context section; rely on templates/READMEs for detailed guidance.

**Rationale:** Significant token savings; clearer anchor rules; reduces redundancy; keeps constitution concise while preserving structure via templates and READMEs.

**Authority:** Kurtis Papple

### D72: Spec Template Use Cases Section (2025-12-04)

**Problem:** Single “User Flow” felt too homogeneous and encouraged one-path thinking. Needed support for multiple use cases with distinct flows without adding bloat.

**Options considered:**
1. Keep “User Flow” as-is.
2. Rename to “Use Cases” and allow multiple flows per spec.
3. Add a new “Use Cases” section and keep “User Flow” (duplicate).

**Decision:** Option 2 — replace “User Flow” with “Use Cases (with flows)” in SPEC-TEMPLATE.md; add guidance/example in specs/README.md.

**Rationale:** Better models multiple scenarios; clearer vocabulary; minimal token impact; keeps template lean while enabling ACs/tests to map to specific use cases.

**Authority:** Kurtis Papple
