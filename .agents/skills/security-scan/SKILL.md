---
name: security-scan
description: A specialized code-scanning skill for manual or automated security verification.
---

# Security & Compliance Skill

Use this skill before every commit and PR creation to ensure the codebase remains secure and free of sensitive information.

## Objectives
- Prevent the accidental leakage of secrets (API keys, tokens, credentials).
- Ensure network and storage security best practices are followed.
- Validate that dependencies are free from known vulnerabilities.

## Step-by-Step Instructions

1. **Secret Detection**:
   - Run a `grep_search` using regex patterns for common secret formats:
     - API Keys (e.g., `AIza`, `sk_live_`, `ghp_`).
     - Private Keys (e.g., `-----BEGIN RSA PRIVATE KEY-----`).
     - Hardcoded passwords or local file paths.
   - If any potential secrets are found, **STOP** and ask the user if they should be moved to a secure environment variable or a local `secrets.properties` file (which must be git-ignored).

2. **Network Security Audit**:
   - Check all Ktor client configurations or URL strings.
   - Ensure `https://` is used for all external API calls.
   - Verify that sensitive data is not being leaked in URL parameters or logs.

3. **Storage & Data Privacy**:
   - Review database or shared preference implementations.
   - Ensure sensitive user data (tokens, PII) is encrypted (e.g., using SQLCipher for SQLDelight or EncryptedSharedPreferences on Android).

4. **Dependency Audit**:
   - Run `./gradlew dependencyCheckAnalyze` (if the plugin is installed) to check for CVEs in external libraries.
   - If vulnerabilities are found, use the `kmp-dependency-update` skill to bump to a patched version.

5. **Compliance Report**:
   - Output a brief summary: "Security Scan: PASS" or "Security Scan: VIOLATIONS FOUND".
   - If violations are found, detail them and suggest immediate remediation steps.
