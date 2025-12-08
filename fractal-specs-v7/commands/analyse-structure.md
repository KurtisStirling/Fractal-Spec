# analyse-structure Command (Things & Components Tree Design)
*A structured command for Claude to help design, review, and optimise the folder hierarchy for Fractal Specs.*

---

## 🧠 Purpose

This command is for analysing and shaping the **things & components tree** (folder structure) of a repo using the Fractal Specs model.

Claude must help ensure that:

- Each folder represents a **meaningful thing**
- Child folders are **independently valuable components** of that thing
- The structure is neither too flat nor over-fragmented
- Large or "fat" areas are decomposed only when it makes sense
- New repos start with a good initial structure
- Existing repos get a safe, planned path to improvement (via a `*-plan.md`)

Claude MUST follow this workflow precisely.

---

## ✅ `analyse-structure` Command

**Claude, when I invoke `analyse-structure`, you must follow these steps in order.**

---

## STEP 1 — Understand the repo and its purpose

Ask me:

1. What is this repo for? (one or two sentences)
2. What are the main things this repo should cover? (e.g., app, API, data pipeline, notes, experiments)
3. Is this an existing repo with files/folders, or are we designing from scratch?
4. Are there any natural "top-level things" you already think of? (e.g., web app, CLI tool, docs, infrastructure)

Do **not** assume the domain. Get a clear mental model first.

---

## STEP 2 — If repo is NEW → propose an initial structure

If there is **no real folder structure yet**:

1. Ask questions to identify:
   - the main things in the system
   - their major components
   - likely atomic areas (smallest meaningful parts)

2. Apply the Fractal Spec rules:
   - Each folder = a thing
   - Child folders = meaningful components of that thing
   - No folders for attributes
   - Stop decomposition when further splitting yields non-valuable fragments

3. Propose a **candidate top-level tree**, e.g.:

   ```text
   app/
     app.md
   api/
     api.md
   infra/
     infra.md
   ```

4. Ask me to review and confirm or adjust the proposal.

5. Once agreed, **offer** to:
   - Output a `structure-setup-plan.md` for the repo root, describing how to create the folders and specs.
   - Keep the plan high-level and editable; do not assume you will execute it automatically.

---

## STEP 3 — If repo is EXISTING → inspect current structure

If a structure already exists:

1. Ask permission to review the tree (and, if applicable, suggest commands like `tree` or `find` if you cannot see it yet).
2. Request or derive:
   - A tree of directories (at least 2–3 levels deep)
   - Approximate sizes per folder (if possible using `du` or a similar tool; otherwise ask user)

3. Summarise back what you see:
   - List top-level folders and their rough sizes
   - Call out folders that appear "fat" (many files, subfolders, or large size)
   - Note any obvious mixing of concerns (e.g., code + docs + assets nested arbitrarily)

Do **not** suggest changes yet. First reflect what you see.

---

## STEP 4 — Evaluate structure using Fractal Specs rules

For each major folder (thing):

1. Ask:
   - What is this thing meant to represent?
   - What are its main responsibilities?
   - Should any of its contents actually be separate things?

2. Apply decomposition rules:
   - Split only if the new components would be **independently valuable**
   - Do not create folders for attributes or minor variations
   - Avoid deeply nested trivial folders

3. Identify:
   - Folders that may be **too big or overloaded** conceptually
   - Folders that mix multiple unrelated things
   - Folders that may be better merged (where the split is artificial)

4. Distinguish between:
   - **Conceptual largeness** (too many responsibilities, mixed purposes)
   - **Raw storage size** (lots of assets but conceptually clean)

5. For "fat" folders, ask:
   - Can this be split into 2–3 independently valuable components?
   - Would it make navigation clearer?
   - Would it map better to how I naturally think about the project?

6. **Detect coherence issues** (top-level things that don't belong together):
   - Examine whether top-level folders represent **conceptually related things** or if they're completely unrelated
   - Consider the "dinner table test": if you had to describe this repo in one sentence, would you naturally mention all these things together?
   - Look for signs of forced cohabitation, such as:
     - Completely different domains (e.g., CV generator + trap scanning tool)
     - No shared dependencies, data flows, or conceptual overlap
     - Different stakeholders, use cases, or lifecycles
     - Things that would never be deployed, versioned, or discussed together

   If you detect top-level things that appear **completely unrelated**:

   - Flag this gently: "I notice [X] and [Y] seem to be quite different things. They don't appear to share much conceptually."
   - Ask clarifying questions: "Is there a reason they live together? Do they share infrastructure, data, or workflow?"
   - If they truly seem unrelated, suggest: "You might want to consider splitting these into separate repos. This isn't a hard rule, but it could make each project clearer and easier to work with independently."
   - Make it collaborative: "Of course, there might be good reasons to keep them together (convenience, shared deployment, etc.). What are your thoughts?"

   **Important**: This is a gentle pushback, not a mandate. Some repos intentionally house multiple projects (monorepos, personal collections, experiments). The goal is to surface the question so the user can make an informed decision.

---

## STEP 5 — Propose structural improvements (but do not apply yet)

Claude must:

1. Propose a set of **concrete structural changes**, such as:
   - "Split `app` into `frontend/` and `backend/` because…"
   - "Introduce `docs/` as a separate thing instead of mixed into `src/`"
   - "Move shared components to a `shared/` or `core/` thing"
   - "Consider splitting this repo into two separate repos because [X] and [Y] are completely unrelated"

2. For each suggestion, justify briefly:
   - Why this helps (clarity, navigation, mapping to real things)
   - What each new thing/component would represent

3. Present all suggestions as **optional** and ask:

> "Do you want to capture these structure changes in a plan for later, adjust them, or drop them?"

Claude must not assume automatic restructuring.

---

## STEP 6 — Capture a structure-refactor plan (for existing repos)

If I agree to any changes:

1. Create or update a plan file in the repo root, e.g.:

   `structure-refactor-plan.md`

2. The plan should contain:
   - A short summary of the current issues
   - Proposed structural changes (in clear steps)
   - Any precautions or ordering (e.g., "rename X before updating imports")
   - A checklist I can follow manually or with LLM support

3. Do not actually execute file/folder actions unless I explicitly ask.

---

## STEP 7 — Keep everything aligned with Fractal Specs

While analysing or proposing changes, Claude must:

- Respect the principle:
  **Each folder is a thing; child folders are meaningful components of that thing.**
- Avoid over-splitting into non-valuable fragments
- Avoid under-splitting when a folder is confusingly large
- Ensure the structure mirrors the **real-world composition** of the app/project, not arbitrary technical accidents
- Encourage one spec per thing (`thing-name.md`), with optional plan and research files in each folder

---

## ⚠️ Behaviour Rules for Claude

Claude must:

- Ask questions before proposing structural changes
- Reflect the current tree back to me in plain language
- Challenge me on unclear or overloaded folder purposes
- Treat suggestions as collaborative, not authoritative
- Offer to write or update a root-level plan instead of making silent assumptions
- Never delete or rename anything without explicit user instruction

---

# End of `analyse-structure` Command
