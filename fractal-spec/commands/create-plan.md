---
description: Create or refresh a subject-level plan inside a Fractal Spec structure
model: opus
---

# Create Plan (Fractal Spec)

You create a single active plan for a subject. Plans live alongside the subject’s spec (`subject-name.md`) and should reflect current intent at that level (roadmap-like in macro subjects, task-like in micro subjects).

## Initial response

1) If a subject path or plan path is provided, read the spec (`subject-name.md`), any existing `*-plan.md`, and nearby `research.md` fully.  
2) If nothing provided, ask for: subject path, goal/intent, constraints, and any prior research links.

## Process

1. Locate the subject
   - Confirm the folder (subject) this plan belongs to.
   - Ensure there is only one active `*-plan.md` for that subject; if one exists, you will update it.

2. Gather context
   - Read the subject spec: Requirements (demand), Design (supply), Change Log (trace).
   - Read parent spec if this is a component and shared truths matter.
   - Read existing plan (if present) and `research.md` (temporary notes).

3. Clarify minimally
   - Ask only for information you cannot infer from the spec/research.
   - Confirm scope and outcomes: what “good” looks like when this plan is done.

4. Draft the plan
   - Keep it in the subject folder as `*-plan.md` (you may rename to fit the timeframe, but only one may be active).
   - Use crisp sections; example template:

````markdown
# Plan: <subject/goal>

## Context
- Subject: <folder path>
- Demand to satisfy (from Requirements): ...
- Current supply (from Design): ...

## Objectives / outcomes
- ...

## Approach
- ...

## Tasks / increments
- [ ] Task 1 — owner/context
- [ ] Task 2 — owner/context

## Risks / open questions
- ...

## Done Appendix (for long-lived plans)
- Move completed items here as you go.
````

5. Validate and confirm
   - Restate scope, objectives, and first tasks.
   - Ask for confirmation before finalizing.

6. Finalize
   - Ensure plan is actionable and internally consistent with the spec.
   - Make clear where decisions/assumptions came from (tie back to Requirements/Design).
   - If gaps remain, call them out explicitly; do not leave silent unknowns.

## Guardrails

- One active plan per subject. Archive/rename old ones; use a Done appendix for long-lived plans.
- Do not invent semantics; defer to the subject’s spec and parent spec for shared truths.
- Keep tokens lean: avoid verbose dumps; prefer concise bullets with references to source sections.
- No open questions in the final plan: resolve via research or explicit user confirmation.
