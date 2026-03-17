---
name: visual-validation
description: Standard procedure for verifying UI changes through screenshots, recordings, and design comparisons.
---

# UI Visual Validation Skill

Use this skill whenever a feature involves changes to the UI (Compose Multiplatform, SwiftUI, XML, etc.) to ensure the result matches the design intent.

## Objectives
- Provide visual proof of correctness for reviewers.
- Catch layout regressions early.
- Ensure cross-platform UI consistency (Android/iOS).

## Step-by-Step Instructions

1. **Verify State**:
   - Ensure the UI code is compiled and running on at least one target (Emulator or Simulator).

2. **Capture Evidence**:
   - Use `run_command` or specific simulator tools to:
     - Take a high-resolution screenshot of the affected screen.
     - (Optional) Record a 5-10 second clip of the interaction (e.g., button click, navigation).
   
3. **Design Audit**:
   - Compare the capture against the provided design mockup (if available).
   - Check for:
     - **Layout**: Proper spacing, alignment, and padding.
     - **Styling**: Correct colors, fonts, and corner radii.
     - **Dynamics**: Smooth transitions and hover/click states.

4. **Document Visuals**:
   - Upload the media to a temporary storage or artifacts directory.
   - Use the markdown syntax `![Component Name](/path/to/screenshot.png)` to embed the evidence in the PR description or a `walkthrough.md`.

5. **Cross-Platform Check**:
   - If this is a shared UI (Compose Multiplatform), note if there are any platform-specific rendering differences that need to be addressed.
