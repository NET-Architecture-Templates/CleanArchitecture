# Clean Architecture – Project Template

This repository is an **example template** of Clean Architecture for .NET projects.  
It is **not a framework**, nor a closed solution, and **should not be used as a rigid boilerplate**.

The goal is to **demonstrate a project organization**, responsibilities and architectural boundaries
that can be adapted according to the system's context.

---

## 🎯 Template Objective

This template exists to:

- Demonstrate **clear separation of responsibilities**
- Serve as **architectural reference** for .NET projects
- Support **conscious architectural decisions**
- Facilitate **testability, maintenance and evolution**
- Avoid common couplings (e.g.: API dependent on EF/Core or infrastructure leaking into domain)

> ⚠️ **Important**  
> This repository **does not attempt to solve all scenarios** nor impose absolute rules.  
> Clean Architecture is a **guide**, not a fixed recipe.

---

## 🧱 Project Structure

The solution is organized in layers, each with a clear responsibility.
```
src/
 ├── Api/
 ├── Application/
 ├── Domain/
 ├── Infrastructure/
 └── Tests/
     ├── Domain.Tests
     └── Application.Tests
```

## 🧠 Layers Overview

### 🔹 Domain

**Responsibility:**  
Represent the business core.

**Contains:**
- Entities
- Value Objects
- Business rules
- Repository interfaces (contracts)
- Domain exceptions

**Does not contain:**
- Frameworks
- Database access
- HTTP / Controllers
- Logging
- External dependencies

> The domain doesn't know the system is an API nor how data is persisted.

---

### 🔹 Application

**Responsibility:**  
Orchestrate the system's use cases.

**Contains:**
- Services / Use Cases
- DTOs
- External service interfaces
- Application rules
- Flow validations

**Here are decisions like:**
- Create or update entities
- Orchestrate multiple operations
- Coordinate calls to repositories and services

> The Application layer depends only on Domain.

---

### 🔹 Infrastructure

**Responsibility:**  
Implement technical details.

**Contains:**
- Repository implementations
- Persistence (SQL, MongoDB, etc.)
- External integrations
- Third-party services
- Technical configurations

This layer implements interfaces defined in Domain or Application.

> Infrastructure is replaceable.  
> Domain shouldn't be.

---

### 🔹 API

**Responsibility:**  
Expose the system to the external world.

**Contains:**
- Controllers
- Filters
- Middlewares
- Dependency Injection configuration
- API versioning

**The API:**
- Does not contain business rules
- Does not access database directly
- Acts only as entry layer

---

### 🔹 Tests

Clear separation of tests by layer:

- **Domain.Tests**  
  Tests pure business rules, without external dependencies.

- **Application.Tests**  
  Tests use cases, flows and orchestrations.

---

## 🔄 Dependency Flow

The main Clean Architecture rule:
```
API → Application → Domain
Infrastructure → Application / Domain (via interfaces)
```

**Never:**
- Domain → Infrastructure
- Domain → API
- Application → Infrastructure directly

---

## 🧩 When to Use This Template

This template is indicated when:
- The system has relevant business rules
- There is complexity beyond CRUD
- Testability is important
- The project tends to grow
- Maintainability and evolution are priorities

---

## 🚫 When NOT to Use

Avoid this template when:
- The project is extremely simple
- It's a disposable MVP
- Small scripts, automations or proof of concepts
- Temporary or short-lived APIs

> Overengineering is also an architectural problem.

---

## ⚙️ Adapt to Context

You don't need to:
- Create all layers from the start
- Follow exactly the project names
- Use all suggested folders

Use this repository as:
- Guide
- Reference
- Base for architectural discussion

---

## 🧠 Philosophy

> "Architecture exists to protect business from technical changes."

If you change:
- Database
- Framework
- Infrastructure
- Protocol (REST → gRPC)

…the impact on domain should be minimal.

---

## 📌 Final Notes

This template represents a practical interpretation of Clean Architecture in the .NET ecosystem.  
It's not the only correct way — and doesn't claim to be.

The focus is clarity, separation of responsibilities and sustainable evolution.
