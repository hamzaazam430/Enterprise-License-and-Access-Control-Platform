# Enterprise License & Access Control Platform (ELACP)

## Overview

The **Enterprise License & Access Control Platform (ELACP)** is a production-grade, multi-tenant SaaS backend designed to manage **subscriptions, licenses, device binding, and role-based access control** for enterprise software distribution.

This project is intentionally built as a **senior-level flagship system** to demonstrate real-world system design, clean architecture, security practices, and scalability considerations.

---

## Key Capabilities

* Multi-tenant SaaS architecture
* JWT-based authentication with refresh tokens
* Role-Based Access Control (RBAC) with policy enforcement
* Subscription plans with license limits
* License generation, assignment, and revocation
* One-license–one-device enforcement (device binding)
* Secure license validation APIs for client applications
* Centralized audit logging
* Dockerized deployment with CI/CD readiness

---

## Architecture

### Architectural Style

* **Modular Monolith**
* **Hexagonal Architecture (Ports & Adapters)**

This approach provides:

* Strong domain isolation
* High maintainability
* Clear separation of concerns
* A clean migration path to microservices if needed

### High-Level Layers

* **API Layer** – REST controllers
* **Application Layer** – Use cases and orchestration
* **Domain Layer** – Business rules and entities
* **Infrastructure Layer** – Database, persistence, external adapters

---

## Modules

| Module       | Description                                  |
| ------------ | -------------------------------------------- |
| Auth         | Authentication, JWT issuance, refresh tokens |
| Tenant       | Organization (tenant) lifecycle management   |
| User         | User accounts and credentials                |
| RBAC         | Roles, permissions, and access policies      |
| Subscription | Plans, license limits, expiry                |
| License      | License pool generation and assignment       |
| Device       | Device fingerprinting and binding            |
| Enforcement  | Runtime license validation                   |
| Audit        | Security and activity logging                |
| Shared       | Common utilities and infrastructure          |

---

## Core Use Cases

* Platform admin creates and manages organizations (tenants)
* Organizations receive subscriptions with license quotas
* Org admins create users and assign roles
* Licenses are assigned to users and bound to devices
* Client applications validate licenses securely at runtime
* Admins revoke licenses or devices centrally
* All sensitive actions are audit logged

---

## Data Model

The system uses a relational data model designed for clarity, integrity, and scalability.

**Core entities include:**

* Tenant
* User
* Role
* Subscription
* License
* Device
* LicenseAssignment
* AuditLog

An ERD diagram is included in the `/docs` directory.

---

## API Documentation

All APIs are documented using **OpenAPI (Swagger)**.

Once the application is running:

```
http://localhost:3000/docs
```

---

## Security Design

* Password hashing using industry-standard algorithms
* Stateless JWT authentication
* Refresh token rotation
* Role-based authorization checks at API and service layers
* Device fingerprint validation
* Rate limiting on sensitive endpoints

---

## Tech Stack

### Backend

* Node.js (Fastify) **or** Java Spring Boot
* PostgreSQL
* Prisma / TypeORM (Node) or JPA (Java)

### DevOps

* Docker & Docker Compose
* GitHub Actions (CI)

---

## Local Development Setup

### Prerequisites

* Docker
* Docker Compose
* Node.js or Java (depending on implementation)

### Run Locally

```
docker-compose up --build
```

The API will be available at:

```
http://localhost:3000
```

---

## CI/CD

The project includes a basic CI pipeline:

* Linting
* Automated tests
* Docker image build

This pipeline is designed to be easily extended for cloud deployments.

---

## Design Decisions (Why This Matters)

* **Modular Monolith over Microservices**: reduces complexity while preserving clean boundaries
* **Hexagonal Architecture**: enables testability and long-term maintainability
* **Explicit RBAC & Policies**: mirrors real enterprise security models
* **License Enforcement Layer**: separates business rules from transport concerns

---

## Future Enhancements

* Payment gateway integration
* Usage analytics and reporting
* Event-driven architecture (Kafka/RabbitMQ)
* Service decomposition into microservices
* Offline license caching

---

## Who This Project Is For

This project is intended to demonstrate:

* Senior-level backend engineering skills
* System design and architecture expertise
* Security-first thinking
* Real-world SaaS product development

It is suitable for **technical interviews, portfolio reviews, and architectural discussions**.

---

## License

This project is provided for educational and portfolio purposes.
