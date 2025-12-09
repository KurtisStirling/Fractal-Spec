# verify-design Command (LLM Interrogation Protocol)
*A structured command for Claude to refine, challenge, and verify the **Design** section of a Fractal Spec.*

---

# 🧠 Purpose

This command ensures Claude helps create or refine an **accurate, coherent, and requirement-aligned Design** section for a thing’s spec.

It must:

- Respect the already **verified Need** (requirements)  
- Make the design explicit, unambiguous, and internally consistent  
- Show how the design satisfies the verified requirements  
- Avoid drifting back into re-defining requirements

Claude MUST follow this workflow precisely.

---

# ❗ Precondition — Need must be verified first

Before doing any design work, Claude must:

1. Ask to see the current spec for this thing (at least the **Need** and **Design** sections).  
2. Check that the Need section contains:

   - The heading: `## Need (Verified)`  
   - The stamp:  
     `Verified by Claude using \`verify-requirements\` command on YYYY-MM-DD.`

3. If this stamp is **missing**, Claude must respond:

   > “The Need section for this thing has not been verified yet.  
   > Please run `verify-requirements` first so we have a stable, agreed set of requirements to design against.”

   Then Claude must **stop this command**.

Only if the Need is verified may Claude continue with `verify-design`.

---

# ✅ `verify-design` Command

**Claude, when I invoke `verify-design`, and the Need is verified, you must follow all steps below in order.**

---

## STEP 1 — Establish design context

Ask me:

1. *What is the current status of this thing?* (draft / partly built / fully implemented)  
2. *Is the Design meant to describe the intended future design, the current implementation, or both?*  
3. *Are there any hard technical constraints or choices already made?* (e.g., stack, framework, DB)  
4. *Do you already have a Design section written, or are we starting from almost nothing?*

Summarise back what you understood before moving on.

---

## STEP 2 — Read the verified Need and current Design

Claude must:

1. Read the **Need (Verified)** section carefully.  
2. Read any existing **Design** content for this thing (if present).  
3. Summarise briefly:
   - the core Purpose  
   - key Scope points  
   - the main Requirements / Rules (R1, R2, …)  
   - any existing high-level Design ideas

This summary is just for internal orientation; keep it short.

---

## STEP 3 — Elicit missing or implicit design intent

Claude must ask focused questions to uncover design intent, such as:

- “How do you imagine this thing is structured internally?”  
- “What are its main responsibilities and non-responsibilities?”  
- “How should other components or users interact with it?”  
- “What are the main flows or scenarios you care about?”  
- “Are there any important edge cases or failure modes to account for?”  
- “What data does it own or manage, and where does it live?”  
- “What other components or services does it depend on?”

Do **not** jump straight to proposing a final design.  
First, get the missing information from me.

---

## STEP 4 — Map design to requirements (coverage check)

Claude must:

1. List the key requirements (R1, R2, R3, …) from the Need section.  
2. For each requirement, reason about:

   - How the current or intended design satisfies it  
   - Whether the coverage is clear, partial, or missing  
   - Any conflicts between requirements and design

3. Present a **Requirements → Design coverage** view, for example:

   - **R1 — [short text]** → covered by [Design parts / flows]  
   - **R2 — [short text]** → partially covered; missing X  
   - **R3 — [short text]** → not yet addressed in the design  

Ask me to confirm or correct this mapping.

If new “requirements” emerge while doing this, Claude must ask:

> “This sounds like a new requirement that is not in the Need section.  
> Should we update the Need (and re-run `verify-requirements`) before locking in the design?”

Do **not** silently add new requirements into the Design.

---

## STEP 5 — Clarify and challenge the design

Claude must now interrogate the design itself:

- Identify ambiguities: "What exactly happens in X case?"
- Identify gaps: "How is Y handled?"
- Check boundaries: "Is this the responsibility of this thing, or a different thing?"
- Check consistency: "This part seems to conflict with earlier behaviour. Which is correct?"
- Ask about trade-offs only if helpful to clarify intent, not to judge.

The goal is **clarity and coherence**, not optimisation.

---

## STEP 5.5 — Check parent relationships and duplication

Claude must verify proper use of upward references:

1. **Check for parent spec duplication**
   - Ask: "Does this design duplicate anything already defined in the parent spec?"
   - If duplication found, suggest: "This is already covered in the parent. Use an upward reference instead."

2. **Verify upward reference format**
   - Check any references to parent specs use proper markdown link format: `[text](../parent.md#section)`
   - Example: `See [Authentication Rules](../backend.md#authentication) for shared auth logic.`

3. **Verify conceptual vs literal representation**
   - Ask: "Does this Design conceptually and logically represent the code/reality, rather than replicating it?"
   - The Design should make code easy to understand, not duplicate it
   - Code snippets are fine when illustrative, but avoid full code reproduction

---

## STEP 6 — Produce a refined, spec-ready Design section

When the design is well understood and agreed, Claude must output a clean **Design** section in this shape:

```
## Design

**Responsibilities**
- …

**Behaviour**
- Main flows and scenarios.
- Important edge cases and failure handling.

**Dependencies**
- Things this depends on.
```

**Optional subsections** (add if they clarify the Design):
- **Interfaces** — Endpoints, UI elements, contracts
- **Data / State** — What data it owns/manages
- **Key Decisions** — D1, D2, etc.
- Any other subsection that makes the Design clearer

Design must be:

- consistent with the verified Need
- conceptually and logically representative of the code/reality (not duplicating code)
- unambiguous enough for future-you or an LLM to implement from
- free of duplication with parent specs (use upward references instead)
- free of low-value noise or speculation

Claude should explicitly say whether the Design describes:

- current implementation,
- intended future design,
- or a mix (and where).

---

## STEP 7 — Add verification stamp

Claude MUST append this stamp after the Design section:

```
Verified by Claude using `verify-design` command on YYYY-MM-DD.
```

This signals that:

- the Design has been actively interrogated  
- it is consistent with the current verified Need  
- it is ready to be used for planning and implementation  

---

# ⚠️ Critical Behaviour Rules for Claude

Claude must:

- NOT silently change or reinterpret requirements  
- NOT introduce new requirements inside the Design  
- NOT optimise, refactor, or over-engineer the design by default  
- Ask until the design is clear, coherent, and obviously tied to the Need  
- Work collaboratively, explaining trade-offs only when needed for clarity  
- Treat the user as thoughtful and capable, using questions to uncover intent

Claude’s output must ensure the Design:

- clearly answers “how this thing works or will work”  
- clearly traces back to “why this thing exists” (the Need)  
- is usable as a blueprint for planning and implementation

---

# End of `verify-design` Command
