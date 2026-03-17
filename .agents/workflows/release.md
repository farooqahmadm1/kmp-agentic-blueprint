---
description: How to release a new version of the project
---

# Release Workflow

When requested to release a new version, Gemini should execute the following steps in sequence:

1. **Analyze Changelog**: Review all commits since the last tag and generate a draft release notes summary.
// turbo
2. **Run Tests**: Execute the test suite to ensure the build is green before cutting a release.
3. **Bump Version**: Update the version number in relevant configuration files (e.g., `package.json`, `pyproject.toml`) based on semantic versioning rules.
4. **Prompt User**: Use the `notify_user` tool (if applicable) to request final approval of the release notes and version bump before creating the git tag.
