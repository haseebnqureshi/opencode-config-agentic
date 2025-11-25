---
description: Run feature validation with the Product Manager to ensure all user workflows work correctly
---

Perform comprehensive feature validation from a user's perspective.

## Invoke the Product Manager

You MUST invoke the @product-manager agent to:

1. **Check Environment**: Verify servers are running and configured
2. **Validate Features**: Test each user journey works end-to-end
3. **Identify Issues**: Find broken flows, missing features, or UX problems
4. **Coordinate Fixes**: Assign issues to appropriate developer agents

$ARGUMENTS

## After Product Manager Report

Once the Product Manager completes their validation:

### If Issues Found

1. **Review** the prioritized list of issues
2. **Confirm** with user which issues to address
3. **Dispatch** fixes to appropriate agents:
   - Frontend issues: @frontend-senior-dev (for code review) or fix directly
   - Backend issues: @backend-senior-dev (for code review) or fix directly  
   - Runtime errors: @runtime-developer
4. **Re-validate** affected journeys after fixes

### If All Clear

1. **Summarize** the validation results
2. **Note** any warnings or edge cases to monitor
3. **Suggest** next steps for product improvement

## Focus Areas

You can optionally focus on specific areas:

- `/features onboarding` - Test first-time setup flow
- `/features grading` - Test assignment grading workflow
- `/features settings` - Test configuration management
- `/features api` - Test API endpoints directly
- `/features` - Test everything (default)

## Output Format

Present final synthesis as:

```
## FEATURE VALIDATION COMPLETE

### Overall Status
[Pass/Fail/Partial] - X of Y journeys working correctly

### Issues Resolved
| Issue | Agent | Fix Applied |
|-------|-------|-------------|
| ... | ... | ... |

### Remaining Issues
| Issue | Priority | Blocked By |
|-------|----------|------------|
| ... | ... | ... |

### Recommendations
1. [Next improvement to make]
2. [Feature to add]
...
```
