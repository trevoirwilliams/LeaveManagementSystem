# LeaveManagementSystem Skills

This folder contains task-specific Copilot skills. Skills are used for focused, repeatable workflows and provide structured guidance for reviews or implementations in a specific domain.

## Skills In This Folder

1. `aspnet-security-hardening`
   - File: `aspnet-security-hardening/SKILL.md`
   - Purpose: Security hardening guidance for authentication, authorization, MVC forms, configuration, secrets, logging, and deployment.
   - Typical use: Security-sensitive ASP.NET Core MVC changes and secure-by-default reviews.

2. `efcore-data-access-review`
   - File: `efcore-data-access-review/SKILL.md`
   - Purpose: EF Core data access review workflow for query design, write safety, relationships, migrations, and leave workflow validation.
   - Typical use: Reviewing or changing entities, queries, DbContext behavior, and service-layer persistence logic.

## How To Use In A Companion Repo

1. Copy this folder to `.github/skills/` in the companion repository.
2. Preserve each skill folder name and `name` in frontmatter to avoid discovery mismatches.
3. Update examples and validation commands if solution or project names differ.
4. Keep skill descriptions specific so automatic skill selection is reliable.

## Recommended Companion Repo Layout

```text
.github/
  skills/
    README.md
    aspnet-security-hardening/
      SKILL.md
    efcore-data-access-review/
      SKILL.md
```

## Notes

- Skills should be concise and workflow-oriented, not broad policy documents.
- If a guideline applies to nearly all code, place it in `copilot-instructions.md` or file instructions instead of a skill.
- Review and update skills whenever your architecture, security requirements, or EF Core conventions evolve.
