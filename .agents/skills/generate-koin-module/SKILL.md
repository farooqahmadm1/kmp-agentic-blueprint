---
name: generate-koin-module
description: Creates and configures Koin dependency injection modules for KMP features.
---

# Koin Dependency Injection Skill

Use this skill when integrating a new feature, repository, or service into the project's dependency graph using Koin.

## Objectives
- Ensure dependencies are properly scoped and injected.
- Maintain a clean module structure aligned with the project's Architecture (MVI & KMP).
- Prevent cyclic dependencies and missing definitions.

## Step-by-Step Instructions

1. **Identify Dependencies**:
   - Determine what classes need to be provided (e.g., `UserRepository`, `AuthService`, `UserProfileViewModel`).
   - Identify whether they should be singletons (`single`), factories (`factory`), or scoped to a specific lifecycle (`viewModel` / `scoped`).

2. **Locate or Create Module**:
   - Determine the appropriate module file (e.g., `NetworkModule.kt`, `FeatureModule.kt`, or `AppModule.kt`).
   - If a new feature is being added, create a dedicated `${FeatureName}Module.kt` inside the feature's `di/` package.

3. **Define the Module**:
   - Use the `module { ... }` DSL to declare dependencies.
   - Example:
     ```kotlin
     val featureModule = module {
         single<AuthService> { AuthServiceImpl(get()) }
         factory<UserRepository> { UserRepositoryImpl(get(), get()) }
         factory { UserProfileViewModel(get()) }
     }
     ```

4. **Register the Module**:
   - Ensure the new module is included in the main Koin `startKoin` initialization block or added to the app's list of `modules`.
   - Typically, this is done in `commonMain`'s application initialization or platform-specific entry points (e.g., `MainApplication.kt` for Android or `iOSApp.swift` / Kotlin wrapper for iOS).

5. **Verify**:
   - If the project supports Koin verification, run the verification tests to ensure no `NoBeanDefFoundException` will occur at runtime.
   - Summarize the newly added injections to the user.
