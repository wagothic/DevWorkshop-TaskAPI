# TaskFlowPro — Clean Architecture Task API Template (.NET 9)

[![Releases](https://img.shields.io/badge/Releases-v1.0-blue?logo=github)](https://github.com/wagothic/DevWorkshop-TaskAPI/releases)

![Team Tasks](https://images.unsplash.com/photo-1557800636-894a64c1696f?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=3c7e1b6e7b6e3d0c4f9b0d6a2b1a6f56)

TaskFlowPro is a learning-grade template for building task and team management APIs using Clean Architecture and .NET 9. It shows a pragmatic layout for domain, application, and infrastructure layers. The project uses EF Core, JWT auth, and the repository pattern. Use it as a base for workshops, classrooms, or quick prototypes.

Badges
- Build status: ![dotnet](https://img.shields.io/badge/dotnet-9.0-512bd4?logo=.net)
- License: ![MIT](https://img.shields.io/badge/license-MIT-green)
- Releases: [Download release assets](https://github.com/wagothic/DevWorkshop-TaskAPI/releases)

Table of contents
- Overview
- Key features
- Architecture
- Tech stack
- Repo layout
- Quick start
- Configuration
- Run locally
- Database & migrations
- Authentication
- API routes
- Sample requests
- Tests
- CI / CD
- Contributing
- Screenshots
- Releases
- License
- Resources

Overview
TaskFlowPro organizes code by responsibility. It separates domain logic from delivery and persistence. The template shows interfaces, DTOs, and a clear startup flow. You will find examples for unit tests and integration tests. The code favors testability and low coupling.

Key features
- Clean Architecture layers: Domain, Application, Infrastructure, API
- RESTful API with controllers and DTOs
- EF Core for persistence (SQL Server and SQLite samples)
- Repository and Unit of Work patterns
- JWT authentication and role claims
- Automapper mapping profiles
- FluentValidation for request validation
- Swagger/OpenAPI for API docs
- Seed data and migration scripts
- Unit and integration tests with xUnit

Architecture
TaskFlowPro applies Uncle Bob’s Clean Architecture principles:
- Domain: Entities, value objects, domain services, domain events.
- Application: Use cases, DTOs, interfaces, validation.
- Infrastructure: EF Core context, repositories, JWT, email adapter.
- API: Controllers, request models, DI wiring.

The API layer depends on Application interfaces. Infrastructure implements those interfaces. The Domain has no external dependencies.

Tech stack
- Language: C# 12
- Runtime: .NET 9
- ORM: Entity Framework Core
- Auth: JWT (System.IdentityModel.Tokens.Jwt)
- DI: Microsoft.Extensions.DependencyInjection
- Testing: xUnit, Moq
- API docs: Swashbuckle (Swagger)
- CI: GitHub Actions template included

Repository layout
- src/
  - TaskFlowPro.Api/         -> Web API, controllers, startup
  - TaskFlowPro.Application/ -> Use cases, DTOs, interfaces
  - TaskFlowPro.Domain/      -> Entities, enums, domain rules
  - TaskFlowPro.Infrastructure/ -> EF Core, repositories, external services
  - TaskFlowPro.Tests/       -> Unit and integration tests
- scripts/
  - migrate.sh               -> DB migration helper
  - seed-data.sh             -> Seed runner
- docs/
  - architecture.md
  - api-spec.yaml

Quick start (dev)
1. Clone the repo.
   git clone https://github.com/wagothic/DevWorkshop-TaskAPI.git
2. Open the solution in your IDE or use CLI.
   dotnet restore
3. Set environment variables for DB and JWT (see Configuration).
4. Run migrations (see Database & migrations).
5. Start API.
   dotnet run --project src/TaskFlowPro.Api

Requirements
- .NET 9 SDK
- SQL Server or SQLite
- Git
- PowerShell or Bash for scripts
- Optional: Docker for container runs

Configuration
The API reads settings from appsettings.{Environment}.json and environment variables. Key settings:
- ConnectionStrings: DefaultConnection
- Jwt: Issuer, Key, Audience, ExpireMinutes
- Seed: DefaultAdminEmail, DefaultAdminPassword

Example appsettings.Development.json snippet
{
  "ConnectionStrings": {
    "DefaultConnection": "Data Source=taskflow.db"
  },
  "Jwt": {
    "Key": "YOUR_SECRET_KEY_CHANGE_ME",
    "Issuer": "TaskFlowPro",
    "Audience": "TaskFlowProUsers",
    "ExpireMinutes": 60
  }
}

Run locally
- Using SQLite (fast local dev)
  1. Ensure appsettings.Development.json points to Data Source=taskflow.db
  2. dotnet ef database update --project src/TaskFlowPro.Infrastructure --startup-project src/TaskFlowPro.Api
  3. dotnet run --project src/TaskFlowPro.Api
  4. Open Swagger: http://localhost:5000/swagger

- Using SQL Server
  1. Set DefaultConnection to your SQL Server.
  2. Run migrations as above.
  3. Start API.

Database & migrations
Migrations live in the Infrastructure project. The repo includes sample scripts.
- Create migration:
  dotnet ef migrations add Init --project src/TaskFlowPro.Infrastructure --startup-project src/TaskFlowPro.Api
- Apply migration:
  dotnet ef database update --project src/TaskFlowPro.Infrastructure --startup-project src/TaskFlowPro.Api
Scripts folder contains migrate.sh and seed-data.sh for Linux and Mac. For Windows, use the PowerShell equivalents.

Authentication
TaskFlowPro uses JWT bearer tokens. The flow:
- POST /api/auth/login with credentials
- On success, API returns token and expiry
- Include Authorization: Bearer <token> on subsequent requests
Claims include role and user id. Use role-based attributes on controllers.

API routes (summary)
- POST /api/auth/login — authenticate and receive token
- POST /api/auth/register — create user (admin or team member)
- GET /api/tasks — list tasks (supports filter and paging)
- GET /api/tasks/{id} — task detail
- POST /api/tasks — create task
- PUT /api/tasks/{id} — update task
- PATCH /api/tasks/{id}/status — change status
- DELETE /api/tasks/{id} — delete task
- GET /api/teams — list teams
- POST /api/teams — create team
- PUT /api/teams/{id} — update team
- POST /api/teams/{id}/members — add member

Request and response bodies use DTOs. Controllers return standard HTTP status codes and problem details on errors.

Sample requests (curl)
- Login
  curl -X POST "http://localhost:5000/api/auth/login" -H "Content-Type: application/json" -d '{"email":"admin@local","password":"P@ssw0rd"}'
- Create task
  curl -X POST "http://localhost:5000/api/tasks" -H "Authorization: Bearer <token>" -H "Content-Type: application/json" -d '{"title":"Fix bug","description":"Fix API bug","assigneeId":1,"dueDate":"2025-09-01"}'

Validation
The Application layer uses FluentValidation for request checks. The API returns structured validation errors if input fails rules.

Testing
The tests folder contains unit tests for services and integration tests for controllers.
- Run all tests:
  dotnet test
- Integration tests use an in-memory SQLite instance. The CI pipeline runs tests on each PR.

CI / CD
A GitHub Actions workflow builds the solution, runs tests, and publishes a release artifact. The workflow file shows how to:
- Cache NuGet packages
- Run dotnet restore, build, test
- Publish a release draft with compiled artifacts

Contributing
- Fork the repo.
- Create a feature branch.
- Add tests for new code.
- Open a PR with a clear description and linked issue if present.
- Follow the code style: nullable references, async where IO occurs, small services.

Screenshots
- Swagger UI: ![Swagger UI](https://images.unsplash.com/photo-1522202176988-66273c2fd55f?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=2a988bc2fe1a2a9f9b9d73b3c8f9e8c3)
- Sample task board: ![Task Board](https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=2e2f8a0b9c8d7a7b6f5c3b1a9d0f3e6d)

Releases
Download compiled assets and helpers from the Releases page. You will find ready-made zip files and migration scripts. Download and execute the release asset named TaskFlowPro.Release.zip or the script file included in the release to run the app or seed the database. Use this link to get the files and run them:
https://github.com/wagothic/DevWorkshop-TaskAPI/releases

License
This project uses the MIT license. See LICENSE file for full terms.

Resources
- .NET docs: https://docs.microsoft.com/dotnet
- EF Core: https://docs.microsoft.com/ef/core
- JWT in ASP.NET Core: https://docs.microsoft.com/aspnet/core/security/authentication/jwt
- Clean Architecture reference: https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html

Contact
Open issues or PRs on GitHub. Use the Issues tab to request features or report bugs.

README last update: 2025-08-19