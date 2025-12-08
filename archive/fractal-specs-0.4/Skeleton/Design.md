# Skeleton / Design

D01 — Implemented subject anatomy:

```
Subject/
  Requirements.md
  Design.md
  work/
    Plan.md
  Supporting-Files/   (optional)
  child-subject-a/    (optional)
  child-subject-b/    (optional)
```

D02 — Works across all scales (system → feature → UI element).

## Anatomy reference

Example decomposition:

```
Project Documentation (using Fractal Specs)
└─ Product/                           (Subject)
   ├─ Requirements.md                 (Demand: what must remain true)
   ├─ Design.md                       (Supply: what exists now)
   ├─ work/ (optional)
   │   └─ Plan.md                     (Future intent; where the work is done)
   ├─ Supporting-Files/ (optional)    (Collateral referenced by Design)
   ├─ Onboarding/                     (Child subject)
   ├─ Billing/                        (Child subject)
   └─ Admin-Portal/                   (Child subject)
       ├─ Requirements.md
       ├─ Design.md
       └─ work/ (optional)
```

Terms:
- Subject: the folder in focus (microcosm of its parent, macrocosm of its children).
- Parent subject: the folder above this one.
- Child subjects (components/parts): sibling folders inside that carry the same anatomy.
- Siblings: child subjects at the same level.
