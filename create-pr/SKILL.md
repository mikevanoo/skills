---
name: create-pr
description: Creates a new GitHub pull request (PR) from the changes in the current branch. Use when the user wants to propose a change to the codebase.
---

Follow these steps in order:

1. **Analyze the Changes:** Run `git status`, `git branch --show-current`, and `git log main..HEAD` (or `master..HEAD`) to understand the context and specifics of the changes made in the current branch. If there are uncommitted changes, use the `commit` skill to commit them.

2. **Prompt the User:** Pause your execution and ask the user: *"What is the related GitHub issue number for this PR?"* This is optional. There may not be a related issue.

3. **Draft the PR Content:** Using the context gathered in Step 1, draft a concise but complete Pull Request title and body. The body should clearly summarise the "Why" and "What" of the changes.

4. **Link the Issue:** At the very end of the PR body, if the user gave an issue number, add a new line with the exact text: `Closes issue #<ISSUE_NUMBER>` (replacing `<ISSUE_NUMBER>` with the input received in Step 2).

5. **Push the Branch:** Ensure the current branch is pushed to the remote repository. Run:
   `git push -u origin HEAD`

6. **Create the PR:** Use the GitHub CLI to open the pull request automatically. Run:
   `gh pr create --title "<DRAFTED_TITLE>" --body "<DRAFTED_BODY>"`

7. **Confirm Success:** Once the `gh` command succeeds, output the URL of the newly created Pull Request to the user.