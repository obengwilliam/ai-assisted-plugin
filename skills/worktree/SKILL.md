---
name: worktree
description: Create, list, switch, and delete git worktrees. Use when the user says "worktree", "wt", "new branch", "gwa", "gwd", "gwl", wants to work on a feature in isolation, or needs to manage parallel working directories.
---

# Git Worktree Management

Wraps the user's `git wt` aliases for worktree operations.

## Available Commands

| Alias | Description |
|-------|-------------|
| `gwl` | List all worktrees |
| `gwa <branch> [start-point]` | Create/switch worktree (also creates `.envrc` with `CLAUDE_CODE_TASK_LIST_ID`) |
| `gwd <branch>` | Safe delete worktree + branch |
| `gwD <branch>` | Force delete worktree + branch |
| `gwac <branch>` | Create with `.env*` files copied |
| `gwn <branch>` | Create but stay in current dir |
| `gwall <branch>` | Create with ignored + untracked files copied |

## Usage

Based on `$ARGUMENTS`, perform the appropriate action:

### No arguments or "list"
```bash
gwl
```
Show the worktree list to the user.

### "create <branch>" or "add <branch>" or just "<branch-name>"

**Before creating**, always ask the user:
> "Do you want to branch off `main` (default) or a different base branch?"

- If the user says yes / confirms default → use `main` (or `master` if that's the default branch)
- If the user specifies a different branch → use that as the start-point

```bash
# Default: checkout from main/master
gwa <branch> main

# From a user-specified base branch
gwa <branch> <start-point>
```

### "delete <branch>" or "remove <branch>"
```bash
# Safe delete (default)
gwd <branch>

# Force delete only if user explicitly asks
gwD <branch>
```
**Always confirm with the user before force-deleting.**

### "copy <branch>" (with env/untracked files)
```bash
gwall <branch>
```

## Important Notes

- The default branch (main/master) is protected from deletion.
- Worktrees are stored in the directory configured by `wt.basedir` (default: `../{gitroot}-wt`).
- `gwa` automatically creates `.envrc` with `CLAUDE_CODE_TASK_LIST_ID` set to the branch name for Claude Code task tracking.
- Always show the user the worktree list after create/delete operations so they can see the result.
- When deleting, prefer safe delete (`gwd`) unless the user explicitly requests force (`gwD`).
