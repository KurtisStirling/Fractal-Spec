# Decision Trees

## "What goes where?"

```
                                ┌────────────────────────────┐
                                │  START: I have content     │
                                │  related to this subject.  │
                                └───────────────┬────────────┘
                                                │
                     ┌──────────────────────────┴──────────────────────────┐
                     │                                                     │
     ┌───────────────▼───────────────┐                     ┌───────────────▼───────────────┐
     │Q1: Is it only historical,     │                     │Q2: Is it raw, noisy,          │
     │obsolete, or no longer true?   │                     │undistilled, or mixed-topic    │
     │(e.g. past plans, expired      │                     │input? (e.g. meeting notes,    │
     │constraints, old project scope)│                     │dumped tickets, unrefined text)│
     └───────────────┬───────────────┘                     └───────────────┬───────────────┘
                     │Yes                                              Yes │
                     ▼                                                   ▼
         ┌───────────────────────┐                         ┌──────────────────────────┐
         │ OFF-RAMP: Archive or  │                         │ Put in work/ as          │
         │ keep outside Fractal  │                         │ Research/Scratch input:  │
         │ Specs skeleton.       │                         │   work/Research.md       │
         └───────────────────────┘                         │   work/Scratch.md        │
                     │                                     └───────────────┬──────────┘
                     │No                                                  No │
                     └───────────────────────────────────────────────────────┘
                                                │
                                                ▼
                            ┌───────────────────┴────────────────────┐
                            │Q3: Is it describing what SHOULD be     │
                            │true, independent of implementation?    │
                            │(needs, rules, constraints, behaviour,  │
                            │reasons, expectations, outcomes)        │
                            └───────────────────┬────────────────────┘
                                                │Yes
                                                ▼
                                  ┌──────────────────────────┐
                                  │ Put in Requirements.md   │
                                  │ (Demand: what must       │
                                  │ remain true now)         │
                                  └───────────┬──────────────┘
                                              │No
                                              ▼
                          ┌───────────────────┴─────────────────────┐
                          │Q4: Is it describing what IS currently   │
                          │true about this subject?                 │
                          │(current behaviour, structure, rules,    │
                          │decisions, models at a human-readable    │
                          │level – not line-by-line code)           │
                          └───────────────────┬─────────────────────┘
                                              │Yes
                                              ▼
                                ┌───────────────────────────────┐
                                │ Put in Design.md              │
                                │ (Supply: how the subject      │
                                │ currently meets demand)       │
                                └───────────────┬───────────────┘
                                                │No
                                                ▼
                      ┌─────────────────────────┴────────────────────────┐
                      │Q5: Is it about future work or change?            │
                      │(intent, options, decisions-to-make, priorities,  │
                      │tasks, roadmaps, sequencing, "what we plan to do")│
                      └─────────────────────────┬────────────────────────┘
                                                │Yes
                                                ▼
                              ┌──────────────────────────────────────┐
                              │ Put in work/Plan.md                 │
                              │ (Work: future intent; the plan at   │
                              │ this subject is where the work is   │
                              │ done)                               │
                              └───────────────────┬──────────────────┘
                                                  │No
                                                  ▼
                     ┌────────────────────────────┴──────────────────────────┐
                     │Q6: Does it primarily help explain or illustrate       │
                     │the subject, without itself being demand/supply/plan?  │
                     │(diagrams, UI mocks, data models, examples, references)│
                     └────────────────────────────┬──────────────────────────┘
                                                  │Yes
                                                  ▼
                                    ┌──────────────────────────────┐
                                    │ Put in Supporting-Files/     │
                                    │ (Collateral: supporting      │
                                    │ material the subject refers  │
                                    │ to, but is not itself truth) │
                                    └────────────────┬─────────────┘
                                                     │No
                                                     ▼
         ┌───────────────────────────────────────────┴────────────────────────────────┐
         │Q7: Does it actually describe something that deserves its OWN subject?       │
         │(a distinct area with its own demands, supply, and work: a department,      │
         │product, service, subsystem, team, or module)                               │
         └───────────────────────────────┬────────────────────────────────────────────┘
                                         │Yes
                                         ▼
                         ┌────────────────────────────────────────────┐
                         │ Create a new child subject (sibling folder)│
                         │ and give THAT new subject its own:         │
                         │   Requirements.md, Design.md, work/Plan.md │
                         └───────────────────────────────┬────────────┘
                                                         │No
                                                         ▼
                         ┌────────────────────────────────────────────────┐
                         │ OFF-RAMP: This content likely belongs in code, │
                         │ tooling (e.g. Jira, Git), or an external/      │
                         │ legacy area, not inside the Fractal Specs      │
                         │ skeleton for this subject.                     │
                         └────────────────────────────────────────────────┘
```
