# Gemini Blueprint

This file serves as the unified "Source of Truth" for Gemini within this repository.
It dictates project-specific context, ground rules, and architectural guidelines that Gemini Agents must adhere to.

## Project Context
- **Name**: Agentic Blueprint
- **Goal**: Establish a reference architecture for Gemini-native agentic environments.
- **Tech Stack**: Kotlin Multiplatform (KMP)

## Architectural Guidelines
All Gemini Agents must adhere to the following when writing or reviewing code in this codebase:
- **Architecture Pattern**: Model-View-Intent (MVI).
    - UI components (Views) should only observe State and emit Intents. They must contain no business logic.
    - Business logic resides in the Intent handlers/Reducers, which output new Model states.
- **Core Principles**: Strictly adhere to **SOLID principles**.
- **Separation of Concerns (SoC)**: Maintain strict isolation between UI, Domain, and Data layers.
- **Dependency Injection**: Use **Koin** for all dependency injection and inversion of control. Constructor injection is preferred.

## Agent Ecosystem
This repository is configured with a modular agentic architecture:
- **Agent Skills**: Custom capabilities for Gemini are located in `.agents/skills/`. Each skill is defined by a `SKILL.md` manifest.
- **Workflows**: Multi-step, reproducible procedures are stored in `.agents/workflows/`. Gemini can parse and execute these directly.

## AI Context & Memory
To maintain an efficient "mental map" of the codebase, Gemini should periodically update the `AI_CONTEXT.md` file using the `index-project-context` skill. This file serves as the agent's long-term memory, summarizing:
- Module dependencies and architectural boundaries.
- Key class entry points and structural maps.
- Current active focus areas to maintain continuity across sessions.

## General Guidelines
- Gemini should implicitly load this `GEMINI.md` file whenever interacting with the repository.
- Before starting a complex task, Gemini should check `.agents/workflows/` for existing standard operating procedures.
- When encountering a specific domain problem, Gemini should look for available skills in `.agents/skills/`.
- Code generated must be robust, well-documented, and fully typed.

## Strict Gating & Approvals
Gemini must NEVER proceed automatically through the development lifecycle. The following hard stops must be observed:
1. **Planning Phase**: Gemini must generate a plan (`implementation_plan.md` or `task.md`) and STOP. Explicit user approval is required before writing any code (features or bug fixes).
2. **Review Phase**: After code is written, Gemini must present the changes and STOP. Explicit user approval is required before staging or committing. If comments/feedback are given, Gemini must adjust the plan and re-execute.
3. **Commit & PR Phase**: Code must be committed independently. Explicit user approval is required before pushing the branch and opening a Pull Request.
4. **Master Branch Protection**: Gemini is strictly FORBIDDEN from merging directly into `main` or `master`. All changes must go through the Pull Request pipeline.

## Gemini Output & Code Conventions
- **Diff Formatting**: Always output code changes as unified diffs when summarizing changes.
- **Imports**: Never use wildcard imports in Kotlin (`import com.example.*`). Always explicitly declare imports.
- **Testing**: When writing tests, prefer MockK for mocking dependencies within the KMP ecosystem.
- **Coroutines**: Prefer suspending functions and `Flow` over callbacks. Always inject `CoroutineDispatcher`s rather than hardcoding `Dispatchers.IO` or `Dispatchers.Main` to ensure testability.

## Naming Conventions (Senior Mobile Standard)
- **Classes & Interfaces**: Use `PascalCase` (e.g., `UserProfileViewModel`).
- **Functions & Variables**: Use `camelCase`, and keep names descriptive rather than abbreviated (e.g., `fetchUserData` instead of `fetchData`).
- **Constants & Enums**: Use `UPPER_SNAKE_CASE` (e.g., `MAX_RETRY_COUNT`).
- **Backing Properties**: Prefix private mutable backing fields with an underscore (e.g., `_uiState` publicly exposed as `val uiState`).
- **Booleans**: Prefix boolean variables or functions with `is`, `has`, `should`, or `can` to ensure they read like a question (e.g., `isLoading`, `hasNetworkError`).
- **Implementations**: Interfaces should have clean semantic names (e.g., `UserRepository`). Implementations should end with `Impl` (e.g., `UserRepositoryImpl`) unless specific (e.g., `OfflineUserRepository`).
- **View Models**: Intent functions should be named as actions (e.g., `onSubmitClicked`), state variables should describe the screen state.
