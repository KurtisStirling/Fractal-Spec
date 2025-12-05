This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repo develops the **Constitution Framework** - a copy-pasteable workflow system for LLM-powered development that embeds spec-driven and test-driven development principles. The output is designed to be used in other projects, not within this repo itself.

## Repository Architecture

**Three-folder structure:**

```
output/
  version-X/              # The product: copy-pasteable framework
    CONSTITUTION.md       # The core framework document
    specs/, technical/, tasks/  # Framework structure with templates

input-consumed/           # Reference documents already analyzed
input-to-consume/         # Reference documents pending analysis

requirements-and-decisions.md  # Meta: requirements & decisions for framework development
```

**Key insight:** This repo creates a framework, it doesn't use the framework. Don't apply the Constitution Framework's rules (Spec → Test → Task → Code) to this repo's own development.

### CRITICAL: Framework Rules Are Product Features, Not Development Constraints

**The framework rules (R1, R2, R3... R12, etc.) are THE PRODUCT we're building - they are NOT rules that govern how we develop the framework itself.**

When analyzing, reviewing, or designing the framework:
- ✅ **DO:** Use your own unbiased reasoning and judgment
- ✅ **DO:** Recommend changing or removing framework rules if that creates a better product
- ✅ **DO:** Question whether rules provide value vs. token cost
- ✅ **DO:** Suggest improvements even if they contradict existing rules
- ❌ **DON'T:** Cite framework rules (like R6) as rationale for design decisions
- ❌ **DON'T:** Treat framework rules as constraints on framework development
- ❌ **DON'T:** Assume existing rules are sacred or unchangeable

**Example:**
- ❌ Bad: "We shouldn't remove the Origin section because R6 requires it"
- ✅ Good: "The Origin section duplicates Requirements Changelog v1. Token ROI analysis suggests removing it and updating R6."

The framework rules apply to **users of the framework**, not to us while we're designing it.

## Working in This Repo

### Creating New Framework Versions

When iterating on the framework:
1. Create new `output/version-N/` folder
2. Copy previous version as starting point or build fresh
3. Document decisions in `requirements-and-decisions.md`
4. Update version number in CONSTITUTION.md frontmatter

### The Output Product Structure

What users get when they copy `output/version-X/`:
- **CONSTITUTION.md** - Framework structure with [CONTEXT-SPECIFIC] sections users edit
- **GLOBAL-RULES.md** - Universal + Context-Specific rules (living document)
- **Templates** - DOMAIN-SPEC-TEMPLATE.md, TEST-SPEC-TEMPLATE.md, PATTERN-TEMPLATE.md
- **ROADMAP.md** - Now/Next/Later backlog (living document, not template)
- **Folder structure** - specs/domain/, specs/tests/, technical/patterns/, task-mgmt/
- **README.md** - Usage instructions (optional)

### Critical Design Constraints

The framework MUST be:
1. **LLM token-optimized** - This is THE primary challenge. Every word counts.
2. **Universal** - Works personal → enterprise without modification
3. **Immutable sections** - Framework parts never change per-project
4. **Scalable** - Rules and roadmap can grow without bloating core documents
5. **Game-framed** - Answers "what's the goal?" and "what are the rules?"

### THE CORE CHALLENGE: Token Budget vs Comprehensiveness

**The Problem:**
Previous work (input-to-consume files) contains valuable content, but implementing it all creates a "book that burns half your token budget every new conversation."

**The Principle:**
- Framework must be **minimal but comprehensive** - not "explain everything like you're 5"
- Each section must have **positive ROI** - token cost must justify value
- Avoid excessive [OPTIONAL] markers - users can extend the framework themselves
- Goal: Sensible foundation, not one-size-fits-all behemoth

**When Designing V2+:**
1. **ROI Analysis Required** - For every new section, ask: "Does the token cost justify the value?"
2. **Ruthlessly Prioritize** - What's truly essential vs nice-to-have?
3. **Trust Users** - They can add sections on top. Framework provides foundation only.
4. **Test Token Usage** - Measure actual token counts of Constitution + templates

**Red Flags:**
- Adding sections "just in case"
- Explaining concepts that experienced devs already know
- Duplicating information across multiple locations
- Verbose explanations when terse examples suffice

### Decision Tracking

All architectural decisions go in `requirements-and-decisions.md` using this format:

```markdown
### DEC-N: [Decision Title] (YYYY-MM-DD)
**Problem:** [What needed deciding]
**Options considered:** [List with pros/cons]
**Decision:** [What was chosen]
**Rationale:** [Why]
**Authority:** Kurtis Papple
```

### Key Design Decisions Already Made

From requirements-and-decisions.md (latest critical decisions):
- **DEC-34**: V5 constitution/ folder structure (pure Scrum Guide model)
- **DEC-40**: Framework renamed to TGSA (Token-efficient, Game-framed, Spec-driven, Agentic-workflow)
- **DEC-46**: GLOBAL-RULES.md → RULES.md (folder context signals "global")
- **DEC-47**: Core Components formatting fix (5 components with game-framing analogy)
- **DEC-48**: Removed Origin sections from templates (redundant with Requirements Changelog v1)
- **DEC-49**: R6 revised - focuses on evolution tracking, not "who requested, why, when"
- **DEC-68**: Public version is 1; state it only in constitution frontmatter. Internal folders (e.g., `version-7/`) are iteration history, not release versioning.

See requirements-and-decisions.md for all decisions.

### Working with Kurtis

From requirements-and-decisions.md § Process Requirements:
- **Must be methodical** - Plan and break down tasks, don't rush
- **Cannot over-engineer** - Start simple, add when pain appears
- **Must track decisions** - Document in requirements-and-decisions.md
- **Consider holistic UX** - Think about both human and LLM users

### Input Files

- **input-consumed/** - Already analyzed and incorporated
- **input-to-consume/** - Read these when creating next version
- Move files from input-to-consume → input-consumed after analysis

## The Framework's Core Concept

The Constitution Framework enforces:
1. **Game Framing** - Goals (Mission/Objective) + Rules (Universal + Project-specific)
2. **Spec → Test → Task → Code** workflow
3. **Token-efficient reading order** for LLMs (≤300 tokens unless needed)
4. **Traceability** - Origin sections, Requirements Changelogs, related IDs
5. **Scalability** - "Start simple, scale when pain appears"

## Version History

- **v1.0** (2025-12-02) - Initial framework based on WORKFLOW-MODEL-TEMPLATE.md and chatGPT-constitution-skeleton.md
- **v2.0** (2025-12-02) - Refinements and token optimization
- **v3.0** (2025-12-02) - Major structural refactoring, removed verbose sections, 35% token reduction
- **v4.0** (2025-12-02) - Extracted GLOBAL-RULES.md, expanded to 12 universal rules, created all templates, ROADMAP as living document
- **v5.0** (2025-12-03) - ✅ COMPLETE - Template refinement, removed Origin sections, revised R6, Business Logic, MoSCoW, Test Strategy, all templates production-ready
