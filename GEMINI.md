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

## General Guidelines
- Gemini should implicitly load this `GEMINI.md` file whenever interacting with the repository.
- Before starting a complex task, Gemini should check `.agents/workflows/` for existing standard operating procedures.
- When encountering a specific domain problem, Gemini should look for available skills in `.agents/skills/`.
- Code generated must be robust, well-documented, and fully typed.

## Gemini Output & Code Conventions
- **Diff Formatting**: Always output code changes as unified diffs when summarizing changes.
- **Imports**: Never use wildcard imports in Kotlin (`import com.example.*`). Always explicitly declare imports.
- **Testing**: When writing tests, prefer MockK for mocking dependencies within the KMP ecosystem.
- **Coroutines**: Prefer suspending functions and `Flow` over callbacks. Always inject `CoroutineDispatcher`s rather than hardcoding `Dispatchers.IO` or `Dispatchers.Main` to ensure testability.
