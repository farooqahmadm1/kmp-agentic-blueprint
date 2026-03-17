---
name: validate-soc
description: A specialized code-scanning skill that checks for Separation of Concerns violations.
---

# Separation of Concerns (SoC) Validation Skill

Use this skill to strictly enforce the architectural boundaries defined in `GEMINI.md` within a Kotlin Multiplatform, MVI-driven codebase.

## Objectives
- Prevent "God objects" and tightly coupled code.
- Ensure Views remain stateless and only emit intents.
- Ensure Domain models contain no UI or Framework-specific imports.

## Step-by-Step Instructions

1. **Target Selection**:
   - Identify the files or directory you want to validate (e.g., passing a specific feature package to the agent).
   - Read the contents using `view_file` or `grep_search`.

2. **UI Layer Validation**:
   - **Check**: Do any `View` or `Screen` (Compose) functions contain business logic, database queries, or direct network calls?
   - **Check**: Does the View receive a `State` object and emit an `Intent` via a callback (e.g., `(Intent) -> Unit`)?
   - **Violation Trigger**: If a View directly accesses a Repository or an HTTP client, flag it as a critical failure.

3. **Domain Layer Validation**:
   - **Check**: Do `State`, `Intent`, or `Reducer/ViewModel` files import UI frameworks (e.g., `androidx.compose.*` or `UIKit`)?
   - **Violation Trigger**: If the Domain layer knows about UI specifics, flag it. It should remain pure Kotlin.

4. **Data Layer Validation**:
   - **Check**: Does the network or database implementation bleed into the application logic?
   - **Check**: Does the Data layer map its DTOs/Entities back to Domain `Model` classes before returning them?
   
5. **Report & Auto-Fix**:
   - Provide a markdown report of all violations.
   - Use `multi_replace_file_content` to proactively sever the connections, moving the offending code into its correct layer if possible.
