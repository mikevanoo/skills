---
name: write-a-prd
description: Create a PRD through user interview, codebase exploration, and module design, then submit as a GitHub issue. Use when user wants to write a PRD, create a product requirements document, or plan a new feature.
---

This skill will be invoked when the user wants to create a PRD. You may skip steps if you don't consider them necessary.

1. Ask the user for a long, detailed description of the problem they want to solve and any potential ideas for solutions.

2. Explore the repo to verify their assertions and understand the current state of the codebase.

3. Run a `grill-with-docs` session (or `grill-me` if the project has no `CONTEXT.md` or ADRs to grill against) to stress-test the plan and resolve open branches of the design tree. Do not re-implement the interview procedure here — defer to those skills so the questioning style stays consistent and any future improvements to them flow through automatically.

4. Sketch out the major modules you will need to build or modify to complete the implementation. Actively look for opportunities to extract deep modules that can be tested in isolation.

A deep module (as opposed to a shallow module) is one which encapsulates a lot of functionality in a simple, testable interface which rarely changes.

Check with the user that these modules match their expectations. Check with the user which modules they want tests written for.

**Skip this step if you skipped the codebase exploration in Step 2.** Without grounding in the current code, the sketch becomes speculative architecture that will likely conflict with what already exists. In that case, leave the *Implementation Decisions* section to be filled in later (or by `prd-to-issues`).

5. Once you have a complete understanding of the problem and solution, use the template below to write the PRD. Submit it as a GitHub issue with:
   - Title prefixed with `PRD: `.
   - The `prd` label applied (create it with `gh label create prd` if it doesn't exist). This lets `prd-to-issues` and other downstream skills find PRD issues reliably.
   - A milestone, if the user has one in mind for this work (ask if unclear).

<prd-template>

## Problem Statement

The problem that the user is facing, from the user's perspective.

## Solution

The solution to the problem, from the user's perspective.

## User Stories

A LONG, numbered list of user stories. Each user story should be in the format of:

1. As an <actor>, I want a <feature>, so that <benefit>

<user-story-example>
1. As a mobile bank customer, I want to see balance on my accounts, so that I can make better informed decisions about my spending
</user-story-example>

This list of user stories should be extremely extensive and cover all aspects of the feature.

## Implementation Decisions

A list of implementation decisions that were made. This can include:

- The modules that will be built/modified
- The interfaces of those modules that will be modified
- Technical clarifications from the developer
- Architectural decisions
- Schema changes
- API contracts
- Specific interactions

Do NOT include specific file paths or code snippets. They may end up being outdated very quickly.

## Testing Decisions

A list of testing decisions that were made. Include:

- A description of what makes a good test (only test external behavior, not implementation details)
- Which modules will be tested
- Prior art for the tests (i.e. similar types of tests in the codebase)

## Success Criteria

How we will know this feature is successful once shipped. Prefer observable, falsifiable criteria over vague aspirations. Mix qualitative ("a new user can complete onboarding without help") and quantitative ("p95 checkout latency stays under 800ms", "support tickets about X drop by 50% within 30 days") as appropriate. If a metric implies instrumentation that doesn't yet exist, call that out — the instrumentation work belongs in the issue breakdown.

## Out of Scope

A description of the things that are out of scope for this PRD.

## Further Notes

Any further notes about the feature.

</prd-template>
