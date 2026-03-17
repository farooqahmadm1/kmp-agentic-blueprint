---
name: analyze-tech-debt
description: Analyzes the codebase for technical debt and generates a report.
---

# Tech Debt Analysis Skill

This skill empowers Gemini to proactively identify and categorize technical debt within the repository.

## Instructions for Gemini
When invoked to perform tech debt analysis, follow these steps:

1. **Scan**: Analyze the codebase for common anti-patterns (e.g., duplicated code, overly complex methods, missing unit tests, outdated dependencies).
2. **Review Context**: Cross-reference findings with the architectural guidelines defined in the project's `GEMINI.md`.
3. **Categorize**: Group identified debt into categories: `High Priority`, `Refactoring Needed`, or `Documentation Missing`.
4. **Report**: Output a structured markdown report detailing the findings, exact file locations, and actionable recommendations to resolve the debt.

### Optional Helper Scripts
(If this skill requires custom scripts, they would reside in an adjacent `scripts/` directory within this skill folder, and Gemini would execute them as part of the analysis).
