# Plan: v7 Improvements

## Context
- Subject: fractal-specs-v7/
- Based on external review feedback and user clarifications
- Focus: Address ambiguities, reduce friction, improve LLM guidance
- Current state: v7 core model is solid; needs refinement in edges and commands

## Objectives
1. Clarify multi-level plan strategy and when multiple concurrent plans are acceptable
2. Improve decomposition guidance to reduce LLM confusion
3. Add quality-of-life tooling (versioning, linting, navigation)
4. Tone down high-latency commands while maintaining rigor
5. Create missing verify-design command with explicit linking checks
6. Add concrete examples throughout guide

## Approach
Address each feedback point systematically. Use parallel subagents where appropriate to draft solutions concurrently. Test each change against the core principles (token efficient, predictable, traceable, local, fractal).

---

## Tasks

### 1. Core Model Clarifications

All tasks completed - see Done Appendix

### 2. Command Updates

All tasks completed - see Done Appendix

### 3. Change Log Management

All tasks completed - see Done Appendix

### 4. Tooling & Artifacts

All tasks completed - see Done Appendix

### 5. Examples & Templates

All tasks completed - see Done Appendix

### 6. Research Lifecycle Clarification

Task completed - see Done Appendix

---

## Risks / Open Questions

- Multi-plan question: Is the nested-level approach sufficient, or do we need to support multiple concurrent plans at same level for truly parallel work? (Discuss after task 1 is drafted)
- Change log in git: Is referring to git history enough, or do users need markdown-based changelog for quick reference?
- Folder purity lint: Should this be a real script/tool, or just documented spec for now?

---

## Done Appendix

### Batch 1 - Core Model Clarifications (Completed 2025-12-08)

- [x] **Clarify nested multi-level plan strategy** - Added as Section 3.5
  - Full version with concrete example (projects/edit-project)
  - Changed from rule to suggestion: multiple concurrent plans allowed if useful
  - Distinguishes scheduler-like (high-level) vs task-list (low-level) plans

- [x] **Add rules for when NOT to split components** - Added to Section 5
  - Don't split if < 1 hour of work
  - Don't split attributes or non-valuable fragments
  - Examples: flowers/ good, flowers/stem/ bad
  - Emphasize collaborative approach: "ask the user if unsure"

- [x] **Clarify "Done" definition** - Added to Section 7
  - Explicit: Done = spec.Design matches production reality
  - For code: merged + deployed + spec updated
  - Distinguishes implemented ≠ deployed ≠ done

- [x] **Add guidance for horizontal vs vertical components** - Added to Section 2
  - Frontmatter pattern: `used-by: [app-a, app-b]` or `used-by: [checkout, user-profile]`
  - Horizontal (shared services/infrastructure) vs vertical (value streams/features)
  - Examples: single app with shared data-schema, and monorepo structure
  - Applies to any codebase, not just monorepos

- [x] **Clarify how to handle generated/external things** - Added to Section 3
  - Don't create specs for generated artifacts or external dependencies
  - Mention in parent spec's Design section instead
  - Examples with ✅/❌ markers

- [x] **Document spike/experiment approach** - Added as Section 6.5
  - Quick questions: no docs needed
  - Substantial experiments: create spike/ or experiment/ component
  - Example: trapscan-app/spike/
  - Can have lighter specs or just research.md

- [x] **Document research.md lifecycle explicitly** - Updated Section 3
  - Temporary → archived as `_research-YYYY-MM-DD.md` or deleted
  - Cross-reference to RPI Workflow for knowledge compression
  - "Not always needed" clarification

- [x] **Add Design conceptual representation note** - Added to Section 3
  - Design must conceptually and logically represent code/reality
  - Can include code snippets where useful
  - Intent: make code easy to understand, not replicate it

### Batch 2 - Command Updates (Completed 2025-12-08)

- [x] **Tone down verify-requirements command** - Updated commands/verify-requirements.md
  - Changed STEP 3 from "5 Whys" to "Focused interrogation (2-3 Whys)"
  - Reduced interrogation depth without losing rigor
  - Added "without excessive back-and-forth" clarification
  - Maintained verification loop and quality standards

- [x] **Add pushback logic to analyse-structure command** - Updated commands/analyse-structure.md
  - Added STEP 4.6 "Detect coherence issues"
  - Includes "dinner table test" for repo coherence
  - Gentle flagging of unrelated top-level things (CV + trapscan example)
  - Collaborative, non-dogmatic approach
  - Added repo splitting suggestion to STEP 5

- [x] **Review and update verify-design command** - Updated commands/verify-design.md
  - Added STEP 5.5 "Check parent relationships and duplication"
  - Explicit upward reference format checking: `[text](../parent.md#section)`
  - Conceptual vs literal representation verification
  - Added flexible sections note: "You may add additional sections to clarify"
  - Quality checks for architecture, interfaces, behavior, dependencies already present

- [x] **Allow flexible spec sections in verify commands**
  - Added to verify-design.md line 186
  - Maintains recommended structure but allows additions for clarity

### Batch 3 - Examples & Tooling (Completed 2025-12-08)

- [x] **Implement change log size limits** - Updated guide Section 3 and Spec-Template-v2.md
  - Added guidance: "Keep maximum 5 most recent entries (token efficiency)"
  - Added: "For older history: add note 'See git history for full change log'"
  - Updated template comment with same guidance

- [x] **Add .fractal-specs-version file guidance** - Added as Section 2.5
  - Created `/home/kurtis/fractal-specs/fractal-specs-v7/.fractal-specs-version` with content `v7`
  - Added guidance explaining purpose and LLM requirement
  - Future-proofs for v8, v9, etc.

- [x] **Create folder purity linting guidance** - Created folder-purity-lint-spec.md
  - Comprehensive specification document for lint tool
  - 6 validation checks: spec presence, plan limit, valid file types, component folders, archived naming, content validation
  - Includes error messages, regex patterns, CLI interface spec
  - Implementation-ready specification

- [x] **Add navigation helper guidance** - Added as Section 2.6
  - Created `/home/kurtis/fractal-specs/fractal-specs-v7/navigation-example.md`
  - Explains when to use (5+ components, complex domains, onboarding)
  - Example shows Trapscan structure with vertical and horizontal components
  - Optional feature for large structures

- [x] **Add plan granularity examples** - Added to Section 3.5
  - Macro-level plan example (Projects Q1 2025, quarterly timeframe)
  - Micro-level plan example (Edit Project Implementation, task-list)
  - Nested relationship explained with folder structure
  - Shows how macro item spawns micro component plan

- [x] **Add explicit linking examples** - Updated Section 6
  - Added "Why Explicit Links Matter" explanation
  - Bad examples: vague text references
  - Good examples: markdown links with anchors
  - Pattern guidance: relative path + anchor + context

- [x] **Add guidance for when plans are needed** - Updated Section 3
  - High-level: almost always (exception: inactive products)
  - Low-level: simple work (bugs) = no plan, complex work (refactors) = plan
  - Heuristic: > 1 hour OR multiple files OR needs sequencing → plan it
