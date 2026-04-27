# Leave Management System

A production-style, layered **ASP.NET Core MVC** application for managing employee leave requests, approvals, allocations, and reporting. Built as the hands-on project for the Udemy course below - it prioritises clarity for learners while demonstrating real-world, secure, maintainable .NET patterns.

---

## Related Udemy Course

**[Complete ASP.NET Core and Entity Framework Development](https://www.udemy.com/course/complete-aspnet-core-31-and-entity-framework-development/?referralCode=739749EF600855CEE34F)**
*by Trevoir Williams*

This course teaches you to build a complete, data-driven web application from scratch using ASP.NET Core and Entity Framework Core. Topics covered include:

- MVC architecture (Models, Views, Controllers)
- ASP.NET Core Identity - authentication and role-based authorization
- Entity Framework Core - Code-First, migrations, and data seeding
- Repository pattern and dependency injection
- AutoMapper and view models
- Asynchronous programming
- Email service integration
- Serilog structured logging
- Bootstrap and front-end integration
- Source control with GitHub
- Deployment to IIS and Microsoft Azure
- Automated CI/CD with GitHub Actions and Azure DevOps
- **Responsible use of AI tools** (dedicated course section - see below)

> **Who is this for?** Anyone learning data-driven ASP.NET Core development, developers transitioning from .NET Framework, and beginners who want a strong foundation in enterprise-style .NET web applications.

---

## Technology Stack and Versions

| Component | Version |
|---|---|
| .NET / ASP.NET Core | **10.0** |
| C# | **13** |
| Entity Framework Core | **10.0.7** |
| ASP.NET Core Identity | **10.0.7** |
| AutoMapper | **16.1.1** |
| Serilog | **4.3.1** |
| Serilog.AspNetCore | **10.0.0** |
| Serilog.Settings.Configuration | **10.0.0** |
| Serilog.Sinks.File | **7.0.0** |
| Serilog.Sinks.Seq | **9.0.0** |
| SQL Server | 2019 or later (LocalDB supported for development) |
| Visual Studio | 2022 17.12+ / VS Code with C# Dev Kit |

---

## Solution Architecture

The solution is split into four focused projects:

```
LeaveManagementSystem.sln
+-- LeaveManagementSystem.Web          # ASP.NET Core MVC - controllers, views, Program.cs
+-- LeaveManagementSystem.Application  # Services, DTOs/view models, AutoMapper profiles
+-- LeaveManagementSystem.Data         # EF Core DbContext, entities, migrations, Identity
+-- LeaveManagementSystem.Common       # Shared constants (roles, etc.)
```

**Key conventions:**
- Controllers handle HTTP concerns only; business logic lives in application services.
- Views use strongly typed view models - EF Core entities are never exposed directly to views.
- Authorization is enforced server-side, not just at the UI level.
- Async/await is used throughout all I/O, EF Core, and Identity operations.
- Secrets are managed via .NET User Secrets locally and environment variables / Azure App Settings in production.

---

## Features

### Employee
- Submit leave requests with type, date range, and optional comments
- View personal leave balances per leave type and period
- Review the status history of all own requests

### Supervisor / Administrator
- Review, approve, or reject leave requests with comments
- Manage leave types (create, edit, delete)
- Manage leave periods and allocations per employee
- View and filter leave records across the organisation
- Manage user accounts and role assignments

---

## Prerequisites

- [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0)
- SQL Server 2019+ **or** SQL Server LocalDB (included with Visual Studio)
- Visual Studio 2022 17.12+ **or** VS Code with the C# Dev Kit extension
- *(Optional)* [Seq](https://datalust.co/seq) for structured log viewing locally

---

## Running the Application Locally

### 1. Clone the repository

```bash
git clone https://github.com/trevoirwilliams/LeaveManagementSystem.git
cd LeaveManagementSystem
```

### 2. Configure user secrets

Never put real connection strings in `appsettings.json` committed to source control. Use .NET User Secrets for local development:

```bash
cd LeaveManagementSystem.Web
dotnet user-secrets set "ConnectionStrings:DefaultConnection" "Server=(localdb)\mssqllocaldb;Database=LeaveManagement;Trusted_Connection=True;"
```

Alternatively, edit `appsettings.Development.json` (which is git-ignored) with your local SQL Server connection string.

### 3. Apply database migrations

```bash
# From the solution root
dotnet ef database update --project LeaveManagementSystem.Data --startup-project LeaveManagementSystem.Web
```

Or from the Package Manager Console in Visual Studio - set the **Default Project** to `LeaveManagementSystem.Data`, then run:

```powershell
Update-Database
```

### 4. Restore, build, and run

```bash
dotnet restore LeaveManagementSystem.sln
dotnet build LeaveManagementSystem.sln --configuration Release
dotnet run --project LeaveManagementSystem.Web
```

Or press **F5** in Visual Studio with `LeaveManagementSystem.Web` set as the startup project.

### 5. Access the application

```
https://localhost:7xxx/    (port shown in terminal output)
```

**Default seeded admin account (development only):**

| Field | Value |
|---|---|
| Username | admin@localhost.com |
| Password | Password1234! |

> **Security note:** Change or remove the seeded admin credentials before deploying to any shared or production environment. Do not commit real credentials to source control.

---

## Running Tests

```bash
dotnet test LeaveManagementSystem.sln --configuration Release
```

---

## Configuration Reference

| Key | Location | Description |
|---|---|---|
| `ConnectionStrings:DefaultConnection` | User Secrets / env var | SQL Server connection string |
| `EmailSettings:*` | User Secrets / env var | SMTP configuration for leave notification emails |
| `Serilog:*` | `appsettings.json` | Structured logging sinks and minimum levels |

Production deployments should supply all secrets via environment variables or Azure Key Vault - never via committed config files.

---

## Responsible Use of AI in This Project

The associated Udemy course includes a dedicated section - **Responsible Use of AI Tools** - covering how to use AI assistants (such as GitHub Copilot) effectively and ethically during software development.

The following principles are applied in this codebase:

- **AI as a collaborator, not a replacement for understanding.** Every AI-assisted change is reviewed, tested, and understood before it is committed. Students are expected to understand the code they ship, not just accept generated output.
- **Verify before you trust.** AI suggestions are checked against official documentation, compiler output, and test results. Hallucinated package versions, deprecated APIs, and insecure patterns are caught during review.
- **Security is non-negotiable.** AI-generated code is reviewed against the OWASP Top 10. SQL injection, insecure secrets handling, missing authorization checks, and overposting vulnerabilities are common AI blind spots that require human vigilance.
- **No sensitive data in prompts.** Connection strings, credentials, personal data, and proprietary business logic are never included in prompts sent to external AI services.
- **Attribution and academic integrity.** In an educational context, using AI to generate solutions without understanding them undermines the learning objective. AI is a tool to accelerate understanding - not a shortcut around it.
- **Prefer small, targeted prompts.** Asking AI to generate entire features at once leads to code that is harder to review and verify. Smaller, focused requests produce better, safer results.

---

## Contributing

Pull requests are welcome. For major changes, open an issue first to discuss the proposed change. Ensure `dotnet build` and `dotnet test` pass before submitting.

---

## License

This project is provided for educational purposes as the companion codebase for the Udemy course listed above. See the course page for terms of use.
