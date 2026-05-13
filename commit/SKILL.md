---
name: commit
description: Commit the pending changes in the current branch. Use when a user wants to commit their changes.
---

Create a complete but concise commit message describing the pending changes in the current branch. Then commit the changes.

## Procedure

1. Run `git status` and `git diff` (plus `git diff --staged` if anything is already staged) to see exactly what will be committed. Read the diff before drafting the message — don't infer changes from filenames alone. If there is nothing to commit, say so and stop; do not create an empty commit.
2. Run `git log -n 10 --format=%s%n%b` to sample the repo's commit style (prefix, tense, body conventions) before drafting your message.
3. If both staged and unstaged changes exist, ask the user which set to commit rather than guessing. Don't blanket `git add -A`; stage files by name. If the diff covers unrelated concerns (e.g. bugfix + unrelated refactor), propose splitting into separate commits.
4. Refuse to stage or commit files that likely contain secrets (`.env`, `*.pem`, `id_rsa`, `credentials.json`, `*.key`, anything under a `secrets/` path). If the user explicitly insists, warn first and confirm.
5. If a pre-commit hook fails, the commit did not happen. Fix the underlying issue, re-stage, and create a **new** commit. Never use `--amend` to recover from a failed hook — it rewrites the previous (already-good) commit and can destroy work. Never bypass hooks with `--no-verify` unless the user explicitly asks.

## Commit message

Always include a body paragraph, not just a summary title.
Focus on the "why" and key design decisions rather than listing files.
Match the repo's existing commit style for prefix/format (sampled in step 2), but always write a body paragraph explaining the why.
