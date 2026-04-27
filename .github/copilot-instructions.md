# GitHub Copilot Instructions — LeaveManagementSystem

## Project identity

This repository contains a layered ASP.NET Core MVC Leave Management System for employees, supervisors, and administrators. The application supports leave requests, leave approvals, leave types, allocations, periods, user management, email notifications, and role-based access.

Treat this as a production-style educational application. Preserve clarity for learners, but prefer modern, secure, maintainable .NET 10 patterns.

## Target platform

- Target .NET 10 for all new development.
- Prefer `net10.0` for project target frameworks unless a task explicitly requires another version.
- Use C# modern language features where they improve readability.
- Keep nullable reference types enabled.
- Keep implicit usings enabled.
- Prefer async APIs for I/O, EF Core, email, identity, and external service operations.
- Add `CancellationToken` parameters to service and data-access methods when introducing or refactoring async workflows.

## Architecture conventions

The solution uses a layered structure:

- `LeaveManagementSystem.Web`
  - ASP.NET Core MVC application.
  - Controllers, Views, Identity UI, `Program.cs`, web configuration, static assets.
- `LeaveManagementSystem.Application`
  - Application services, DTOs/view models, AutoMapper profiles, business workflows.
- `LeaveManagementSystem.Data`
  - EF Core DbContext, Identity user, entities, configurations, migrations.
- `LeaveManagementSystem.Common`
  - Shared constants and reusable static values.

Respect the current separation:

- Controllers should orchestrate HTTP concerns only.
- Business logic belongs in application services.
- EF Core queries and persistence concerns should not be pushed into views.
- Views should use strongly typed view models.
- Do not expose EF Core entities directly to views if a view model exists or should exist.
- Avoid putting business rules in Razor views.

## ASP.NET Core MVC conventions

- Use constructor injection for dependencies.
- Keep controller actions small and intention-revealing.
- Validate `ModelState` before processing POST requests.
- Use `[ValidateAntiForgeryToken]` on unsafe form actions unless there is a clear framework-provided alternative.
- Use `[Authorize]` and named policies for protected workflows.
- Prefer policy-based authorization over scattered role string checks.
- For admin/supervisor workflows, use the existing role/policy pattern rather than ad hoc checks.
- Redirect after successful POST operations to avoid duplicate form submissions.
- Return `NotFound()` or `Forbid()` explicitly when the current user should not access a resource.
- Do not create a `TestController` or debugging endpoint in production code.

## Authentication and authorization

- Ensure the middleware order is correct:
  1. `app.UseRouting()`
  2. `app.UseAuthentication()`
  3. `app.UseAuthorization()`
  4. endpoint mappings
- Do not remove Identity configuration without replacing it with an equivalent secure design.
- Do not weaken password, lockout, token, cookie, or role settings.
- Do not hardcode default production admin credentials.
- Use named constants for roles and policies.
- Treat authorization as both UI-level and server-side enforcement. Hiding a button is not authorization.

## EF Core and data access

- Use EF Core async methods: `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, `AnyAsync`, `SaveChangesAsync`.
- Use `AsNoTracking()` for read-only queries.
- Prefer projection with `Select` into view models/DTOs when returning data to the UI.
- Avoid lazy-loading assumptions unless explicitly configured.
- Avoid N+1 queries. Use projection or explicit includes intentionally.
- Keep migrations in `LeaveManagementSystem.Data`.
- Keep entity configuration in dedicated configuration classes where practical.
- Never concatenate SQL strings with user input.
- Use transactions only when a workflow genuinely spans multiple persistence operations that must succeed or fail together.
- Do not use EF Core entities as form post models when overposting is possible.

## Security baseline

- Never commit secrets, publish profiles, passwords, API keys, or production connection strings.
- Use user secrets for local development and environment variables/Azure App Settings/Key Vault for deployed configuration.
- Production SQL connections should use encrypted connections unless explicitly justified.
- Avoid `Encrypt=false` in production connection strings.
- Do not log passwords, tokens, cookies, connection strings, personal data, or full exception details to end users.
- Use secure cookie settings in production.
- Prefer centralized exception handling and friendly error pages.
- Keep HSTS enabled outside Development.
- Use HTTPS redirection.
- Treat all user input as untrusted.

## Logging and observability

- Use structured logging through `ILogger<T>` or the configured logging provider.
- Log business events such as leave request submission, approval, rejection, allocation changes, and admin actions.
- Include useful context such as request id, user id, leave request id, and operation name.
- Do not log sensitive personal details unnecessarily.
- Prefer logs that help diagnose a production issue without exposing sensitive data.

## Testing expectations

For every meaningful feature change:

- Add or update tests.
- Prefer unit tests for application services.
- Prefer integration tests for controller, authentication, authorization, and EF Core behavior.
- Use clear test names: `MethodOrScenario_State_ExpectedResult`.
- Cover authorization boundaries, validation failures, happy paths, and edge cases.
- Do not claim a change is complete until restore, build, and tests pass.

## CI expectations

- Prefer solution-level commands:
  - `dotnet restore LeaveManagementSystem.sln`
  - `dotnet build LeaveManagementSystem.sln --configuration Release --no-restore`
  - `dotnet test LeaveManagementSystem.sln --configuration Release --no-build`
- Use .NET 10 SDK in CI.
- Keep GitHub Actions pinned to current major versions.
- Do not deploy from CI unless build and tests pass.
- Avoid putting publish profiles or deployment secrets in source control.

## Code style

- Use clear, descriptive names.
- Keep methods small and focused.
- Avoid unnecessary abstractions.
- Avoid broad catch blocks unless they add value.
- Prefer guard clauses for invalid inputs.
- Prefer records for immutable request/response models when appropriate.
- Prefer primary constructors only when they improve readability.
- Keep public APIs clean and documented where useful.
- Do not introduce a new package unless it provides clear value and is compatible with .NET 10.

## Documentation

When changing architecture, authentication, authorization, deployment, or database behavior:

- Update `README.md`.
- Document required configuration keys.
- Document migration steps.
- Document how to run the application locally.
- Document how to run tests.