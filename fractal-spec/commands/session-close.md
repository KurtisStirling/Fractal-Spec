# session-close (Lightspec)

Purpose-built, lightweight session wrap-up for Lightspec projects.

## 0) Git presence (skip if absent)
- If `git rev-parse --is-inside-work-tree` fails → skip git steps.
- Else `git status --porcelain` to see if there’s work to close.

## 1) Session recap (brief)
- What changed/created (files)?
- Decisions made?
- Unfinished work / blockers?

## 2) Framework alignment
- Specs: updated content? version bumped? changelog entry?
- Tests: updated to match specs? scenarios/coverage still valid?
- Technical: any new patterns/ADRs to capture?
- Roadmap: tasks added/updated? move done work to `roadmap/done/` if applicable.

## 3) Rules/Goals/Decisions
- Any new global rules? → add R13+ in `constitution/RULES.md`.
- Any mission/objective changes? → update `constitution/GOALS.md`.
- Any cross-cutting choices? → add to `constitution/DECISIONS.md`.

## 4) Sanity checks
- Acceptance criteria satisfied? edge cases covered?
- Naming matches conventions (kebab-case, R# refs)?
- Token terseness ok (no bloat)?

## 5) Optional tests
- If code changed, ask whether to run tests; run if approved.

## 6) Git workflow (only if git present + work to close)
- Show status; confirm files to include.
- Stage (`git add …`) → confirm.
- Propose commit message (conventional commits).
- Commit only after approval.
- Push only after approval (if remote configured).

## 7) Final confirmation
- Recap what was committed (or noted as deferred).
- Note any follow-ups to add to ROADMAP or DECISIONS.
- Ask if anything else to document before ending session.
