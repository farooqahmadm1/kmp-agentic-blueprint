---
name: review-code
description: Perform a comprehensive code review focusing on quality, security, and performance.
---

# Code Review Skill

Use this skill when asked to review a pull request, a specific pull of code, or as a final check before deployment.

## Objectives
- Catch bugs before they reach production.
- Enforce code style and maintainability.
- Identify security vulnerabilities and performance bottlenecks.

## Step-by-Step Instructions

1. **Context & Intent**:
   - Understand *why* the code was written. What problem does it solve?
   - Compare the code against the original requirements.

2. **Readability & Maintainability Check**:
   - Are variable and function names descriptive?
   - Is there dead code or unnecessary comments?
   - Are functions too large? (Suggest breaking them down if so).
   - Does it adhere to `GEMINI.md` standards?

3. **Performance Audit**:
   - Look for N+1 query problems in database calls.
   - Check for inefficient loops or unnecessary memory allocations.
   - Suggest memoization, caching, or asynchronous patterns where appropriate.

4. **Security Scan**:
   - Ensure inputs from users or external APIs are validated and sanitized.
   - Check for hardcoded secrets or credentials.
   - Verify proper authorization checks are in place.

5. **Deliver Findings**:
   - Create a structured markdown response.
   - Group feedback logically (e.g., "Critical Issues", "Suggestions", "Nitpicks").
   - Provide concrete code snippets illustrating how to improve the code, rather than just pointing out the flaw.
