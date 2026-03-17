---
name: write-tests
description: Generate and execute unit, integration, or end-to-end tests.
---

# Testing Skill

Use this skill ensuring the newly implemented feature works correctly and does not introduce regressions. 

## Objectives
- Achieve high code coverage for new logic.
- Verify edge cases and error handling.
- Ensure the build is green before finalizing a feature.

## Step-by-Step Instructions

1. **Identify the Target**:
   - Determine which files were recently modified or created.
   - Note the exported functions, classes, or API endpoints that require coverage.

2. **Locate the Test Suite**:
   - Search for existing tests to match the project's testing framework (e.g., Jest, PyTest, Go test).
   - Match the naming conventions (e.g., `feature.spec.ts` or `test_feature.py`).

3. **Draft the Tests**:
   - **Happy Path**: Write tests that verify the expected behavior works perfectly.
   - **Edge Cases**: Pass empty arrays, null values, or extreme numbers.
   - **Error Handling**: Assert that the code throws the correct errors or handles failures gracefully.
   - Mock dependencies (DBs, network calls) to keep tests isolated and fast.

4. **Execution and Refinement**:
   - Run the test command using `run_command` (e.g., `npm test <filename>`).
   - If a test fails, analyze the output. Determine if the bug is in the test implementation or the application code, and fix it.

5. **Finalize**:
   - Mark the testing phase as `[x]` complete in the `task.md`.
