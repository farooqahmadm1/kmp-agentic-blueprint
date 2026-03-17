---
name: index-project-context
description: Builds and updates an AI-readable map of the project structure, modules, and key entry points.
---

# Project Indexing (AI Context Map) Skill

Use this skill when first entering a new codebase, or after a major restructuring (like modularization), to create a "memory map" that allows Gemini to navigate the project efficiently.

## Objectives
- Create a high-level summary of the codebase for efficient context loading.
- Map module dependencies and architectural boundaries.
- Reduce the "search cost" for the agent during complex tasks.

## Step-by-Step Instructions

1. **Structural Scan**:
   - Run `ls -R` or use `list_dir` recursively to understand the top-level directory structure.
   - Identify core modules (e.g., `:app`, `:core:network`, `:features:auth`).

2. **Identify Entry Points**:
   - Find main application classes, Gradle settings, and dependency injection root files (e.g., `AppModule.kt`, `MainApplication.kt`).
   - Note where the "Source of Truth" (`GEMINI.md`) is located.

3. **Generate/Update AI_CONTEXT.md**:
   - Create or update a file named `AI_CONTEXT.md` in the root (or `.agents/context/`). This file serves as the agent's "long-term memory" for this project.
   - **Template for AI_CONTEXT.md**:
     ```markdown
     # Project Context Map (AI Memory)
     
     ## Core Modules
     - `:app`: Main entry point, platform orchestrator.
     - `:core:network`: Ktor client implementation, shared DTOs.
     - `:features:*`: Isolated feature modules following MVI.

     ## Crucial Files
     - `libs.versions.toml`: Central dependency management.
     - `AppModule.kt`: Root of the Koin DI graph.
     - `Database.sq`: SQLDelight schema definitions.

     ## Relationship Map
     - `:features` depend on `:core:network` and `:domain:models`.
     - `:app` depends on all `:features`.

     ## Active Focus Areas
     - [Current development focus, e.g., "Refactoring User Auth"]
     ```

4. **Hierarchical Indexing Strategy (Scaling for Large Repos)**:
   - For repositories with many modules, do not try to fit everything in the root `AI_CONTEXT.md`.
   - **Root Level (`AI_CONTEXT.md`)**: High-level map, dependency graph, and entry points only.
   - **Module Level (`.context.md` or `README.md`)**: Each module/feature should have its own local context file. This file should describe:
     - The module's primary responsibility.
     - Public API / Interface.
     - Internal data flow (MVI specifics).
     - Known limitations or quirks.
   - **Search Depth**: When working on a specific feature, the agent should first read the root `AI_CONTEXT.md` to find the correct module, and then read the local `.context.md` for that module to get deep-dive details.

5. **Finalize**:
   - Use `notify_user` to present the updated context map and ask if there are any "hidden" dependencies or architectural nuances not caught by the scan.
