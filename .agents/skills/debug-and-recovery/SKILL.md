---
name: debug-and-recovery
description: Systematically diagnoses and fixes complex KMP build errors and environment issues.
---

# Debug & Recovery Skill

Use this skill when common build commands (`./gradlew build`) fail with complex or ambiguous errors, particularly those involving multiplatform linking (iOS/Android/Desktop).

## Objectives
- Reduce downtime caused by build environment issues.
- Systematically eliminate variables until the root cause is found.
- Document known "gotchas" in the project's build process.

## Step-by-Step Instructions

1. **Information Gathering**:
   - Run the failing command with `--stacktrace` and `--info` flags.
   - Capture the logs and use `grep_search` to find the primary error message.
   - Determine if the failure is in `commonMain`, a specific platform target (e.g., `:app:iosX64`), or a Gradle plugin.

2. **The "Clean Slate" Protocol**:
   - If the error looks like a cache or sync issue, use `run_command` to execute:
     - `./gradlew clean`
     - Deleting local `.gradle` and `build` folders for the affected module.
     - For iOS: `rm -rf ~/Library/Developer/Xcode/DerivedData` and re-running `pod install` (if using CocoaPods).

3. **Incremental Bisecting**:
   - Comment out recently added dependencies or code blocks to see if the build passes.
   - Verify if the issue is a version mismatch by running the `gradle-update-check` skill.

4. **KMP Linkage Check**:
   - For iOS errors, check the Kotlin-Swift interop layer. Ensure all types are correctly exported in the framework header.
   - Check if any native dependencies (e.g., C-interop or CocoaPods) are missing or outdated.

5. **Recovery Report**:
   - Once the fix is found, document the solution in the project's troubleshooting guide or update the `AI_CONTEXT.md` focus area if it's a recurring environment problem.
