---
name: implement-feature
description: Execute the coding phase of a feature based on an approved plan.
---

# Feature Implementation Skill

Use this skill when executing the tasks outlined in `task.md` or an approved `implementation_plan.md`.

## Objectives
- Write clean, maintainable, and well-documented code.
- Follow the project's established conventions.
- Make incremental, verifiable progress.

## Step-by-Step Instructions

1. **Review the Plan**:
   - Read the `task.md` to understand the current priority.
   - Understand the expected outcome of the current sub-task.

2. **Setup & Scaffolding**:
   - If new libraries are needed, use `run_command` to install them (e.g., `npm install <pkg>`).
   - Create new files using the `write_to_file` tool with boilerplate code based on project patterns.

3. **Development (Iterative)**:
   - For existing files, use `multi_replace_file_content` to inject new logic.
   - Ensure all functions and complex logic blocks have explanatory comments.
   - Follow the architectural guidelines specified in the root `GEMINI.md`.

4. **Self-Correction & Debugging**:
   - If you encounter type errors or linting issues, resolve them immediately before moving to the next task.
   - Continually review the current state of files utilizing `view_file` to ensure context isn't lost.

5. **Track Progress**:
   - Update `task.md` (`[/]` for in-progress, `[x]` for completed) after finishing each logical chunk of work.
