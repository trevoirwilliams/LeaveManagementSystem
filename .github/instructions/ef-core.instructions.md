---
applyTo: "LeaveManagementSystem.Data/**/*.cs,LeaveManagementSystem.Application/Services/**/*.cs"
---

# EF Core Data Access Instructions

Use these instructions when modifying entities, DbContext configuration, migrations, repositories, services, and queries.

- Use async EF Core APIs.
- Add `CancellationToken` support to new async service/data methods.
- Use `AsNoTracking()` for read-only queries.
- Use projection with `Select` for list/detail screens when entity tracking is unnecessary.
- Avoid returning EF Core entities directly to views.
- Avoid overposting by using view models or command models.
- Keep migrations in the data project.
- Keep entity configuration explicit for required properties, max lengths, relationships, delete behavior, indexes, and concurrency where needed.
- Avoid N+1 queries.
- Avoid client-side evaluation of large datasets.
- Do not concatenate SQL from user input.
- Use transactions intentionally and narrowly.
- Treat leave approval/allocation workflows as business-critical operations requiring validation and authorization.