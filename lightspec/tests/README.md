# Test Specifications

**Read when:** Creating or modifying test specs, or when you need guidance on test structure.

Test specs describe HOW to verify features.

## What Are Test Specs?

Test specifications define:
- **What to test** (scenarios, cases)
- **How to verify** (given/when/then, expected outcomes)
- **Coverage** (primary/alternate flows, exceptions, edges)
- **Testing strategy** (unit/integration/e2e, focus areas)

## When Are Test Specs Required?

Per **R3:** No implementation without corresponding test specifications.

**Why required:** Test specs lock intent and verification before planning/implementation, flush ambiguities early, and provide a stable, low-token contract for LLMs to read across sessions. Plans/tasks inherit clear expected outcomes, preventing scope drift and “vibe coding.” They also give regression-ready scenarios when specs evolve.

**Required for:**
- Code (functions, APIs, components)
- User-facing features
- Business logic and validation rules
- Integration points

**Optional for:**
- Simple documentation-only deliverables
- Research or discovery work
- When acceptance criteria in domain spec suffices

When in doubt, write one.

## How to Use the Template

1. **Copy the template:**
   ```bash
   cp tests/TEST-TEMPLATE.md tests/your-feature-tests.md
   ```

2. **Name consistently with spec:**
   - Spec: `user-login.md`
   - Tests: `user-login-tests.md`

3. **Fill in all sections:**
   - **Feature Under Test**
   - **Test Strategy**
   - **Test Scenarios**
   - **Test Coverage**
   - **Changelog**

4. **[REQUIRED] sections must be included** (framework standard)

## Test Scenario Format

Use **Given/When/Then** pattern:

```markdown
### Scenario: User logs in with valid credentials

**Given:** User has registered account with email "user@example.com"

**When:** User enters valid email and password, clicks "Login"

**Then:** User is redirected to dashboard with active session

**Test Data:**
- Email: user@example.com
- Password: ValidPass123!

**Expected Result:**
- HTTP 200 response
- Session cookie set with 30min expiry
- Redirect to /dashboard
- Welcome message displays user's name
```

## Coverage Checklist

Think in use cases: cover the primary flow, alternate/exception flows, error handling, edge conditions, rules, and ACs.

## Test Specs vs. Test Implementation

**Test Specs (tests/):**
- WHAT to test and WHY
- Scenarios, expected outcomes
- Language-agnostic, tool-agnostic

**Test Implementation (src/tests/ or tests/ in codebase):**
- Actual test code (Jest, pytest, JUnit, etc.)
- Runs in CI/CD pipeline
- Implements scenarios from test specs

Test specs guide implementation, not replace it.

## Tips for Writing Good Test Specs

**Do:** Cover primary + alternate/exception flows, errors, edges; concrete test data; observable results; link to spec; update when changed.

**Don't:** Write implementation code; skip exceptions/edges; assume; forget Changelog.

## For LLMs

Read domain spec; cover all ACs; think errors/edges; test all rules; use concrete data; update Changelog.
