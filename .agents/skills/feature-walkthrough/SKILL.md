---
name: feature-walkthrough
description: Automatically generates a comprehensive walkthrough of changes for better knowledge sharing.
---

# Feature Walkthrough Skill

Use this skill after completing a feature implementation but before creating a Pull Request to document the "why" and "how" of your changes.

## Objectives
- Improve PR review quality and speed.
- Build a persistent history of architectural changes.
- Ensure the user/reviewer understands exactly what was tested.

## Step-by-Step Instructions

1. **Information Synthesis**:
   - Review the original `implementation_plan.md` and the final code.
   - Gather all visual evidence (screenshots/videos) created via the `visual-validation` skill.

2. **Generate walkthrough.md**:
   - Create a file named `walkthrough.md` (or append to a central log) with the following sections:
     - **Summary**: A high-level 2-sentence description of the feature/fix.
     - **Key Changes**: Bulleted list of architectural decisions (linking to the ADR if applicable).
     - **Visuals**: Embedded screenshots or recordings showing the UI in action.
     - **Verification Proof**: Summary of test results (Unit/Integration) and manual testing steps performed.
     - **Future Considerations**: Any technical debt introduced or future improvements planned.

3. **Formatting**:
   - Use carousels for multiple related screenshots.
   - Include direct file links to the most important code changes for easy navigation.

4. **Integration**:
   - Copy the core content of this walkthrough into the Pull Request description to ensure reviewers have all the context they need without leaving the PR page.

5. **Finalize**:
   - Present the `walkthrough.md` to the user and request approval before proceeding to the PR phase.
