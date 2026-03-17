# Gemini Blueprint - KMP

The **Gemini Blueprint** is the Gemini equivalent of the "Claude Code" organization-wide blueprint. Introduced in early 2026, it represents a shift from simple system prompts to a tiered, filesystem-based agentic architecture. This repository establishes a reference architecture for **Gemini-native agentic environments**, specifically tuned for **Kotlin Multiplatform (KMP)** development using the **MVI (Model-View-Intent)** pattern and **SOLID** principles.

## 🛠️ How it Works
Instead of a single, static prompt, the Gemini Blueprint uses a tiered discovery system:
1.  **Source of Truth (`GEMINI.md`)**: The root-level context file that defines the project's identity, tech stack, and non-negotiable architectural rules.
2.  **Skill Manifests (`.agents/skills/`)**: Specialized `SKILL.md` files that Gemini "discovers" to perform complex, domain-specific tasks (like MVI scaffolding or DB migrations).
3.  **Reproducible Workflows (`.agents/workflows/`)**: Standard operating procedures for multi-step sequences like PR reviews or releases.
4.  **AI Memory (`AI_CONTEXT.md`)**: A living index that allows the agent to maintain a mental map of large, modular codebases.

## ✨ Key Benefits
-   **Consistency**: Ensures every agent (and developer) follows the exact same senior-level naming and architectural standards.
-   **Strict Safety**: Implements mandatory "Hard Stops" for human approval before planning, coding, or committing.
-   **Context Efficiency**: Uses an indexing skill to map large codebases, preventing the AI from "getting lost" in complex module graphs.
-   **Zero Re-prompting**: The agent self-corrects based on the codebase's local rules as soon as it enters the directory.

## 🚀 How to Adopt this Blueprint

To turn any repository into a "Gemini-Native" brain, follow these steps:

### 1. Copy the Configuration
Copy the following files and directories to the root of your new project:
- `GEMINI.md`: The primary "Source of Truth" for the AI agent.
- `.agents/skills/`: A directory containing modular `SKILL.md` manifests that define specific capabilities (MVI generation, Git workflows, etc.).
- `.agents/workflows/`: A directory containing multi-step procedures (Release cycles, PR pipelines).

### 2. Customize `GEMINI.md`
Edit the `GEMINI.md` file to match your project's specific details:
- Project Name and Goal.
- Specific Tech Stack details (e.g., if you use Compose Multiplatform or SwiftUI).
- Custom Architectural Guidelines.

### 3. Initialize Agent State
When starting the Gemini CLI or Code Assist in the new project, the agent will automatically discover the `GEMINI.md` file. It will use this as its core system instruction, making it aware of your local skills and workflows without needing manual re-prompting.

---

## 🏗️ Core Architecture

### **The GEMINI.md "Brain"**
The `GEMINI.md` file acts as the persistent memory of the project. It defines:
- **Ground Rules**: Strict instructions the agent must never break.
- **Strict Gating**: Mandatory "STOP" points where the agent *must* request user approval before planning, coding, or committing.
- **Naming Conventions**: Senior-level mobile development standards.

### **Agent Skills (`.agents/skills/`)**
Modular capabilities that the agent can "learn" by reading the filesystem:
- `generate-mvi-feature`: Scaffolds MVI components.
- `git-workflow`: Enforces branch naming and conventional commits.
- `database-migration`: Safely handles schema changes and versioning.
- `validate-soc`: Scans for Separation of Concerns violations.
- `generate-koin-module`: Scaffolds dependency injection logic.

### **Workflows (`.agents/workflows/`)**
Standard operating procedures for complex tasks:
- `pr-review-pipeline`: Automated code quality check.
- `deploy-to-staging`: Build and distribution procedure.

## 🛡️ Strict Gating & Protections
This blueprint is designed for safety. The agent is **FORBIDDEN** from:
- Committing directly to `main` or `master`.
- Merging PRs automatically.
- Proceeding from planning to execution without explicit approval.
- Committing code without a final manual review.

---

*Set up by Antigravity.*
