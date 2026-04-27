---
name: efcore-data-access-review
description: Use this skill when reviewing EF Core queries, entities, migrations, DbContext configuration, and application service data access.
---

# EF Core Data Access Review Skill

Use this skill for data access changes.

## Review process

1. Identify whether the code path is read-only or write-oriented.
2. For read-only paths:
   - Use `AsNoTracking()`.
   - Project into DTOs/view models.
   - Avoid loading entire entity graphs unnecessarily.
3. For write paths:
   - Load only the data needed to validate and update.
   - Validate ownership and authorization before mutation.
   - Use transactions only when multiple changes must commit atomically.
4. For relationships:
   - Check required/optional relationships.
   - Check delete behavior.
   - Check indexes for frequently filtered fields.
5. For migrations:
   - Confirm migration name describes the change.
   - Confirm migration does not drop data unexpectedly.
   - Confirm seed data does not include production credentials.
6. For leave workflows:
   - Validate date ranges.
   - Validate leave type existence.
   - Validate allocation availability.
   - Validate request status transitions.
   - Validate the current user can perform the action.

## Validation commands

Run:

```bash
dotnet restore LeaveManagementSystem.sln
dotnet build LeaveManagementSystem.sln --configuration Release --no-restore
dotnet test LeaveManagementSystem.sln --configuration Release --no-build