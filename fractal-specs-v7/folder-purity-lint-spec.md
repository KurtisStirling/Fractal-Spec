# Folder Purity Lint Specification

## Overview

This document specifies the checks a linting tool must perform to enforce folder purity rules in Fractal Specs v7 projects. The tool validates that each folder adheres to the strict anatomical constraints defined in the Fractal Spec Guide.

## Core Purity Rule

From the Fractal Spec Guide (Section 4):

> A folder may contain ONLY:
> - spec
> - one active plan
> - research
> - files directly describing this thing
> - folders for meaningful components
>
> Nothing else.

## Required Checks

### 1. Spec File Presence

**Rule**: Every folder representing a "thing" must contain exactly one spec file named `{folder-name}.md`.

**Check Logic**:
- For each directory in the tree, verify that a spec file exists with name matching the folder name
- Exception: Root folder may not require a spec if it's a container for multiple top-level things

**Violations**:

**Missing spec file**:
```
Error: Missing spec file
Location: /project/authentication/
Expected: /project/authentication/authentication.md
Message: Every thing folder must contain a spec file named after the folder.
```

**Misnamed spec file**:
```
Error: Misnamed spec file
Location: /project/authentication/auth.md
Expected: /project/authentication/authentication.md
Message: Spec file name must match folder name exactly.
```

---

### 2. Active Plan Limit

**Rule**: Maximum one active plan file (files matching pattern `*-plan.md`) per folder.

**Check Logic**:
- Scan folder for files matching `*-plan.md` pattern
- Archived plans `_*-plan.md` should not count as active
- Count must be ≤ 1

**Violations**:

**Multiple active plans**:
```
Error: Multiple active plans
Location: /project/authentication/
Found:
  - oauth-plan.md
  - ldap-plan.md
Message: Only one active plan allowed per folder. Archive or delete unused plans.
Suggestion: Rename unused plans to _oauth-plan.md or _ldap-plan.md to archive them.
```

---

### 3. Valid File Types

**Rule**: Only permitted file types may exist in a folder.

**Permitted files**:
1. **Spec file**: `{folder-name}.md`
2. **Active plan**: `*-plan.md` (max one)
3. **Research file**: `research.md`
4. **Archived research**: `_research-*.md` (pattern: `_research-YYYY-MM-DD.md`)
5. **Archived plans**: `_*-plan.md`
6. **Direct description files**: Any `.md` file that directly describes/models/explains this thing
7. **Hidden/system files**: Files starting with `.` (e.g., `.gitkeep`)

**Check Logic**:
- Enumerate all files (non-directories) in folder
- Classify each file:
  - Spec: matches folder name + `.md`
  - Active plan: matches `*-plan.md` (not starting with `_`)
  - Research: `research.md`
  - Archived research: `_research-*.md`
  - Archived plan: `_*-plan.md`
  - Hidden/system: starts with `.`
  - Direct description: `.md` extension (catch-all for other markdown)
  - Invalid: anything else
- Flag files that don't match any permitted pattern

**Violations**:

**Non-markdown file**:
```
Error: Invalid file type
Location: /project/authentication/diagram.png
Message: Only markdown files and hidden system files are permitted in thing folders.
Suggestion: Move binary assets to a documentation folder or embed as external references.
```

**Executable or code file**:
```
Error: Invalid file type
Location: /project/authentication/helper.js
Message: Code files should not exist in spec folders.
Suggestion: This folder describes a thing; actual implementation belongs elsewhere.
```

**Multiple research files**:
```
Warning: Multiple research files
Location: /project/authentication/
Found:
  - research.md
  - notes.md
Message: Consider consolidating research into research.md or archiving older files.
```

---

### 4. Component Folder Detection

**Rule**: All subdirectories must be meaningful component folders following the same anatomy.

**Check Logic**:
- Recursively validate all subdirectories
- Each subdirectory should pass all folder purity checks
- Flag directories that appear to be organizational containers rather than components

**Violations**:

**Organizational subfolder anti-pattern**:
```
Warning: Potential organizational anti-pattern
Location: /project/authentication/docs/
Message: Subdirectories should represent meaningful components, not organizational buckets.
Suggestion: If 'docs' contains files describing authentication, move them up to /project/authentication/.
```

**Empty component folder**:
```
Error: Empty component folder
Location: /project/authentication/oauth/
Message: Component folders must contain at least a spec file (oauth.md).
```

---

## Additional Validation Rules

### 5. Archived File Naming Convention

**Rule**: Archived files must follow the `_` prefix convention.

**Check Logic**:
- Archived research: must match `_research-YYYY-MM-DD.md` pattern
- Archived plans: must start with `_` and end with `-plan.md`

**Violations**:

**Improperly archived research**:
```
Error: Invalid archive naming
Location: /project/authentication/old-research.md
Expected pattern: _research-YYYY-MM-DD.md
Message: Archived research must use the _research-{date} naming convention.
```

---

### 6. Spec File Content Validation (Optional/Future)

**Rule**: Spec files should contain Need, Design, and Change Log sections.

**Check Logic** (low priority):
- Parse spec markdown
- Verify presence of key sections
- This is a "soft" check for completeness, not strict purity

**Violations**:

**Missing sections**:
```
Warning: Incomplete spec structure
Location: /project/authentication/authentication.md
Missing sections: Design, Change Log
Message: Specs should contain Need, Design, and Change Log sections.
```

---

## Lint Tool Behavior

### Exit Codes

- `0`: No violations
- `1`: Errors found (purity violations)
- `2`: Warnings only (suggestions, not strict violations)

### Output Format

**Success**:
```
✓ Folder purity check passed
  Scanned: 47 folders
  Files validated: 153
```

**Errors**:
```
✗ Folder purity violations found

ERROR: Missing spec file
  Location: /project/authentication/
  Expected: authentication.md

ERROR: Multiple active plans
  Location: /project/database/
  Found: schema-plan.md, migration-plan.md
  Suggestion: Archive unused plans with _ prefix

2 errors, 0 warnings
```

### Command-Line Options

Suggested flags for the tool:

- `--strict`: Treat warnings as errors
- `--path <dir>`: Specify root directory to check (default: current directory)
- `--recursive`: Check all subdirectories (default: true)
- `--ignore <pattern>`: Ignore specific paths (e.g., `--ignore node_modules,dist`)
- `--fix`: Auto-fix certain violations where safe (e.g., renaming misnamed specs)
- `--json`: Output results in JSON format for CI integration

---

## Implementation Notes

### Detection Heuristics

1. **Root folder identification**: The tool should identify the root of the Fractal Specs tree, possibly by:
   - Looking for a `.fractal-specs` marker file
   - Command-line argument specifying the root
   - Scanning upward from current directory

2. **Spec file matching**: Use exact string match: `{folder_name}.md`

3. **Plan file matching**: Regex pattern: `^[^_].*-plan\.md$`

4. **Archived file matching**:
   - Plans: `^_.*-plan\.md$`
   - Research: `^_research-\d{4}-\d{2}-\d{2}\.md$`

5. **Hidden files**: `^\.`

### Edge Cases

1. **Symlinks**: Should the tool follow symlinks? Recommendation: No, flag as violation
2. **Case sensitivity**: Enforce case-sensitive matching on all platforms
3. **Hidden directories**: Skip directories starting with `.` (e.g., `.git`)
4. **Empty directories**: Flag as warnings unless they contain a spec file

---

## Extensibility

Future enhancements could include:

1. **Frontmatter validation**: Check `used-by` fields for horizontal dependencies
2. **Cross-reference validation**: Verify referenced components actually exist
3. **Plan lifecycle checks**: Detect stale plans (last modified > N days ago)
4. **Spec completeness scoring**: Rate spec quality based on section presence/depth
5. **Component depth warnings**: Flag excessive nesting (> 5 levels deep)

---

## References

- Fractal Spec Guide v7 - Section 4 (Folder Purity)
- Fractal Spec Guide v7 - Section 2 (Anatomy of Every Folder)
- Fractal Spec Guide v7 - Section 3 (What Goes Where)
