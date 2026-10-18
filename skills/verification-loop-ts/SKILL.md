---
name: verification-loop
description: A comprehensive verification system for Claude Code sessions. Use after completing a feature, before creating a PR, after refactoring, or when you want to ensure quality gates pass.
---

## Verification Phases

### Phase 1: Build Verification
```bash
npm run build 2>&1 | tail -20
# OR
pnpm build 2>&1 | tail -20
```
If build fails, STOP and fix before continuing.

### Phase 2: Type Check
```bash
# TypeScript projects
npx tsc --noEmit 2>&1 | head -30

# Python projects
pyright . 2>&1 | head -30
```
Report all type errors. Fix critical ones before continuing.

### Phase 3: Lint Check
```bash
# JavaScript/TypeScript
npm run lint 2>&1 | head -30

# Python
ruff check . 2>&1 | head -30
```

### Phase 4: Test Suite
```bash
npm run test -- --coverage 2>&1 | tail -50
# Target: 80% minimum coverage
```
Report:
- Total tests: X
- Passed: X
- Failed: X
- Coverage: X%

### Phase 5: Security Scan
```bash
# Check for secrets
grep -rn "sk-" --include="*.ts" --include="*.js" . 2>/dev/null | head -10
grep -rn "api_key" --include="*.ts" --include="*.js" . 2>/dev/null | head -10

# Check for console.log
grep -rn "console.log" --include="*.ts" --include="*.tsx" src/ 2>/dev/null | head -10
```

### Phase 6: Diff Review
```bash
git diff --stat
git diff HEAD~1 --name-only
```
Review each changed file for:
- Unintended changes
- Missing error handling
- Potential edge cases

## Output Format

```
VERIFICATION REPORT
==================

Build:     [PASS/FAIL]
Types:     [PASS/FAIL] (X errors)
Lint:      [PASS/FAIL] (X warnings)
Tests:     [PASS/FAIL] (X/Y passed, Z% coverage)
Security:  [PASS/FAIL] (X issues)
Diff:      [X files changed]

Overall:   [READY/NOT READY] for PR

Issues to Fix:
1. ...
2. ...
```

## Continuous Mode

For long sessions, run verification every 15 minutes or after major changes:
- After completing each function
- After finishing a component
- Before moving to next task

## Integration with Hooks

This skill complements PostToolUse hooks but provides deeper verification. Hooks catch issues immediately; this skill provides comprehensive review.

## Arguments

$ARGUMENTS can be:
- quick - Only build + types
- full - All phases (default)
- pre-pr - Full checks with extra security scrutiny
