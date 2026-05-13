---
name: create-pr
description: Creates a new GitHub pull request (PR) from the changes in the current branch. Use when the user wants to propose a change to the codebase, open a PR, raise a pull request, or push their work for review.
---

Follow these steps in order:

1. **Determine the base branch.** Do not assume `main` or `master`. In order of preference:
   - If the branch has an upstream, use the repo's default branch: `gh repo view --json defaultBranchRef --jq .defaultBranchRef.name`.
   - Fall back to `git symbolic-ref refs/remotes/origin/HEAD --short` and strip the `origin/` prefix.
   - If both fail, ask the user which base branch the PR targets.

   Use the result (call it `$BASE`) for all subsequent `git` ranges.

2. **Check whether a PR already exists.** Run `gh pr view --json url,state,isDraft` for the current branch. If one exists and is open, share its URL and stop — do not create a duplicate. If it exists but is closed/merged, confirm with the user before proceeding.

3. **Analyse the changes.** Run `git status`, `git branch --show-current`, and `git log "$BASE"..HEAD` to understand the context and specifics. If there are uncommitted changes, use the `commit` skill to commit them.

4. **Find the related issue automatically.** Scan the branch name and `git log "$BASE"..HEAD` output for `#NNN`, `issue-NNN`, or `NNN-` patterns. If exactly one match is found, use it. If multiple or none are found, ask the user: *"I couldn't determine the related GitHub issue — what is the issue number (or 'none')?"*

5. **Draft the PR content.** Using the context gathered in Step 3, draft a concise but complete Pull Request title and body. The body should clearly summarise the "Why" and "What" of the changes.

6. **Link the issue.** If an issue number was identified in Step 4, add `Closes #<ISSUE_NUMBER>` on its own line at the end of the body.

7. **Push the branch.** Determine whether the branch has an upstream with `git rev-parse --abbrev-ref --symbolic-full-name '@{u}'`:
   - No upstream: `git push -u origin HEAD`.
   - Has upstream and is ahead only: `git push`.
   - Has upstream and has diverged (e.g. after rebase): confirm with the user before running `git push --force-with-lease`. Never use plain `--force`.

8. **Create the PR.** Pipe the body via stdin to avoid quoting issues with multi-line content:

   ```sh
   gh pr create --base "$BASE" --title "<DRAFTED_TITLE>" --body-file - <<'EOF'
   <DRAFTED_BODY>
   EOF
   ```

9. **Confirm success.** Once the `gh` command succeeds, output the URL of the newly created Pull Request to the user.
