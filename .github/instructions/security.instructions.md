---
applyTo: "**/*.{cs,cshtml,json,yml,yaml,config,ps1,sh}"
---

# Security Instructions

Use these instructions for authentication, authorization, configuration, CI/CD, logging, and data-handling changes.

- Never commit secrets, passwords, tokens, API keys, publish profiles, or production connection strings.
- Do not add default production credentials.
- Do not log secrets, tokens, cookies, passwords, connection strings, or sensitive personal data.
- Use user secrets locally and environment variables or Azure App Settings/Key Vault in deployed environments.
- Production SQL connections must use encryption unless there is a documented exception.
- Keep HSTS and HTTPS redirection enabled outside Development.
- Preserve Identity security unless explicitly asked to replace it.
- Do not weaken password, lockout, cookie, token, or authorization settings.
- Apply authorization checks server-side, not only in the UI.
- Protect state-changing MVC actions with antiforgery validation.
- Use secure defaults before adding custom security mechanisms.
- Add or update tests for authorization-sensitive changes.