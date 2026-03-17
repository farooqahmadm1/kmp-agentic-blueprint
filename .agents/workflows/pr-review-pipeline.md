---
description: Automated pipeline to run when a Pull Request is opened.
---

# PR Review Pipeline Workflow

When invoked to review a newly opened PR, Gemini should execute these steps sequentially to ensure code quality before human review.

1. **Analyze Technical Debt**:
   - Run the `analyze-tech-debt` skill on the files modified in this PR.
// turbo-all
2. **Run Linting & Formatting Check**:
   - Execute formatting commands (e.g., `./gradlew ktlintCheck`).
   - Note any failures or style violations.

3. **Execute Test Suite**:
   - Run all affected unit and integration tests based on the PR changes (e.g., `./gradlew test`).

4. **Verify Architectural compliance**:
   - Scan the diffs to ensure no SOLID principles or Separation of Concerns are violated (as defined in `GEMINI.md`).
   - Specifically check that no business logic exists within UI Views.

5. **Generate Report**:
   - Compile the findings from the steps above into a single markdown summary.
   - Use `notify_user` or output the report directly so it can be posted as a comment on the PR.
