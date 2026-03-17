---
description: How to deploy the current build to a staging environment (TestFlight/Firebase).
---

# Deploy to Staging Workflow

When instructed to push a build to staging for QA, follow this procedure.

1. **Verify State**:
   - Ensure you are on the `main` or an integration branch.
   - Ensure the working directory is clean (`git status`).
// turbo
2. **Run E2E Tests**:
   - Execute the end-to-end test suite to guarantee core flows are functioning correctly before deployment.

3. **Bump Build Numbers**:
   - Increment the android `versionCode` in `build.gradle.kts`.
   - Increment the iOS build number in the `.pbxproj` or `Info.plist`.

4. **Build Artifacts**:
   - **Android**: Use `run_command` to execute `./gradlew assembleRelease` or `./gradlew bundleRelease`.
   - **iOS**: Use `run_command` with fastlane or xcodebuild (e.g., `fastlane ios beta`).

5. **Upload & Distribute**:
   - Upload the Android `.apk`/`.aab` to Firebase App Distribution using the Firebase CLI or appropriate Gradle plugin.
   - Upload the iOS `.ipa` to TestFlight.
   - Wait for confirmation of successful upload.

6. **Notify Team**:
   - Output a summary of the release notes for this staging build, including the new version numbers. Use `notify_user` to communicate success.
