---
name: kmp-dependency-update
description: A specialized skill for updating dependencies in Kotlin Multiplatform projects.
---

# KMP Dependency Update Skill

Use this skill when asked to add, update, or resolve conflicts with external libraries in a Kotlin Multiplatform project.

## Objectives
- Understand the structure of `build.gradle.kts` files (specifically `sourceSets` like `commonMain`, `androidMain`, `iosMain`).
- Safely update dependencies without breaking cross-platform compilation.

## Step-by-Step Instructions

1. **Locate Build Files**:
   - Find all `build.gradle.kts` files using the `find_by_name` tool.
   - Typically, dependencies are defined in `Shared/build.gradle.kts` or a centrally managed `libs.versions.toml` (Version Catalog).

2. **Analyze Current Versions**:
   - Read the relevant build file or version catalog.
   - Identify the library the user wishes to update (e.g., Ktor, SQLDelight, Coroutines).

3. **Check Compatibility**:
   - Verify that the target version of the library supports Kotlin Multiplatform and the specific targets configured in the project (Android, iOS, Desktop, Web).

4. **Apply Updates**:
   - Use `replace_file_content` to carefully update the version string.
   - Ensure the dependency is added to the correct `sourceSet`. For common code, it belongs in `commonMain.dependencies`. For platform-specific implementations, it goes in `androidMain.dependencies`, `iosMain.dependencies`, etc.

5. **Verify**:
   - Run the Gradle build or sync command (e.g., `./gradlew assemble`) using `run_command` to ensure there are no resolution errors.
