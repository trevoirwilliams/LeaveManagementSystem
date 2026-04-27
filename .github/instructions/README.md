# LeaveManagementSystem Instruction Files

This folder contains file-scoped GitHub Copilot instructions used by the LeaveManagementSystem codebase. These instruction files are designed to be copied into a companion repository so Copilot can apply the same architectural, EF Core, MVC, and security expectations.

## Files In This Folder

1. `aspnet-mvc.instructions.md`
   - Scope: `LeaveManagementSystem.Web/**/*.{cs,cshtml,json}`
   - Focus: MVC controller/view patterns, model validation, authorization attributes, antiforgery, middleware ordering, and presentation-layer boundaries.

2. `ef-core.instructions.md`
   - Scope: `LeaveManagementSystem.Data/**/*.cs,LeaveManagementSystem.Application/Services/**/*.cs`
   - Focus: async EF Core usage, `AsNoTracking()` for read paths, projection-first querying, overposting prevention, migration placement, and N+1 avoidance.

3. `security.instructions.md`
   - Scope: `**/*.{cs,cshtml,json,yml,yaml,config,ps1,sh}`
   - Focus: secrets handling, secure configuration defaults, Identity hardening, safe logging, HTTPS/HSTS, and authorization-sensitive testing.

## How To Use In A Companion Repo

1. Copy this folder to `.github/instructions/` in the companion repository.
2. Also include `.github/copilot-instructions.md` for always-on, repository-wide guidance.
3. Update each file's `applyTo` glob if project names or folder structure differ.
4. Commit these files so collaborators and CI Copilot workflows use the same guidance.

## Recommended Companion Repo Layout

```text
.github/
  copilot-instructions.md
  instructions/
    README.md
    aspnet-mvc.instructions.md
    ef-core.instructions.md
    security.instructions.md
```

## Notes

- Keep instruction wording short and directive so it remains actionable.
- Prefer specific `applyTo` globs over broad patterns to reduce irrelevant context.
- Review these files whenever architecture, security posture, or data access conventions change.