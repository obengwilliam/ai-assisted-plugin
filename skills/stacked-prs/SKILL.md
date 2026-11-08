---
name: stacked-prs
description: "Use before writing code for a change that spans more than one concern or layer (refactor plus feature, backend plus UI, schema plus logic), or whose diff a reviewer could not read in one sitting. Decides whether to ship it as a stack of narrow PRs and hands the commands to gh-stack. Skip single-concern changes."
---

# Stacked PRs

Prefer several narrow PRs to one large one. Decide before you write the first file.

## Stack when any of these is true
- The change has more than one concern (refactor, then feature, then UI).
- A layer could be reverted without the others.
- A reviewer would need more than one sitting to read the diff.

## Ship one PR when
- It is a small fix or a single concern.
- The layers cannot build and pass tests on their own.

## Rules
1. Tell the user the layer plan before coding: one line per PR, in merge order,
   with enabling work (refactors, schema, shared helpers) at the bottom.
2. Every PR must build and pass tests by itself.
3. The base is the branch this repo's PRs target: the default branch unless the repo's docs say otherwise.
4. Unrelated or independent work gets its own PR or stack. A stack is a linear chain, so it never branches.
5. For commands, use the `gh-stack` skill. If `gh stack` is missing, or a command exits 9
   (stacked PRs not enabled on the repo), fall back to a plain chain of branches,
   each PR opened with `--base <branch below>`.
6. `submit` and `push` publish every branch in the stack. Get the user's approval first, as for any push.
