---
name: generate-mvi-feature
description: Scaffolds a new Kotlin Multiplatform feature following the MVI architecture and SOLID principles.
---

# Generate MVI Feature Skill

Use this skill when asked to create a new component, screen, or entirely new functional area in the app.

## Objectives
- Auto-generate the boilerplate for Model-View-Intent architecture.
- Strictly separate UI (Views), Domain (Models/Intents), and Data layers.
- Ensure cross-platform compatibility where applicable.

## Step-by-Step Instructions

1. **Context Understanding**:
   - Ask the user for the `Feature Name` (e.g., `UserProfile`, `Checkout`).
   - Determine if the feature requires local database caching or network calls.

2. **Directory Structure Strategy**:
   - Determine the correct module/package for this feature based on the existing codebase (typically inside `commonMain` for KMP).
   - Ensure you are creating files within `ui/`, `domain/`, and `data/` sub-packages according to the Separation of Concerns (SoC) principle.

3. **Generate Domain Layer (The Core)**:
   - Create the `State` class (e.g., `UserProfileState.kt`) to hold the immutable data structure for the View.
   - Create the `Intent` sealed class (e.g., `UserProfileIntent.kt`) defining all possible actions (e.g., `LoadProfile`, `UpdateName`).
   - Create the `Reducer` or `ViewModel` equivalent that takes an `Intent` and mutates the `State`.

4. **Generate Data Layer (Optional but Common)**:
   - If data fetching is required, stub out a `Repository` interface in the Domain layer and implement it in the Data layer.

5. **Generate UI Layer (Stateless)**:
   - Create the View component (e.g., in Compose Multiplatform).
   - The View MUST NOT contain business logic; it must only receive the `State` and a callback function for emitting `Intent`s.

6. **Finalize**:
   - Output the generated code to the appropriate files using the `write_to_file` tool.
   - Summarize the new architecture graph for the user using `notify_user`.
