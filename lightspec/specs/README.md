# Specifications

**Read when:** Creating or modifying specs, or when you need guidance on spec structure.

Specs capture the "what" and "why" of features.

## What Are Specifications?

Specifications capture:
- **What** needs to be built (requirements, capabilities)
- **Why** it matters (purpose, value proposition)
- **Constraints** that govern behavior (rules, validation)
- **Success criteria** (how we know it works)

They preserve intent that code alone cannot.

## When to Create a Spec

Create when:
- Starting a new feature or capability
- Requirements are complex enough to need documentation
- Many people need to understand what's being built
- You need to track how requirements evolved

## How to Use the Template

1. **Copy the template:**
   ```bash
   cp specs/SPEC-TEMPLATE.md specs/your-feature.md
   ```

2. **Fill in all sections:**
   - **Purpose**
   - **Requirements (MoSCoW)**
   - **Rules**
   - **Use Cases (with flows) (optional)**
   - **Acceptance Criteria**
   - **Changelog (v1+)**

3. **[REQUIRED] sections must be included** (framework standard)

4. **Reference related artifacts:**
   - Global rules: `(per R4+)`
   - Other specs: `#42`
   - Tests: Link to corresponding test spec

## Example: Complete Specification

```markdown
---
id: S12
version: 1
status: active
created: 2025-01-10
last_updated: 2025-01-10
user(s): end users
---

# User Login

## Purpose

Enable users to securely authenticate using email and password to access their personalized dashboard and account features.

## Requirements

#### Must have:

- Email and password input fields
- "Login" button that validates and authenticates
- Redirect to dashboard on successful login
- Error message display for invalid credentials
- Session creation with 30min timeout

#### Should have:

- "Remember me" checkbox for extended sessions (30 days)
- Password visibility toggle
- "Forgot password?" link

#### Nice to have:

- Social login options (Google, GitHub)
- Biometric authentication on supported devices

## Use Cases (with flows)

**Use Case A: Standard login**
1. User navigates to /login
2. User enters email and password
3. User clicks "Login" button
4. System validates credentials against database
5. On success: redirect to /dashboard with session cookie
6. On failure: display error message, remain on login page

**Use Case B: Remember me**
1. User checks "Remember me"
2. User logs in successfully
3. Session persists for 30 days

## Rules

- Email must be valid format (per R4)
- Password minimum 12 characters with uppercase, number, symbol (per R5)
- Maximum 5 failed attempts per hour per IP (per R6)
- Session expires after 30min inactivity
- HTTPS required for all auth endpoints

## Acceptance Criteria

- [ ] User can log in with valid email/password
- [ ] Invalid credentials show clear error message
- [ ] Successful login redirects to dashboard with active session
- [ ] Session expires after 30min inactivity
- [ ] Rate limiting prevents brute force attacks (5 attempts/hour)
- [ ] Password requirements enforced (R5)
- [ ] "Remember me" extends session to 30 days

## Changelog

### v1 - 2025-01-10

**Changes:** Initial specification created

**Rationale:** Users need secure authentication to access personalized features and account management

**Notes:** Requested by Product team. Must comply with R5 (password security) and R6 (rate limiting). Related to #S13 (Password Reset) and #S14 (User Registration).
```

## Users Field and Spec References

**`user(s):` field (optional):** Declares who/what this spec is for. Can be end users, roles ("managers", "end users"), or other spec IDs (S1, S5, S6).

Specs serving other specs are reusable patterns - reference them instead of restating.

**Examples:**
```yaml
user(s): end users              # Feature spec
user(s): managers, admins       # Role-specific feature
user(s): S1, S5, S6            # Shared pattern/model used by other specs
```

## Specifications vs. Tests vs. Technical Docs

**Specifications (specs/):**
- WHAT to build and WHY
- Requirements, rules, acceptance criteria
- Outcome-focused

**Test Specs (tests/):**
- HOW to verify it works
- Test scenarios, coverage
- Validation-focused

**Technical Docs (technical/):**
- HOW to implement
- Patterns, architecture decisions, APIs
- Implementation-focused

## Tips for Writing Good Specs

**Do:** Focus WHAT/WHY; be specific/testable; separate requirements vs rules; reference global rules; track changes.

**Don't:** Include implementation; assume; skip Changelog; bloat.

**Use cases:** Include multiple use cases when they matter; keep each flow concise and link ACs/tests to them.

---

## Evolving Specifications

Specifications naturally evolve as you learn more, requirements change, or priorities shift. The framework uses edit-in-place with version tracking.

**Process:**

Edit; bump version; update Changelog; update tests; add tasks; implement; mark version.

**Changelog example for v2:**

```markdown
## Changelog

### v2 - 2025-06-15

**Changes:** Added "Remember me" checkbox requirement; Removed SMS verification (replaced with email-only)

**Rationale:** User feedback requested persistent sessions. SMS costs prohibitive for current user volume.

**Notes:** See DECISIONS.md D42 for authentication strategy decision. Updated test spec accordingly.

### v1 - 2025-01-10

**Changes:** Initial specification created

**Rationale:** Users need secure authentication to access personalized features

**Notes:** Requested by Product team. Must comply with R5 (security standards).
```

The Changelog provides complete evolution history. Single spec file remains the source of truth.

---

## For LLMs

Read template; ask if unclear; separate requirements vs rules; ensure ACs testable; update Changelog when modifying.
