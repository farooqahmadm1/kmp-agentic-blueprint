---
name: gradle-update-check
description: Verifies and updates Gradle dependencies, ensuring version alignment and compatibility across the project.
---

# Gradle Dependency & Version Check Skill

Use this skill to safely update project dependencies while strictly guaranteeing that cross-module versions and toolchains (Kotlin, Compose, KSP, Coroutines) are correctly aligned.

## Objectives
- Prevent version mismatches between interdependent libraries.
- Standardize the usage of Gradle Version Catalogs (`libs.versions.toml`).
- Audit the build environment for outdated tools.

## Step-by-Step Instructions

1. **Locate the Source of Truth**:
   - First, check for the existence of `gradle/libs.versions.toml` using the `find_by_name` tool. Assure this file acts as the single source of truth for library versions.
   - If not using a Version Catalog, locate the root `build.gradle.kts` (or `buildSrc`) where extra properties or central dependency constants are defined.

2. **Verify Critical Version Alignments**:
   - **Kotlin Version**: Ensure the Kotlin compiler version (e.g., `1.9.23`) matches the `kotlinx-coroutines`, `kotlinx-serialization`, and `ksp` plugin requirements exactly.
   - **Compose Multiplatform**: Ensure the Compose compiler version accurately matches the active Kotlin compiler version.
   - **Ktor**: If using Ktor, verify that `ktor-client-core`, `ktor-client-content-negotiation`, and engine dependencies (e.g., `ktor-client-darwin`, `ktor-client-okhttp`) are all on the exact same version number.

3. **Check for Redundant Definitions**:
   - Search the sub-modules (`commonMain`, `androidMain`, `iosMain`) for hardcoded version strings (e.g., `"1.2.0"`). 
   - Flag any hardcoded version as technical debt. All dependencies should reference the central Version Catalog (e.g., `libs.ktor.core`).

4. **Perform Safe Updates**:
   - When updating a library in the `libs.versions.toml`, scan the document to update *all* related artifacts simultaneously.
   - Example: If bumping `sqlDelight` from `2.0.0` to `2.0.1`, ensure the `sqldelight-android-driver` and `sqldelight-native-driver` versions are also bumped.

5. **Validation Step**:
   - Use `run_command` to execute `./gradlew buildHealth` (if using dependency analysis plugin) or structurally `./gradlew sync`.
   - Provide a summary report detailing which libraries were bumped, the old version, the new version, and confirmation that inter-dependencies remain aligned.
