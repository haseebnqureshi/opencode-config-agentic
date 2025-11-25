---
description: Run comprehensive code review with frontend and backend senior developers, then implement approved changes
---

Perform a comprehensive code review focusing on DRY principles and code quality.

## Phase 1: Gather Expert Reviews

You MUST invoke BOTH of these agents in parallel:

1. @frontend-senior-dev - Review all frontend code in `app/` for duplication and DRY violations
2. @backend-senior-dev - Review all backend code in `api/` and `shared/` for duplication and DRY violations

$ARGUMENTS

## Phase 2: Evaluate Findings

After both agents complete their reviews:

1. **Synthesize** their findings into a unified prioritized list sorted by impact
2. **Evaluate** each recommendation for:
   - Technical correctness
   - Risk of introducing bugs
   - Alignment with project patterns
3. **Decide** which recommendations to accept, reject, or defer
4. **Present** your decisions to the user with clear reasoning

## Phase 3: Implementation (After User Approval)

Once the user approves the action plan:

1. **Implement** the approved refactorings one at a time
2. **Test** after each change:
   - Run `npm run build` in the `app/` directory for frontend changes
   - Run `npm run build` in the `api/` directory for backend changes
   - Run any relevant tests
3. **Verify** the refactoring didn't break functionality
4. **Commit** each logical refactoring as a separate commit with a descriptive message

## Decision Framework

Accept recommendations that:
- Eliminate clear duplication (2+ occurrences)
- Have low risk of breaking existing functionality
- Follow established project patterns

Reject or defer recommendations that:
- Require extensive testing not currently available
- Would significantly change APIs used elsewhere
- Have unclear benefit vs. complexity tradeoff

## Output Format

Present your synthesis as:

```
## CODE REVIEW SYNTHESIS

### Approved for Implementation
| Priority | Area | Change | Impact | Risk |
|----------|------|--------|--------|------|
| 1 | Frontend/Backend | Description | ~X lines | Low/Med/High |

### Deferred (Needs Discussion)
- [Item]: [Reason for deferral]

### Rejected
- [Item]: [Reason for rejection]

Ready to proceed with implementation? (waiting for user confirmation)
```
