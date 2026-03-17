---
name: git-workflow
description: Standard operating procedure for Git branch naming, commit messages, and PR creation.
---

# Git Workflow & Standards

Use this skill when interacting with version control, committing code, pushing branches, or creating Pull Requests.

## Objectives
- Maintain a clean and navigable commit history.
- Ensure branch names clearly identify the type of work being done.
- Standardize Pull Request descriptions for easier code review.

## 1. Branch Naming Conventions
Always create a new branch for your work. Never commit directly to `main` or `master`.

**Format:** `<type>/<issue-number-or-short-desc>`

**Types:**
- `feat/`: For new features (e.g., `feat/add-user-auth`, `feat/123-payment-gateway`)
- `fix/`: For bug fixes (e.g., `fix/login-crash`, `fix/456-typo-in-header`)
- `chore/`: For routine tasks, dependency updates, or tool configuration (e.g., `chore/update-deps`)
- `docs/`: For documentation updates only.
- `refactor/`: For code changes that neither fix a bug nor add a feature.

## 2. Commit Message Conventions
Follow the Conventional Commits specification.

**Format:**
```
<type>(<optional scope>): <description>

[optional body]

[optional footer(s)]
```

**Rules:**
- `type` must match the branch type (`feat`, `fix`, `chore`, etc.).
- `description` must be short (under 50 characters), imperative mood ("add feature" not "added feature").
- `body` is optional but encouraged for complex changes. Explain *why* the change was made, not just *what* was changed.

**Example:**
```
feat(auth): add OAuth2 login support

Implemented the standard OAuth2 authorization code flow to allow users
to log in via Google and GitHub.

Resolves #123
```

## 3. Pull Request (PR) Creation
When work is complete and tested, create a PR targeting the main development branch.

**PR Title:** Should match the final commit message (e.g., `feat(auth): add OAuth2 login support`).

**PR Body Template:**
```markdown
## Description
Provide a clear and concise summary of the changes made.

## Related Issues
- Resolves #<issue_number> OR N/A

## Changes Made
- Added X
- Modified Y
- Removed Z

## Verification
- [ ] Unit tests added/updated and passing.
- [ ] Local manual testing completed. Describe steps if necessary.
- [ ] Documentation updated (if applicable).
```

## 4. Execution Steps for Gemini
When tasked with saving work or creating a PR, Gemini MUST follow these guarded steps:
1. **Prepare**: Verify the current branch (`git branch`). If on `main` or `master`, immediately checkout a new branch following the naming conventions. **NEVER commit directly to main/master.**
2. **Review Approval**: Present the changes to the user and request explicit permission to commit. DO NOT proceed without approval.
3. **Commit**: Once approved, stage appropriate files (`git add <files>`) and commit with a formatted message (`git commit -m "..."`).
4. **PR Approval**: Request explicit permission from the user to push the branch and open a PR. DO NOT proceed without approval.
5. **Create PR**: Once approved, push the branch (`git push -u origin <branch-name>`) and generate the PR using the `gh` CLI (e.g., `gh pr create`) with the templates above. **NEVER merge the PR automatically.**
