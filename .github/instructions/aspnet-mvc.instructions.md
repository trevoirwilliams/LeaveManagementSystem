---
applyTo: "LeaveManagementSystem.Web/**/*.{cs,cshtml,json}"
---

# ASP.NET Core MVC Instructions

Use these instructions for controllers, Razor views, Identity pages, filters, middleware, and web configuration.

- Keep controllers thin.
- Place business rules in application services.
- Use strongly typed view models.
- Validate `ModelState` before performing state changes.
- Use `[HttpPost]` and `[ValidateAntiForgeryToken]` for form submissions.
- Use `[Authorize]` on protected controllers/actions.
- Use named policies for admin/supervisor workflows.
- Ensure `app.UseAuthentication()` appears before `app.UseAuthorization()`.
- Do not expose debug-only controllers, endpoints, stack traces, or diagnostics in production.
- Use TempData sparingly for user-facing status messages.
- Prefer partial views or view components for reusable UI.
- Keep Razor views presentation-focused.
- Avoid database access directly from views.