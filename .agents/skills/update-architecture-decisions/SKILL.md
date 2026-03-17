---
name: update-architecture-decisions
description: Maintains an Architecture Decision Records (ADR) log documenting major technical choices.
---

# Architecture Decision Records (ADR) Logger Skill

Use this skill whenever a significant architectural change or technology choice is made within the project (e.g., "Choosing SQLDelight over Room", "Deciding on Koin vs Hilt").

## Objectives
- Maintain a historical log of *why* decisions were made, preserving context for future agents and developers.
- Standardize the format of ADR documentation.

## Step-by-Step Instructions

1. **Locate or Initialize the ADR Directory**:
   - Check if a `docs/adr/` directory exists. If not, use `run_command` (`mkdir -p docs/adr`) to create one.
   - If this is the first ADR, create an `index.md` listing the records.

2. **Draft the New Record**:
   - Determine the next available sequential number (e.g., `0004-use-ktor-for-networking.md`).
   - Use the `write_to_file` tool to create the new ADR using the standard template:

### ADR Template
```markdown
# [Title of Document]

* Status: [proposed | accepted | rejected | deprecated | superseded]
* Date: [YYYY-MM-DD]

## Context and Problem Statement
What is the issue that we're seeing that is motivating this decision or change?

## Considered Options
* [Option 1]
* [Option 2]
* [Option 3]

## Decision Outcome
Chosen option: "[Option 1]", because [justification. e.g., it is multiplatform compatible, performs better, etc.].
```

3. **Update Index**:
   - Update `docs/adr/index.md` to include a link to the newly created record.

4. **Notify**:
   - Use `notify_user` to prompt the user to review and accept the newly proposed ADR before finalizing it.
