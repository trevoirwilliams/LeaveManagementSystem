---
name: aspnet-security-hardening
description: Use this skill when reviewing or changing authentication, authorization, Identity, MVC forms, configuration, secrets, logging, or deployment behavior.
---

# ASP.NET Core Security Hardening Skill

Use this skill for security-sensitive ASP.NET Core MVC changes.

## Security checklist

1. Authentication and authorization:
   - Confirm Identity is configured intentionally.
   - Confirm `UseAuthentication()` appears before `UseAuthorization()`.
   - Confirm protected controllers/actions have `[Authorize]` or policy enforcement.
   - Confirm role/policy checks happen server-side.

2. MVC forms:
   - Confirm unsafe form posts use `[HttpPost]`.
   - Confirm unsafe form posts use `[ValidateAntiForgeryToken]`.
   - Confirm posted models avoid overposting.
   - Confirm `ModelState.IsValid` is checked.

3. Configuration:
   - Do not commit secrets.
   - Do not commit production publish profiles.
   - Do not commit real production connection strings.
   - Avoid `Encrypt=false` in production SQL connections.
   - Prefer user secrets locally and environment variables/Azure App Settings/Key Vault in production.

4. Logging:
   - Use structured logs.
   - Do not log passwords, tokens, cookies, connection strings, or sensitive personal data.
   - Do not show raw exception details to users outside Development.

5. Deployment:
   - Preserve HSTS outside Development.
   - Preserve HTTPS redirection.
   - Ensure deployment depends on successful build and tests.

## Required output

For every finding, provide:

- File
- Concern
- Risk
- Recommended fix
- Test to add or update