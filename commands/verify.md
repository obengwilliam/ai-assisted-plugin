---
description: Run comprehensive verification on current codebase state
---

Execute verification in this exact order:

## Build Check
- Run the build command for this project
- If it fails, report errors and STOP

## Type Check
- Run TypeScript/type checker
- Report all errors with file:line

## Lint Check
- Run linter
- Report warnings and errors

## Test Suite
- Run all tests
- Report pass/fail count
- Report coverage percentage

## Console.log Audit
- Search for console.log in source files
- Report locations

## Git Status
- Show uncommitted changes
- Show files modified since last commit

## Output
Produce a concise verification report:

```
VERIFICATION: [PASS/FAIL]

Build:    [OK/FAIL]
Types:    [OK/X errors]
Lint:     [OK/X issues]
Tests:    [X/Y passed, Z% coverage]
Secrets:  [OK/X found]
Logs:     [OK/X console.logs]

Ready for PR: [YES/NO]
```

If any critical issues, list them with fix suggestions.

## Arguments
$ARGUMENTS can be:
- quick - Only build + types
- full - All checks (default)
- pre-commit - Checks relevant for commits
- pre-pr - Full checks plus security scan
