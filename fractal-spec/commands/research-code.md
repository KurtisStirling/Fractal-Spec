# research-code Command (Fractal Spec + Sub-Agents)

A command for Claude to investigate code and document **what exists today** using parallel sub-agents.  
Claude must act purely as a **documentarian**, not a critic or designer.

Research is temporary and should output to `<thing>/research.md`.

---

# 🧠 Purpose

Use this command to understand **current behaviour, structure, flows, and dependencies** so planning and design updates can be accurate.  
Claude documents *what exists*, not *what should exist*.

Forbidden during this command:
- critique  
- suggestions or improvements  
- redesign  
- debugging  
- root cause analysis  

---

# 🟦 When invoked, Claude replies:

```
I'm ready to research the codebase. What would you like to understand?
```

Then Claude waits.

---

# 🔷 Rules (Terse, High-Value)

- Describe **only actual present behaviour**.  
- Read all referenced files **fully** before sub-tasks.  
- Ask clarifying questions before exploring widely.  
- Spawn sub-agents for parallel exploration.  
- Synthesise findings—never dump raw outputs.  
- Write results to `research.md` in the correct folder.  
- Remind the user that research is temporary.

---

# 🔶 Research Steps

## STEP 1 — Clarify the research question
Ask:
- What exactly should be understood?
- Is the focus behaviour, flow, architecture, or interactions?
- Any specific files or components to start from?

Do not assume.

---

## STEP 2 — Read any mentioned files fully
If named, read them in full and extract:
- responsibilities  
- behaviour  
- interactions  
- state/data patterns  
- flows or branching

---

## STEP 3 — Break the research into sub-problems
Claude identifies:
- relevant modules/components  
- flows to trace  
- interactions needing mapping  
- data transformations  
- boundary points  

Claude summarises the intended plan before proceeding.

---

## STEP 4 — Spawn parallel sub-agents

Use sub-agents to:

### 📁 Locate code (locator agents)
- Identify files, folders, modules involved.

### 🔍 Analyse code (analyzer agents)
- Describe behaviour, purpose, interactions.
- Map control flow, data flow, responsibilities.

### 🔗 Trace flows (flow agents)
- Request → handler → service → DB → response  
- Event → consumer chains  
- UI → state → backend interactions  

Sub-agents must **ONLY document**, not critique.

---

## STEP 5 — Wait for all agents and synthesise

Claude must:
- collect all results  
- unify and clean them  
- remove overlaps  
- describe interactions between components  
- map real architecture and flows  

Never present raw sub-agent output directly.

---

## STEP 6 — Produce `research.md`

Write content as:

```
# Research: [Topic]

## Summary
High-level explanation of what exists.

## Findings
### Area / Component 1
- What it does
- How it behaves
- Key functions/classes
- Interactions
- File paths

### Area / Component 2
...

## Flows (if relevant)
Describe actual request/response, events, or UI → state → backend flows.

## Data (optional)
Important structures, persistence, transformations.

## Evidence (brief)
- path/to/file — behaviour summary
- another/file — key logic

## Notes
Temporary observations for planning context.
```

---

## STEP 7 — Ask whether to create/update a plan

```
Would you like me to update or create a plan based on these findings?
```

If yes → move to planning.  
If no → stop.

---

## STEP 8 — Remind research is temporary

Claude adds:

```
(Research is temporary. Promote relevant findings into the Design section later or delete when done.)
```

---

# ⚠️ Behaviour Requirements for Claude

Claude must:
- NEVER critique or propose improvements  
- NEVER infer intention or ideal behaviour  
- NEVER refactor or redesign  
- ALWAYS use sub-agents where helpful  
- ALWAYS ask clarifying questions  
- ALWAYS produce a synthesised, coherent document  
- ALWAYS document “what IS,” not “what SHOULD BE”

Claude is a **neutral documentarian**, not a reviewer.

---

# End of `research-code` Command
