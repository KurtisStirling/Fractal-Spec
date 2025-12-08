# verify-requirements Command (LLM Interrogation Protocol)
*A structured command for Claude to elicit, challenge, clarify, and verify requirements for a Fractal Spec.*

---

# 🧠 Purpose

This command ensures Claude extracts **accurate, unambiguous, deeply interrogated, verified requirements** for the *Need* section of a spec.  
It forces Claude to avoid assumptions, avoid premature design, and produce clean, spec-ready requirements with a verification stamp.

Claude MUST follow this workflow precisely.

---

# ✅ `verify-requirements` Command

**Claude, when I invoke `verify-requirements`, you must follow all steps below in order.**

---

## **STEP 1 — Establish foundational understanding**
Ask me:
1. *What is this thing?*  
2. *What problem should it solve or what value should it provide?*  
3. *Why does this thing need to exist? (core reason)*  
4. *Who or what will use or depend on it?*  
5. *Is anything already built, or is this entirely new?*

Never assume anything.

---

## **STEP 2 — Elicit raw requirements**
Ask targeted questions to gather:
- functional needs  
- constraints  
- exclusions (what this thing must not do)  
- mandatory behaviours or rules  
- environmental or technical constraints  
- expectations for success  
- safety/reliability notes (if relevant)

Capture everything. Do NOT compress yet.

---

## **STEP 3 — Focused interrogation (2-3 Whys)**
For each requirement, challenge it:

- "Why does this matter?"
- "What is the underlying real need?"
- "Is this a requirement or an implementation idea?"
- Ask up to **2-3 levels of 'Why'** to reach clarity.

Goal: reduce shallow statements into **stable, universal demand** without excessive back-and-forth.

---

## **STEP 4 — Clarify ambiguity**
Ask:
- “What exactly do you mean by X?”  
- “Can you give a concrete example?”  
- “What happens in edge cases?”  
- “If X and Y conflict, which wins?”  
- “Is this behaviour mandatory, or optional?”  

Repeat until everything is unambiguous.

---

## **STEP 5 — Reflect requirements back for confirmation**
Present a clean summary and ask:

> “Please confirm: is this correct and complete?”

Loop until I explicitly answer:

> **“Yes, these requirements are verified.”**

Do NOT continue without confirmation.

---

## **STEP 6 — Produce final spec‑ready NEED section**
Claude outputs:

```
## Need (Verified)

**Purpose**
- …

**Scope**
- Includes: …
- Excludes: …

**Requirements / Rules**
- R1 — …
- R2 — …
- …

**Success Notes (optional)**
- …
```

Requirements must be:
- concise  
- unambiguous  
- independent of implementation  
- phrased as **demand**, not design  

---

## **STEP 7 — Add verification stamp**
Claude MUST append:

```
Verified by Claude using `verify-requirements` command on YYYY-MM-DD.
```

This stamp signals to future Claude runs that the Need is confirmed and should NOT be re-elicted unless the user explicitly asks.

---

# ⚠️ Critical Behaviour Rules for Claude

Claude must:
- NOT propose design during this command  
- NOT generate architecture, flows, UI, or implementation  
- NOT reorganise requirements until interrogation is complete  
- Ask until ALL ambiguity is eliminated  
- Confirm understanding before generating the final Need section  
- Work collaboratively, not prescriptively  
- Only stop when the user says: **“Yes, verified.”**

Claude must ensure the Need section is:
- actionable  
- correct  
- minimal but precise  
- stable over time  
- aligned with the fractal-spec model (demand vs supply separation)

---

# End of `verify-requirements` Command
