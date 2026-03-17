---
name: database-migration
description: Standard operating procedure for modifying database schemas, bumping versions, and writing migration scripts.
---

# Database Migration Skill

Use this skill whenever a feature requires altering the local database (e.g., adding a table, adding a column, changing a data type) using SQLDelight or Room within a KMP project.

## Objectives
- Prevent data loss during schema upgrades.
- Ensure the database version is consistently bumped.
- Mandate strict planning and explicit user approval before executing any schema changes.

## Step-by-Step Instructions

1. **Mandatory Planning & Approval**:
   - Before writing *any* migration code, generate an `implementation_plan.md` detailing:
     - The current schema.
     - The proposed schema changes.
     - The SQL queries required to migrate the existing data.
   - Use `notify_user` to present the plan. **STOP**. Do not proceed until the user explicitly approves the plan.

2. **Bump Database Version**:
   - Locate the database configuration file (e.g., in SQLDelight, this might be updating the `.sqm` file name like `1.sqm` to `2.sqm`, or in Room, bumping the `version` integer in the `@Database` annotation).
   - Increment the version number sequentially.

3. **Implement the Migration Script**:
   - **SQLDelight**: Create the corresponding `.sqm` migration file (e.g., `<VersionNumber>.sqm`) containing the `ALTER TABLE` statements.
   - **Room**: Create a `Migration` object detailing the schema changes from the old version to the new version and add it to the database builder.

4. **Update Entity Models**:
   - Update the Domain/Data layer data classes to reflect the new schema fields.
   - Ensure the new fields are handled correctly in mapping functions (e.g., providing default values for older records if necessary).

5. **Review Phase (Strict Stop)**:
   - After the migration script and models are updated, present the changes to the user.
   - **STOP**. Request explicit approval to stage and commit the changes.

6. **Testing (Post-Approval)**:
   - If approved, run existing database tests. Ensure the migration path is verified either manually or automatically via the test suite.

7. **PR Creation (Strict Stop)**:
   - Commit the changes to an appropriate branch (e.g., `feat/db-add-user-age`).
   - Request explicit approval from the user to push the branch and create a Pull Request. **Do NOT auto-merge.**
