---
name: post-ship
description: Reconcile a repository checkout after shipping. Use after a release or completed ship workflow when the local checkout must return to main and synchronize with origin/main.
license: MIT
metadata:
  version: "0.1.0"
---

# Post-ship

Return the originating repository checkout to a clean local `main` synchronized with `origin/main` after shipping.

## Procedure

1. Confirm the current directory is the originating repository. Inspect `git status --short --branch`, `git branch --show-current`, and configured remotes. Stop if this is not the expected repository or `origin` is missing.
2. Require a clean worktree. If tracked or untracked changes exist, report their paths and stop. Never stash, discard, stage, or commit changes.
3. Fetch `origin/main`. Stop and report if fetch fails or remote `main` does not exist.
4. Confirm local `main` exists. If current branch is not `main`, switch to local `main` with `git switch main`. Stop if switching fails.
5. Fast-forward local `main` with `git pull --ff-only origin main`. Stop and report if histories diverged or the update fails.
6. Verify current branch is `main`, worktree is clean, and `git rev-parse HEAD` equals `git rev-parse origin/main`. Report each result and stop if any check fails.

Do not push, merge, reset, or delete branches. Report the final branch and commit when all checks pass.
