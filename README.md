# Todo API

A production-style Todo REST API built with ASP.NET Core and DynamoDB, following Clean Architecture and CQRS patterns.

## Architecture

Four-layer Clean Architecture with strict dependency rules:

- **API** — Controllers, middleware, Swagger, DI registration
- **Application** — MediatR handlers, commands/queries, DTOs, FluentValidation
- **Domain** — Entities and value objects with no external dependencies
- **Infrastructure** — DynamoDB repository implementations and AWS SDK wiring

## Stack

- ASP.NET Core Web API (.NET)
- MediatR (CQRS)
- FluentValidation
- AWS DynamoDB
- xUnit + NSubstitute + FluentAssertions
- Docker

## Running Locally

```bash
docker-compose up
dotnet run --project src/TodoApi.API
```

```bash
dotnet test
```
