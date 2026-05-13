# Agent Skills
My personal collection of AI agent skills.

Lifted directly from, or heavily inspired by, https://github.com/mattpocock/skills and https://github.com/haletothewood.

## Typical workflow

The skills are designed to chain together across the life of a feature:

1. **`grill-with-docs`** — stress-test the idea against the existing domain model and update `CONTEXT.md` / ADRs (or `grill-me` for general use cases or where you don't have existing `CONTEXT.md` / ADRs).
2. **`write-a-prd`** — turn the sharpened idea into a PRD filed as a GitHub issue.
3. **`prd-to-issues`** — split that PRD into independently-grabbable vertical-slice issues.
4. **`triage`** — review and shape incoming issues so an agent can pick them up unaided.
5. **`tdd`** — implement a slice red-green-refactor.
6. **`commit`** → **`create-pr`** — land the work and open a PR linked to the issue.

Use any subset on its own — `diagnose`, `improve-codebase-architecture`, `improve-prompt`, and `prove-it-to-me` are independent of the chain.

## Planning & Design

These skills help you think through problems before writing code.

- **grill-me** — Get relentlessly interviewed about a plan or design until every branch of the decision tree is resolved.

  ```
  npx skills@latest add mikevanoo/skills/grill-me
  ```


- **grill-with-docs** — Grilling session that challenges your plan against the existing domain model, sharpens terminology, and updates documentation.

  ```
  npx skills@latest add mikevanoo/skills/grill-with-docs
  ```


- **write-a-prd** — Create a PRD through an interactive interview, codebase exploration, and module design. Filed as a GitHub issue.

  ```
  npx skills@latest add mikevanoo/skills/write-a-prd
  ```


- **prd-to-issues** — Break a PRD into independently-grabbable GitHub issues using vertical slices.

  ```
  npx skills@latest add mikevanoo/skills/prd-to-issues
  ```


## Development

These skills help you write, refactor, and fix code.

- **commit** — Commit the pending changes in the current branch with a descriptive commit message.

  ```
  npx skills@latest add mikevanoo/skills/commit
  ```

- **create-pr** — Create a new GitHub pull request (PR) for the current branch.

  ```
  npx skills@latest add mikevanoo/skills/create-pr
  ```


- **diagnose** — Disciplined diagnosis loop for hard bugs and performance regressions. Reproduce → minimise → hypothesise → instrument → fix → regression-test.

  ```
  npx skills@latest add mikevanoo/skills/diagnose
  ```
  

- **improve-codebase-architecture** — Explore a codebase for architectural improvement opportunities, focusing on deepening shallow modules and improving testability.

  ```
  npx skills@latest add mikevanoo/skills/improve-codebase-architecture
  ```
  

- **tdd** — Test-driven development with a red-green-refactor loop. Builds features or fixes bugs one vertical slice at a time.

  ```
  npx skills@latest add mikevanoo/skills/tdd
  ```

- **triage** — Triage issues through a state machine driven by triage roles..

  ```
  npx skills@latest add mikevanoo/skills/triage
  ```

## Interrogation

These skills help you interrogate and validate agent responses.

- **prove-it-to-me** — Ask the agent to prove, empirically, that its previous response is true. 

  ```
  npx skills@latest add mikevanoo/skills/prove-it-to-me
  ```

## Prompt Engineering

These skills help you craft better prompts.

- **improve-prompt** — Refine and improve an existing AI chat prompt so it is better structured and worded for a higher-quality response.

  ```
  npx skills@latest add mikevanoo/skills/improve-prompt
  ```

## Contributing

This repo ships a pre-commit hook that blocks commits containing files in skill subfolders with CRLF line endings, a UTF-8 BOM, or invalid UTF-8. Enable it once after cloning:

```
git config core.hooksPath .githooks
```

The hook lives at [.githooks/pre-commit](.githooks/pre-commit) and runs on Linux, macOS, and Windows (via Git Bash).
