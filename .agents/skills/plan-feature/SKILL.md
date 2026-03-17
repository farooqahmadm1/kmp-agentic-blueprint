---
name: plan-feature
description: Break down a user request or feature idea into a technical implementation plan.
---

# Feature Planning Skill

Use this skill when beginning work on a new feature, epic, or significant architectural change.

## Objectives
- Ensure requirements are fully understood before any code is written.
- Identify the impact on existing architecture.
- Create a clear, actionable roadmap for development.

## Step-by-Step Instructions

1. **Requirement Analysis**:
   - Read the user's prompt carefully.
   - Outline the primary goal, target audience/users, and required inputs/outputs.
   - STOP and use `notify_user` to ask clarifying questions if key details are missing.

2. **Context Gathering**:
   - Search the repository (`grep_search`, `find_by_name`) for existing components that can be reused.
   - Review related data models, API endpoints, or UI components.

3. **Architecture & Design**:
   - Draft how the feature integrates with the current system.
   - Identify any new dependencies, database schema changes, or external APIs required.

4. **Task Breakdown (The Deliverable)**:
   - Generate an `implementation_plan.md` artifact detailing the approach.
   - Create a `task.md` artifact with a granular checklist of steps (e.g., [ ] `Create DB migration`, [ ] `Add API route`, [ ] `Build UI component`).

5. **Approval**:
   - Use the `notify_user` tool to present the plan and wait for the user to say "approved" before proceeding to implementation.
