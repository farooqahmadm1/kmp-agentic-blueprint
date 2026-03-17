---
name: modularize-feature
description: Extracts existing code or scaffolds a new, isolated Gradle module for a specific feature.
---

# Modularization Skill

Use this skill when asked to break down a monolithic architecture into smaller, independent modules, or when scaffolding a brand new feature module in a Kotlin Multiplatform project.

## Objectives
- Enforce strict separation of concerns at the build level.
- Improve build times by isolating dependencies.
- Ensure proper configuration of `build.gradle.kts` for common/platform targets.

## Step-by-Step Instructions

1. **Understand Module Responsibility**:
   - Determine the scope of the new module (e.g., `:features:auth`, `:core:network`, `:domain:models`).
   - Identify the minimal set of dependencies required for this module to function via the Version Catalog (`libs.versions.toml`).

2. **Scaffold Directory Structure**:
   - Create the new module directory at the requested path.
   - Set up the standard KMP source sets: `src/commonMain/kotlin`, `src/androidMain/kotlin`, `src/iosMain/kotlin` (or others if targeting Desktop/Web).

3. **Configure Build File (`build.gradle.kts`)**:
   - Create the `build.gradle.kts` file in the module root.
   - Apply the necessary Kotlin Multiplatform and Android library plugins.
   - Configure the `kotlin { ... }` block with `androidTarget()` and iOS targets (`iosX64()`, `iosArm64()`, `iosSimulatorArm64()`).
   - Declare internal dependencies to other project modules using `project(":core:network")` sparingly, avoiding circular dependencies.

4. **Update Settings File (`settings.gradle.kts`)**:
   - Add the new module to the root `settings.gradle.kts` (e.g., `include(":features:auth")`).

5. **Code Migration (If Extracting)**:
   - Carefully move the existing files (Domain models, Intents, Views) from the `app` module into the new module's `commonMain` directory using the `run_command` (e.g., `mv ...`).
   - Use `grep_search` to find and update all broken imports across the project that reference the moved classes.
   - Ensure Koin `module { ... }` blocks are also extracted into the new module.

6. **Validation**:
   - Execute `./gradlew :<new-module-name>:assemble` to ensure the new module compiles cleanly in isolation.
   - Provide a summary to the user detailing the new module structure and any dependency graph changes.
