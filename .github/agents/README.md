# LeaveManagementSystem Custom Agents

This folder contains repository-scoped custom agent definitions for focused review workflows. These files can be copied into a companion repository to preserve the same specialized review behavior.

## Files In This Folder

1. `aspnet-security-reviewer.agent.md`
   - Name: `aspnet-security-reviewer`
   - Purpose: Reviews ASP.NET Core MVC, Identity, authorization, configuration, and deployment changes for secure-by-default behavior.
   - Typical use: Security-focused review of auth, antiforgery, secrets/configuration, and logging exposure.

2. `efcore-performance-reviewer.agent.md`
   - Name: `efcore-performance-reviewer`
   - Purpose: Reviews EF Core entities, queries, migrations, and service-layer data access for correctness, performance, and maintainability.
   - Typical use: Data access review for query efficiency, write-path safety, relationship configuration, and migration quality.

## How To Use In A Companion Repo

1. Copy this folder to `.github/agents/` in the companion repository.
2. Keep agent `name` values stable if you reference them from automations or team docs.
3. Adjust wording to match any architecture differences in the companion codebase.
4. Commit with related instruction files so agent behavior and coding standards stay aligned.

## Recommended Companion Repo Layout

```text
.github/
  agents/
    README.md
    aspnet-security-reviewer.agent.md
    efcore-performance-reviewer.agent.md
```

## Notes

- Keep descriptions explicit so the correct agent is selected when tasks are routed.
- Keep agent prompts review-oriented unless you intentionally want code-generation behavior.
- Update checklists when your security baseline or data access patterns change.
